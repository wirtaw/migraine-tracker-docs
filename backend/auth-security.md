# 🛡️ Auth & Security Overview

Protecting user health data is the foundational pillar of the Migraine Tracker architecture. We employ a multi-layered security model that separates authentication from data encryption.

## 1. Authentication (Supabase)

We utilize **Supabase Auth** to handle our identity access management.

* The React frontend authenticates directly with Supabase via OAuth (Google/GitHub) or Magic Links.
* The frontend receives a JWT (JSON Web Token), which is then passed as a Bearer token to our NestJS Monolith.
* The backend `JwtService` verifies this token on every protected request.

## 2. Role-Based Access Control (RBAC)

Not all users have the same permissions. We use a custom `RbacGuard` (`src/auth/guard/rbac.guard.ts`) in NestJS to restrict endpoint access.

* **Standard Users:** Can only read, write, and delete their *own* isolated data payloads.
* **Admins:** Have access to anonymized global telemetry for system health monitoring.

## 3. Data Encryption at Rest

While MongoDB encrypts data at the disk level, we take it a step further. Any sensitive medical telemetry (like specific symptom arrays or medication logs) is encrypted *at the application level* before it is ever written to the database.

* We use **AES-256-CBC** encryption via our `EncryptionService`.
* The symmetric keys used for this encryption are dynamically provided and rotated by an external edge service, completely decoupled from the main database.

*(Read more about this in the [Key Management](key-management.md) section.)**