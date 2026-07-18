# Prompt: Create a Spec Sheet and Implementation Plan for HomeOps

You are an expert full-stack software architect, Linux systems engineer, and technical project planner.

I want to build a personal homelab operations dashboard called **HomeOps**.

## Project Overview

HomeOps is a self-hosted LAN-first dashboard for tracking, monitoring, and eventually managing services running across my homelab. It should help me keep track of services running on Raspberry Pis, Ubuntu machines, Docker containers, local web apps, FastAPI apps, Jellyfin, Pi-hole, Vaultwarden, Caddy, Simple-Server, and similar services.

This project does **not** need to expose anything to the public internet at first. It is primarily meant for local network use, but the design should not prevent future remote access through Tailscale, VPN, or a reverse proxy.

The goal is to create a practical portfolio-quality project that combines:

* Linux administration
* Networking
* Docker
* FastAPI
* React/TypeScript
* SQLite or PostgreSQL
* Service health monitoring
* WebSockets
* SSH-based actions
* Docker container management
* AI-assisted homelab operations in a later phase

## Core Problem

As a homelab grows, it becomes hard to remember:

* Which services are running
* Which machine hosts each service
* Which port each service uses
* Which services are Docker containers
* Which ones are offline
* Which ones have web dashboards
* Which ones need attention
* Where logs live
* Which machines are reachable

HomeOps should solve this by becoming a single dashboard for homelab visibility and lightweight operations.

## Initial MVP

Design an MVP that includes:

1. A service catalog

   * Service name
   * Description
   * Hostname
   * IP address
   * Port
   * Protocol
   * URL
   * Category
   * Tags
   * Service type: Docker, systemd, web app, database, network device, other
   * Notes
   * Enabled/disabled status

2. Health checks

   * HTTP status check
   * TCP port check
   * Ping check if appropriate
   * Last checked timestamp
   * Current status: online, offline, degraded, unknown
   * Response time

3. Dashboard UI

   * Service cards
   * Status badges
   * Search
   * Filtering by host, category, status, and service type
   * Click to open service URL
   * Simple responsive layout

4. Backend API

   * CRUD endpoints for services
   * Endpoint to run health checks
   * Endpoint to get dashboard summary
   * Endpoint to get service details
   * Optional background scheduler for periodic health checks

5. Database

   * Use SQLite for the MVP
   * Design schema so PostgreSQL could be used later
   * Include migrations if appropriate

## Suggested Tech Stack

Use this stack unless there is a strong reason to suggest otherwise:

* Backend: FastAPI
* Frontend: React + TypeScript
* Styling: Tailwind CSS
* Database: SQLite
* ORM: SQLModel or SQLAlchemy
* Runtime: Python 3.12+
* Frontend build tool: Vite
* Containerization: Docker Compose
* Reverse proxy: Caddy later, not required for MVP
* Realtime updates: WebSockets later
* Metrics: psutil later
* Docker integration: Docker SDK later

## Important Design Requirements

The project should be built incrementally.

Do not overbuild the MVP.

Separate the system into clean modules:

* API routes
* database models
* service repository/data layer
* health check engine
* background jobs
* frontend components
* frontend API client
* configuration management

Prefer readable, maintainable code over clever abstractions.

The MVP should be useful even before Docker, SSH, AI, or advanced metrics are added.

## Security Requirements

Because this app could eventually control services, design with security in mind from the beginning.

Include recommendations for:

* LAN-only deployment
* Optional authentication
* Avoiding arbitrary command execution
* Safely storing host credentials later
* SSH key handling later
* Restricting dangerous actions
* Audit logging for future administrative actions
* Separating read-only monitoring from write actions

For the MVP, administrative actions can be excluded. Focus first on visibility and health checks.

## Future Feature Roadmap

Create a roadmap with phases.

Potential future features:

### Phase 2: Better Monitoring

* Periodic background health checks
* Uptime history
* Response time history
* Basic charts
* Service grouping by machine
* Host status pages

### Phase 3: Docker Integration

* Detect local Docker containers
* Show container status
* Show image name
* Show exposed ports
* Start/stop/restart containers
* View recent logs

### Phase 4: SSH-Based Remote Actions

* Add host records
* Connect to Raspberry Pis or Ubuntu machines over SSH
* Run predefined safe commands only
* Restart systemd services
* Check disk usage
* Check memory usage
* Check uptime
* Pull basic system info

### Phase 5: Logs and Metrics

* View recent logs
* Search logs
* Show CPU, RAM, disk, and network usage
* WebSocket live updates
* Alerts or notifications

### Phase 6: AI Assistant

Add an AI assistant that can answer questions like:

* "Which services are down?"
* "What changed recently?"
* "Restart Jellyfin."
* "Show me services running on the Desktop Pi."
* "Which services are using port 8080?"
* "Why might this service be unreachable?"

The AI assistant should be designed safely. It should start as read-only and later support approved actions through a controlled command system.

## Deliverables I Want From You

Create a detailed project planning document that includes:

1. Executive summary
2. Problem statement
3. Goals and non-goals
4. Target users
5. MVP scope
6. Future roadmap
7. Recommended tech stack
8. System architecture
9. Backend architecture
10. Frontend architecture
11. Database schema proposal
12. API endpoint list
13. Health check design
14. Background job design
15. Security considerations
16. Deployment plan
17. Docker Compose plan
18. Suggested folder structure
19. Development milestones
20. Testing strategy
21. Example service records
22. Risks and tradeoffs
23. Portfolio/resume talking points
24. README outline
25. First 10 implementation tasks

## Output Format

Please format the response as a clean technical specification using Markdown.

Use headings, tables, diagrams where helpful, and concrete examples.

For architecture diagrams, use Mermaid syntax.

Prioritize practical implementation guidance over vague theory.

Assume I am comfortable with Linux, GitHub, Raspberry Pi, Docker basics, Python, FastAPI, React, and terminal workflows, but I want a clear build plan that avoids scope creep.

The final result should be something I can save as:

`HOMEOPS_SPEC.md`

and use as the blueprint for building the project.

