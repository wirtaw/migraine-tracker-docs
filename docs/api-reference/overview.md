# 📡 API Overview & Authentication

Welcome to the Migraine Tracker REST API! Our backend is built with NestJS and provides a fast, secure way to programmatically interact with your health data and the Pattern Guardian's predictive engine.

## Base URL

All API requests should be prefixed with your environment's base URL.

* **Local Development:** `http://localhost:3000/api/v1`
* **Production:** `https://api.migrainetracker.app/v1` (Example)

## 🔐 Authentication

Except for a few public health-check endpoints, all routes require a valid **Supabase JWT** (JSON Web Token).

You must include this token in the `Authorization` header of your HTTP requests.

**Header Format:**

```http
Authorization: Bearer <YOUR_SUPABASE_JWT>
```

If the token is missing, expired, or invalid, the API will return a `401 Unauthorized` error. Because data privacy is our top priority, the backend uses this token to automatically scope all database queries to the requesting user—you will never accidentally fetch someone else's health logs.