# 🚀 Changelog & Release Notes

Welcome to the Migraine Tracker updates page! We are constantly working behind the scenes to make your tracking experience smoother, your data safer, and our predictive engine smarter. 

Here is a log of all the new features, environmental integrations, and improvements we've made.

---

## 🌟 Version 1.2.0: The Security & Insights Update
*Release Date: March 2026*

This release focused heavily on protecting your sensitive data and giving you better tools to understand your long-term health trends.

**🔐 Security & Architecture**
* **New:** Introduced an edge-based **Cloudflare Worker** to handle daily symmetric key rotation. Your encrypted health payloads are now secured with dynamically changing keys!
* **Improved:** Upgraded the NestJS backend `RbacGuard` to strictly isolate user data streams, preventing any cross-contamination of predictive rules.

**📊 Dashboard & Reporting**
* **New:** Added the **30-Day Trend Report** (`/reports`). You can now view visual charts mapping your incident frequency and pain severity over the last month.
* **New:** Introduced the **Biorhythm Chart widget** on the daily dashboard to track physical, emotional, and intellectual cycles.
* **Improved:** The Data Management portal now allows for one-click **Database Backups** and full user data resets.

---

## ☀️ Version 1.1.0: The Solar Sensitivity Update
*Release Date: February 2026*

We heard from many users that atmospheric pressure wasn't their only environmental trigger. In this update, we taught the Pattern Guardian to look at the stars!

**🌍 Environmental Integrations**
* **New:** Integrated with the **GFZ German Research Centre** to track the Planetary K-Index (Geomagnetic Storms).
* **New:** Integrated with **NOAA** to track F10.7 Solar Flux and Sunspot activity.
* **New:** Integrated with **TEMIS** to monitor daily Ozone thickness and UV Index spikes.

**🧠 Predictive Engine**
* **Improved:** The *Pattern Guardian* now cross-references your migraine logs with all newly added solar metrics to generate highly specific "Solar Sensitivity" risk rules.
* **New:** Added the **Solar & Geo-Magnetic Widget** to the main dashboard so you can view today's space weather at a glance.

---

## 🚀 Version 1.0.0: Initial Launch
*Release Date: January 2026*

Welcome to Migraine Tracker! This initial release brings the foundational tools you need to find your triggers and reclaim your days.

**✨ Core Features**
* **Dashboard:** A serene, dark-mode-first daily command center built with React.
* **Health Logging:** Quick-add buttons for sleep quality, hydration, mood, and daily preventative medications.
* **Incident Tracking:** Detailed logs for migraine severity, duration, custom symptoms, and rescue medications.
* **Weather Integration:** Automatic local weather and barometric pressure tracking via Open-Meteo.
* **The Pattern Guardian:** Our proprietary backend engine that silently looks for correlations between your pain and the weather.
* **One-Click Auth:** Frictionless sign-up and login via Google and GitHub.

---

*Did you spot a bug or have a feature request? Let us know on our [GitHub Issues](https://github.com/wirtaw/migrane-tracker-dashboard/issues) page!*