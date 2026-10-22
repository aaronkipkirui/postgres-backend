# Postgres Backend API

A robust, containerized **Node.js** and **Express** REST API designed for high performance, structural maintainability, and seamless data management. This backend serves as a standardized boilerplate or standalone service featuring deep **PostgreSQL** integration, robust schema validation, and strict error handling architecture.

## Key Features

*   **RESTful CRUD Operations:** Fully implemented endpoints for reliable data management.
*   **PostgreSQL Integration:** Native connection pooling optimized for relational data structures.
*   **Joi Schema Validation:** Strict request body and parameter validation at the routing layer to ensure data integrity.
*   **Centralized Error Handling:** Global middleware to catch, format, and log operational and programmatic errors consistently.
*   **Dockerized Environment:** Pre-configured Docker settings for quick, environment-isolated local deployment or production staging.

---

## Tech Stack

*   **Runtime:** Node.js (v18+ recommended)
*   **Framework:** Express.js
*   **Database:** PostgreSQL
*   **Validation:** Joi
*   **Containerization:** Docker & Docker Compose

---

## Prerequisites

Before setting up the project locally, ensure you have the following tools installed:

*   [Node.js](https://nodejs.org) (with `npm`)
*   [Docker](https://docker.com) & [Docker Compose](https://docker.com)
*   [PostgreSQL](https://postgresql.org) (if running bare-metal without Docker)

---

## Environment Variables

Create a `.env` file in the root directory of your project and configure the following variables based on your setup:

```env
# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
DB_HOST=localhost
DB_USER=postgres
DB_PASSWORD=your_secure_password
DB_NAME=postgres_backend_db
DB_PORT=5432
```

> **Note:** If you are running the service via Docker Compose, set `DB_HOST=db` (or matching your database container service name).

---

## Local Installation & Setup

### Option 1: Running with Docker (Recommended)

The fastest way to spin up the application along with an isolated PostgreSQL database instance:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/aaronkipkirui/postgres-backend
   cd postgres-backend
   ```

2. **Spin up the containers:**
   ```bash
   docker-compose up --build
   ```
   This command automatically builds the Node.js application container, pulls the official PostgreSQL image, links them within a shared network, and exposes the configured API port.

### Option 2: Running Locally (Bare Metal)

If you prefer to run the Node server directly on your host machine:

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Configure your database:**
   Ensure a local PostgreSQL instance is running, the database specified in your `.env` exists, and your credentials match perfectly.

3. **Start the development server:**
   ```bash
   npm run dev
   ```

4. **Start for production:**
   ```bash
   npm start
   ```

---

## Project Structure

```text
postgres-backend/
├── src/
│   ├── config/          # Database and environment configurations
│   ├── controllers/     # Route handlers & business logic orchestration
│   ├── middleware/      # Joi validators, error handlers, and auth checks
│   ├── models/          # Database schemas, queries, or ORM mappings
│   ├── routes/          # Express API route declarations
│   └── index.js           # Express application initialization & entry point
├── .gitignore
├── docker-compose.yml
├── Dockerfile
├── package.json
└── README.md
```

---

## Request Validation & Error Handling

*   **Validation:** Incoming payloads are intercepted by `Joi` validation schemas before reaching controllers. Any invalid data payload triggers an immediate, descriptive `400 Bad Request` response highlighting the specific formatting error.
*   **Centralized Errors:** All async and synchronous controller errors are safely passed to a centralized error-handling middleware. This prevents server crashes, hides internal database stack traces from the client in production, and standardizes the outgoing JSON error response format.

---
