# 🌍 Environmental Integrations

To accurately predict migraines, our system needs to know what is happening in the atmosphere and magnetosphere. The backend does the heavy lifting of continuously fetching and standardizing this data from various scientific bodies.

These integrations are housed within the `src/weather` and `src/solar` modules.

## 🌤️ Weather Data (Open-Meteo)

We utilize the **[Open-Meteo API](https://open-meteo.com/)** for all terrestrial weather data. It is fast, requires no API keys for open-source projects, and provides high-resolution local data.

**Key Metrics Fetched:**

* Temperature & Humidity
* Barometric Pressure (Crucial for predicting pressure-drop triggers)
* Cloud Cover & Precipitation

**Client Location:** `src/weather/open-meteo.client.ts`

## ☀️ Solar & Space Weather

Many chronic migraine sufferers report sensitivity to invisible shifts in solar radiation and geomagnetic storms. We pull data from three distinct scientific agencies to track this:

### 1. NOAA (Space Weather Prediction Center)

* **What we fetch:** F10.7 Solar Flux and Sunspot Numbers.
* **Why:** High solar activity can influence human circadian rhythms and nervous system sensitivity.
* **Client Location:** `src/solar/noaa.client.ts`

### 2. GFZ (German Research Centre for Geosciences)

* **What we fetch:** The Planetary K-Index (Kp-Index).
* **Why:** The K-index quantifies disturbances in the Earth's magnetic field. Values of 5 or higher indicate a geomagnetic storm, a known environmental stressor.
* **Client Location:** `src/solar/gfz.client.ts`

### 3. TEMIS (Tropospheric Emission Monitoring)

* **What we fetch:** Ozone layer thickness and advanced UV Index data.
* **Why:** Sudden spikes in UV intensity or drops in ozone protection correlate with light-sensitivity triggers (Photophobia).
* **Client Location:** `src/solar/temis.client.ts`

## 🔄 Caching Strategy

To respect the rate limits of these scientific APIs and keep our dashboard blazing fast, the backend heavily caches this environmental data in memory and MongoDB for specific geographic bounding boxes. If two users are in the same city, we only query NOAA once per cycle!