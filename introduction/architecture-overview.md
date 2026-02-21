# System Architecture Overview

Migraine Tracker is built on a modern, decoupled client-server architecture. This separation of concerns allows us to maintain a highly secure backend for processing sensitive health data while delivering a fast, responsive user interface.

## 🏗 The High-Level Stack

### 1. The Client: React Dashboard (`migrane-tracker-dashboard`)
A Single Page Application (SPA) designed with serenity and accessibility in mind.
* **Core Framework:** React 18 + Vite
* **Styling:** Tailwind CSS (with full Dark Mode support for light-sensitive users)
* **State Management:** React Context API (`AuthContext`, `ProfileDataContext`)
* **Hosting:** Configured via Nginx and Docker for seamless deployment.

### 2. The Server: NestJS Monolith (`migraine-tracker-monolith`)
A robust, modular API responsible for data processing, external API orchestration, and prediction algorithms.
* **Core Framework:** NestJS (TypeScript)
* **Database:** MongoDB (via Mongoose)
* **Authentication & AuthZ:** Supabase Auth with custom Role-Based Access Control (RBAC) guards.
* **Security:** AES-256 encryption at rest for sensitive health logs via our custom `EncryptionService`.

## 🔄 How the Data Flows

The true power of Migraine Tracker lies in how it merges personal data with the physical world. Here is a simplified look at the system's data flow:

1. **Environmental Ingestion:**
   The backend continuously polls external APIs based on the user's location.
   * *Weather:* [Open-Meteo](https://open-meteo.com/) (Temperature, Barometric Pressure)
   * *Solar/Geomagnetic:* [NOAA](https://www.noaa.gov/), GFZ, and TEMIS (F10.7 Solar Flux, K-Index, UV Index, Ozone)

2. **User Telemetry:**
   Users submit data via the frontend dashboard. This includes daily `Health Logs` (sleep, mood) and specific `Incidents` (migraines, severity, symptoms).

3. **The Prediction Engine:**
   When an incident is logged, the `Pattern Guardian` service looks at the environmental data from that specific day. Over time, it calculates risk correlations (e.g., "User A has an 80% chance of a migraine when Barometric Pressure drops rapidly and Solar Flux is high") and generates `Prediction Rules`.

4. **Dashboard Visualization:**
   The frontend fetches this aggregated data and renders it through specialized components (like the `SolarFluxIndicator` or `BiorhythmChart`), giving the user a unified, easy-to-read daily forecast.