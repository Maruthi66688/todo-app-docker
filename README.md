# Multi-Container Todo App

A full-stack Todo application built with React, Node.js/Express, and PostgreSQL — fully containerized using Docker and orchestrated with Docker Compose.

## Architecture

┌─────────────┐ ┌─────────────┐ ┌──────────────┐
│ Frontend │────▶│ Backend │────▶│ Database │
│ React+Nginx │ │Node/Express │ │ PostgreSQL │
│ Port 3000 │◀────│ Port 5000 │◀────│ Port 5432 │
└─────────────┘ └─────────────┘ └──────────────┘
All connected via a custom Docker bridge network

Three independent containers communicate over a custom Docker network. The frontend never talks to the database directly — all requests go through the backend API.

## Tech Stack

- **Frontend:** React (Vite), served via Nginx in production
- **Backend:** Node.js, Express
- **Database:** PostgreSQL
- **Containerization:** Docker, Docker Compose

## Features

- Create, read, update, and delete todos
- Mark todos as complete/incomplete
- Filter by All / Active / Completed
- Data persists across container restarts via a Docker volume

## Docker Concepts Demonstrated

- Multi-stage Docker builds (React build stage → Nginx serve stage)
- Custom bridge networking (containers resolve each other by service name, not IP)
- Named volumes for database persistence
- Environment variable injection via Docker Compose
- Service dependency ordering (`depends_on`)
- Auto-initialization of database schema on first run (`init.sql`)

## Getting Started

### Prerequisites
- Docker Desktop installed and running

### Run the app

```bash
git clone <your-repo-url>
cd todo-app
docker-compose up --build
```

Then open: http://localhost:3000

### Stop the app

```bash
docker-compose down
```

## Project Structure

todo-app/
├── backend/
│ ├── server.js
│ ├── db.js
│ ├── init.sql
│ ├── Dockerfile
│ └── .dockerignore
├── frontend/
│ ├── src/
│ ├── Dockerfile
│ └── .dockerignore
├── docker-compose.yml
└── README.md

## What This Project Demonstrates

This project was built to learn Docker fundamentals hands-on — going from zero Docker experience to a working multi-container application with proper networking, persistence, and orchestration, following an incremental build process (local development first, then containerization service by service, then full orchestration).
