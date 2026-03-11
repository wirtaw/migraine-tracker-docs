# 💻 Local Setup (React & Vite)

Welcome to the **Migraine Tracker Dashboard** repository! This is the user-facing side of our ecosystem, built for speed and accessibility. We use React 18 powered by Vite for lightning-fast Hot Module Replacement (HMR) during development.

Here is how to get the dashboard running on your local machine.

## 🛠️ Prerequisites

Make sure you have the following installed before you begin:

* [Node.js](https://nodejs.org/) (v18 or higher)
* [pnpm](https://pnpm.io/) (We use pnpm strictly for workspace and package management)

## 📦 Step 1: Clone and Install

First, clone the frontend repository and install the dependencies.

```bash
git clone https://github.com/your-org/migraine-tracker-dashboard.git
cd migraine-tracker-dashboard
pnpm install
```

## 🔐 Step 2: Environment Variables

The dashboard needs to know how to talk to your backend and Supabase. We have provided an example environment file.

- Copy the example file to create your local environment setup:

```bash
cp env.example .env
```

- Open the .env file and fill in your Supabase URL, Supabase Anon Key, and the local URL for your NestJS backend (usually `http://localhost:3000`).

## 🚀 Step 3: Run the Development Server

Once your dependencies are installed and your .env is configured, start the Vite development server!

```bash
pnpm run dev
```

You should see a message indicating the server is running (usually on `http://localhost:5173`). Open that URL in your browser, and you are ready to start building!

## Step 4: Open-Source Constraints & Customization

This repository includes promotional headers and usage limits intended for the Migraine Pulse ecosystem.

### How to Remove Promotion
To remove the Migraine Pulse banner:
1. Open `src/context/NotificationContext.tsx`.
2. Delete the `promoNotification` constant and the conditional rendering block inside the `NotificationProvider` return statement.

### Adjusting or Removing API/Database Limits
To lift limits on DB entries and API requests (OpenWeather, Termis, NOAA):
1. Open `src/services/api-utils.ts`.
2. Find the `checkUsageLimit` function.
3. Change the logic to `return true;` immediately at the start of the function.

Or `checkUsageLimit` usage from services and from `src/services/api-utils.ts`.