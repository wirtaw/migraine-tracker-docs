# 🔑 Key Management & Rotation (Edge Worker)

To ensure the highest level of security and compliance for our users' health logs, the symmetric encryption keys used by our NestJS `SymmetricKeyService` are not hardcoded or stored in the primary MongoDB instance.

Instead, we utilize a **Cloudflare Worker** to securely generate, serve, and rotate these keys at the edge.

## 🏗️ Why a Cloudflare Worker?

1. **Isolation:** If the main backend monolith is ever compromised, the attacker still cannot access the master rotation logic or historical key vaults.
2. **Speed:** Running at the edge means our monolith can fetch the daily encryption key with almost zero latency.
3. **Automated Rotation:** The worker runs on a cron-trigger, automatically deprecating old keys and generating new ones without requiring manual backend deployments.

## 🔄 The Rotation Lifecycle

Here is how our NestJS backend interacts with the Cloudflare Worker:

1. **Daily Key Generation:** Every 24 hours, the Cloudflare Worker generates a fresh, cryptographically secure AES-256 key. It stores this key in a secure Cloudflare KV (Key-Value) store, tagged with the current date/version (e.g., `v:2026-03-08`).
2. **Backend Request:** When a user logs a new migraine incident, the NestJS `SymmetricKeyService` requests the *active* encryption key from the Worker via a secure, authenticated internal route.
3. **Encryption:** The payload is encrypted using this key. The database saves the encrypted string *and* the Key Version ID (e.g., `payload: "encrypted_string...", key_version: "v:2026-03-08"`).
4. **Decryption:** When the user views their dashboard, the backend sees the data was encrypted with `v:2026-03-08`. It asks the Cloudflare Worker for that specific historical key, decrypts the data in memory, and sends it to the frontend.

## 📝 Cloudflare Worker Example Logic

For contributors looking to understand the edge service, here is a simplified look at the worker's routing logic:

```javascript
// Example Cloudflare Worker Router
export default {
  async fetch(request, env, ctx) {
    const url = new URL(request.url);

    // Authenticate the request from our NestJS Monolith
    if (request.headers.get("X-Internal-Secret") !== env.WORKER_SECRET) {
      return new Response("Unauthorized", { status: 401 });
    }

    // Route: Get Current Key (For encrypting new data)
    if (url.pathname === "/keys/active" && request.method === "GET") {
      const activeKey = await env.KEY_VAULT.get("ACTIVE_KEY");
      return new Response(JSON.stringify({ version: activeKey.version, key: activeKey.material }));
    }

    // Route: Get Historical Key (For decrypting old data)
    if (url.pathname.startsWith("/keys/version/") && request.method === "GET") {
      const version = url.pathname.split("/").pop();
      const historicalKey = await env.KEY_VAULT.get(version);
      return new Response(JSON.stringify({ key: historicalKey }));
    }

    return new Response("Not Found", { status: 404 });
  },

  // Scheduled Cron Trigger for Key Rotation
  async scheduled(event, env, ctx) {
    const newKey = generateSecureKey();
    const newVersion = `v:${Date.now()}`;

    // Save new key and update active pointer
    await env.KEY_VAULT.put(newVersion, newKey);
    await env.KEY_VAULT.put("ACTIVE_KEY", JSON.stringify({ version: newVersion, material: newKey }));
  }
};
```