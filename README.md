# BuildBase Dynamic Flow Engine

<div align="center">

![Vue.js](https://img.shields.io/badge/Vue.js-3.x-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Java](https://img.shields.io/badge/Java-JDK_21_LTS-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)

*A flexible, enterprise-grade workflow automation engine built for BuildBase (Strouwi BV)*

</div>

---

> 📌 **Portfolio Demo Note**
> 
> I *(Zakaria Shahruri)* have adapted this repository from its original BuildBase enterprise configuration to use a free MongoDB Atlas cloud cluster. This ensures the engine can be easily run and demonstrated as a standalone portfolio piece, without requiring access to the original internal company infrastructure.

---

## Overview

The **BuildBase Dynamic Flow Engine** is a configurable system designed to automate and track business processes — such as employee onboarding, absence approvals, and custom internal workflows — for BuildBase (Strouwi BV).

The engine features visual flow mapping, real-time state tracking, and WebSocket-powered notifications, and was built to integrate seamlessly with existing enterprise services. Its architecture is intentionally extendable, making it straightforward to add new process types without restructuring the core system.

---

## Features

- **Visual Flow Mapping** — Intuitive, diagram-based representation of each workflow's steps and transitions
- **Real-Time Notifications** — Live process updates pushed to clients via WebSockets, no polling required
- **State Tracking** — Full visibility into where each process instance is at any point in time
- **Configurable Processes** — New workflow types (onboarding, approvals, etc.) can be defined and deployed without core changes
- **Enterprise Integration** — Designed from the ground up to plug into existing internal services and infrastructure
- **OKD Deployment** — Production-ready, containerised deployment on an OpenShift-based OKD environment

---

## Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | Vue.js, TypeScript, Tailwind CSS |
| **Backend** | Java (JDK 21 LTS), Spring Boot, WebSockets, Maven |
| **Database** | MongoDB (Atlas) |
| **Deployment** | OKD Environment |
| **Architecture** | Monorepo (managed via Concurrently) |

---

## Repository Structure

This project is structured as a monorepo to keep the frontend and backend tightly synchronized:

```
buildbase-dynamic-flow-engine/
├── frontend/       # Vue.js Single Page Application — UI & state management
├── backend/        # Spring Boot REST API & WebSocket server
├── package.json    # Root task runner — starts both servers simultaneously
└── .gitignore      # Global ignore rules
```

---

## Quick Start (Docker) — Recommended

If you have [Docker](https://www.docker.com/products/docker-desktop/) installed, you can run the entire stack with a single command — no Node, Java, or Maven setup required.

```bash
# Clone the repository
git clone https://github.com/<your-username>/buildbase-dynamic-flow-engine.git
cd buildbase-dynamic-flow-engine

# Configure your environment variables (see Step 1 below)

# Build and start all services
docker-compose up --build
```

> **Spring Boot API** → `http://localhost:8080`  
> **Vue.js dev server** → `http://localhost:5173`

---

## Quick Start (Manual Development)

### Prerequisites

Ensure the following are installed before running the project locally:

- [Node.js & npm](https://nodejs.org/)
- [Java JDK 21 LTS](https://adoptium.net/)
- [Maven](https://maven.apache.org/)

---

### Step 1 — Environment Configuration

Before starting, configure environment variables for both services.

**Backend** — create `/backend/.env`:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/?retryWrites=true&w=majority
MONGODB_DATABASE=buildbase_flow_db
SPRING_PROFILES_ACTIVE=dev
```

**Frontend** — create `/frontend/.env`:

```env
VITE_API_BASE_URL=http://localhost:8080
```

---

### Step 2 — Installation & Running

From the **root directory** of the project, run:

```bash
# Install the root task runner
npm install

# Install frontend dependencies
npm install --prefix frontend

# Start the full-stack application concurrently
npm run dev
```

> **Spring Boot API** → `http://localhost:8080`  
> **Vue.js dev server** → `http://localhost:5173`

---

## My Contributions

This project was a significant milestone in my growth as a Full-Stack Developer. Working in a real Scrum environment pushed me to improve not just technically, but professionally — learning to communicate across the stack, manage complex Git histories, and deliver iteratively.

- **Agile/Scrum Integration** — Actively participated in sprint planning, code reviews, and continuous improvement cycles within a structured Scrum team.
- **Full-Stack Development** — Gained hands-on experience bridging the Vue.js frontend with the Spring Boot and MongoDB backend — learning to think across the full request lifecycle.
- **Advanced Git Workflows** — Managed complex branching strategies, pull requests, and led the architectural restructuring of the project into a unified monorepo.

---

## The Team — GlacKIT

Developed in a Scrum-based academic workplace environment by a team of 7 students, under the guidance of:

- **Kristien Melaerts** — Academic Supervisor
- **Tom Peeters** — BuildBase (Company Supervisor)

| Role | Members |
|---|---|
| **Seniors (Mentors / Coordinators)** | Adam Benkhazzi, Samip Shrestha, Anette Hardy |
| **Juniors** | Zakaria Shahruri, Angelo Mouawad, Laïs A., Moad Khaouili |