# Changelog - Migraine Tracker

## February 2026

- **Incidents**: Managed incident types; updated trigger endpoints (Feb 24-25).
- **Predictions**: Implemented complete prediction module & API rules CRUD (Feb 16-20).
- **Health Logs**: Updated sleep data and added water intake metrics (Feb 19).
- **Locations**: Covered location with tests and support location date ranges (Feb 16-18).
- **Weather / Solar**: Added UV Index to hourly forecasts and stabilized weather integrations (Feb 3-8).
- **Frontend**: Implemented management of incident types and added user-specific incident types (Feb 24).
- **Frontend**: Added rules and prediction capabilities (Feb 20).
- **Frontend**: Added tracking functionality for sleep and water health logs across the application (Feb 19).
- **Frontend**: Added new day page layout (Feb 16).
- **Frontend**: Added forecast UvIndex chart (Feb 8).
- **Frontend**: Added medication and forecast capabilities (Feb 5).
- **Frontend**: Implemented edit support for entities (Feb 3).

## January 2026

- **Usage Statistics**: Implemented usage statistics per user (Jan 23).
- **Incidents**: Developed incident statistics service method and endpoints (Jan 17).
- **Security & Fixes**: Secured API documentation page, applied OWASP recommendations, and fixed ESLint issues (Jan 14-22).
- **Testing & Infrastructure**: Drastically optimized CI/CD testing pipelines. Separated environments for tests, updated GitHub Actions workflows, and configured local in-memory DB setups (Jan 10-14).
- **Frontend**: Implemented retention of usage statistics per user (Jan 23).
- **Frontend**: Added incident statistics charts to the report page (Jan 17).
- **Frontend**: Updated the display of error messages (Jan 22).
- **Frontend**: Fixed issues with importing incidents (Jan 15).

## December 2025

- **Weather & Solar Data Expansion**:
  - Integrated Open-Meteo services (Dec 18).
  - Designed an aggregated summary endpoint for location-based weather and solar data (Dec 29).
  - Added fields such as historical geomagnetic data and direct radiation metrics (Dec 6-30).
- **Incidents**: Added notes (optional metadata) and summary fields (Dec 30).
- **Infrastructure**: Introduced robust backend logging (Dec 28) and Cloudflare status/worker implementations (Dec 28).
- **Frontend**: Implemented the ability to add locations and introduced database data upload/backup feature (Dec 30).
- **Frontend**: Added Docker support (Dec 27).
- **Frontend**: Implemented a consolidated health logs form and established dedicated services for managing symptoms, incidents, medications, and triggers (Dec 20).
- **Frontend**: Replaced Open Weather integration (Dec 18).
- **Frontend**: Integrated solar weather data (Dec 17).

## November 2025

- **Solar Modules Setup**: Established foundational solar weather integrations with clients for NOAA and GFZ data (Nov 24-29).
- **User & Security**:
  - Integrated Supabase OAuth2 functionality (Nov 18).
  - Added user Role-Based Access Control (RBAC) (Nov 17).
  - Implemented secure profile retrieval endpoints with payload encryption, including lat/lon data (Nov 19-23).
- **Feature Enhancements**:
  - Iterated comprehensively on Locations, Health Logs, Symptoms, Triggers, and Medications CRUD modules, focusing on test coverage and payload security (Nov 12-16).
- **Frontend**: Integrated solar weather endpoint (Nov 26).
- **Frontend**: Updated Solar Radiation API to use bearer token authentication and removed legacy API key headers (Nov 24).
- **Frontend**: Connected profiles and added birthdate saving (Nov 20).
- **Frontend**: Integrated profile components with API (Nov 19).

## October 2025

- **Data Integrations**: Perfected encoding/decoding implementations for sensitive incident domains (Oct 6).

## September 2025

- **Authentication**: Solidified JWT strategies; symmetric encryption retrieval logic; integration endpoints (Sep 14-16).
- **Core Engineering**: Typecheck enforcement; resolving linting anomalies across newly scoped modules (Sep 7).

## August 2025

- **Initial Authentication & Encryption architecture**: Configured core user authentication flows, token guard services, Auth RBAC structure, and HMAC secure encryption key fetching from workers (Aug 15-30).
- **Foundational Modules Setup**: Scaffolding base schemas and services for Symptoms, Medications, Triggers, and basic Data Mongoose wiring (Jul 29 - Aug 12).
- **Initial Dev Infrastructure**: Git repository creation, Docker configuration with NGIinx load limiters, and establishing the base GitHub e2e and linter pipelines (Jul 25-28).

## July 2025

- **Initial Dev Infrastructure**: Git repository creation, Docker configuration with NGIinx load limiters, and establishing the base GitHub e2e and linter pipelines (Jul 25-28).

## Older Features (Pre-July 2025)

- **2025-06-29** - Separated charts into isolated views.
- **2025-04-30** - Unified various health indicators and added detailed descriptions for indicators.
- **2025-04-19** - Added solar weather indicators.
- **2025-04-13** - Added recommendation page and widget.
- **2025-04-12** - Completed charting components.
- **2025-04-03** - Added Date Information page.
- **2025-07-13** - Updated `uviIndex` naming.
