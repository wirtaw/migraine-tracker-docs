# 🧠 State Management (Context API)

To keep the Migraine Tracker lightweight and avoid unnecessary third-party dependencies, we rely on the native **React Context API** to handle our global state.

All of our contexts are cleanly separated by their domain logic and can be found in the `src/context/` directory.

## 🔐 AuthContext

**File:** `src/context/AuthContext.tsx`

This context wraps the entire application and is responsible for managing the user's session via Supabase.

* It listens for auth state changes (login, logout, token refresh).
* It provides the current `user` object and `session` token to the rest of the app, allowing components like the `ProtectedRoute` to restrict access to authenticated users only.

## 🧬 ProfileDataContext

**File:** `src/context/ProfileDataContext.tsx`

This is the heavy lifter of the dashboard! Instead of prop-drilling complex health data, this context holds the user's active personalized state.

* It stores the user's custom `Triggers`, `Symptoms`, and `Medications`.
* It fetches and caches the daily `HealthLogs` and recent `Incidents`.
* By keeping this in context, widgets across the dashboard (like the Quick Add buttons or the Incident Report charts) can instantly access and update health data without making redundant API calls.

## 🔔 NotificationContext

**File:** `src/context/NotificationContext.tsx`

A simple, global context used to fire off toast notifications. Whether a user successfully logs an incident or encounters a network error, any component can consume this context to trigger a friendly alert on the screen.