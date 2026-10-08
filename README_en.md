# Online Fishing Store Project

Project carried out as part of the **Web Application Programming** course at Warsaw University of Technology.

The application is a full-stack system for a fishing store combined with fishing spot reservations at fisheries. The system allows users to browse products, add them to a shopping cart, reserve fishing spots, place orders, and use an administration panel.

## Technologies Used

### Frontend

- **React** – a library used to build the user interface as a Single Page Application (SPA).
- **React Router** – handles navigation between views without reloading the entire page.
- **Tailwind CSS** – styling of the responsive user interface.

### Backend

- **Spring Boot** – the main backend framework of the application.
- **Spring Web / REST API** – communication between the frontend and backend through HTTP endpoints.
- **Spring Data JPA / Hibernate** – handles object-relational mapping and communication with the database.
- **Spring Security** – configuration of access to application resources.

### Database

- **MySQL 8.4** – a relational database storing information about users, products, shopping carts, orders, fisheries, fish, and fishing spots.

### Deployment and Infrastructure

- **Docker** – containerization of the application.
- **Docker Compose v2** – starts the entire environment with a single command.
- **Nginx** – serves the built React frontend and forwards `/api/` requests to the backend.

## Software Requirements

To run the project, the following are required:

- **Docker Engine** or **Docker Desktop**,
- **Docker Compose v2**, available as the `docker compose` command,
- **Git**, if the project is to be downloaded from a repository,
- available ports:
  - `80` – for the web application served by Nginx,
  - `3307` – for local access to the MySQL database from the host.

There is no need to install additional libraries locally because the application runs in Docker containers.

## Installation and Startup Instructions

### 1. Installing Docker

On Linux, Docker Engine should be installed according to the instructions for the distribution being used. If the system requires it, the user should be added to the `docker` group.

On Windows or macOS, Docker Desktop should be installed and started.

### 2. Verifying the Installation

After installation, check the availability of Docker and Docker Compose:

```bash
docker --version
docker compose version
```

### 3. Downloading the Project

The project should be downloaded from the repository or its directory should be copied to the target machine:

```bash
git clone <repository-address>
cd <project-directory-name>
```

If the project has been provided locally, simply navigate to the project's root directory.

### 4. Checking the Directory Structure

The project's root directory should contain, among others, the following files:

- `compose.yaml`,
- `Dockerfile.backend`,
- `Dockerfile.web`.

### 5. Starting the Application

Build and start the application using the following command:

```bash
docker compose up -d --build
```

### 6. Waiting for Services to Start

After startup, wait until:

- the `mysql` container passes its healthcheck,
- the backend starts on port `8080` within the Docker Compose network,
- the `web` container starts listening on port `80`.

### 7. Opening the Application

After successful startup, the application is available in a web browser at:

```text
http://localhost/
```

The MySQL database is accessible from the host at:

```text
localhost:3307
```

Within the Docker Compose network, the backend connects to the database using the address:

```text
mysql:3306
```

## Database Initialization and Reset

During the first startup, the MySQL container executes initialization scripts from the `init-db` directory. Database data is stored in a Docker volume, so subsequent startups preserve the current state of the database.

To recreate the database from scratch, stop the containers and remove the volumes:

```bash
docker compose down -v
docker compose up -d --build
```

## Stopping the Application

To stop the application, execute the following command:

```bash
docker compose down
```
