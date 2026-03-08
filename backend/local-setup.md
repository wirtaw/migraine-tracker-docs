# 💻 Local Setup (Docker & NestJS)

Welcome to the backend engine of Migraine Tracker! We have designed the local development environment to be as frictionless as possible. You can run the entire stack using Docker, or run the NestJS app locally on your machine for easier debugging.

## 🛠️ Prerequisites

Before you start, ensure you have the following installed:

* [Docker](https://www.docker.com/) & Docker Compose
* [Node.js](https://nodejs.org/) (v18 or higher)
* [pnpm](https://pnpm.io/) (Our package manager of choice)

## 📦 Step 1: Clone and Configure

First, clone the `migraine-tracker-monolith` repository and install the dependencies.

```bash
git clone https://github.com/your-org/migraine-tracker-monolith.git
cd migraine-tracker-monolith
pnpm install
```

Next, set up your environment variables. We have provided an example file for you:

```bash
cp env/.env.example .env
```

Note: For local development, the default values in .env.example will work perfectly with the local Docker setup.

## 🐳 Step 2: Spin up the Infrastructure

To run the database (MongoDB) and any other required infrastructure locally, we use Docker Compose.

```bash
docker-compose -f docker-compose.local.yml up -d
```

This will spin up an isolated MongoDB instance on port `27017` mapped to your localhost.

## 🚀 Step 3: Start the NestJS Monolith

With your database running, you can now start the NestJS application in watch mode. This means the server will automatically restart whenever you save a file.

```bash
pnpm run start:dev
```

If everything is configured correctly, you should see the NestJS startup logs, finishing with:
`[NestApplication] Nest application successfully started`

The API is now listening on `http://localhost:3000`! You are ready to start building.