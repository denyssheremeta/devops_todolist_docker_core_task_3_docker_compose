# INSTRUCTION.md

This document provides detailed instructions on how to build, run, and stop Docker containers using `docker-compose` for the **todolist** application with a MySQL database.

---

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- Docker Engine (version 20.10 or later)
- Docker Compose (version 1.27.0 or later)
- Git (optional, if you need to clone the repository)

## 1. Build Docker Images

From the project root, run:

```bash
docker-compose build
```

This command will:

1. Build the **todoapp** service image based on `Dockerfile`.
2. (If applicable) Build the **mysql** service image or pull from Docker Hub.

## 4. Start the Containers

To start the services in detached mode (in the background), run:

```bash
docker-compose up -d
```

- **-d** flag starts the containers in the background.
- This will start:

  - A MySQL container named `mysql` on port 3306.
  - A Django application container named `todoapp` on port 8080.

## 5. Verify Running Containers

To see the status of all running containers:

```bash
docker-compose ps
```

You should see entries for:

- `mysql` (Up, port 3306)
- `todoapp` (Up, port 8080)

## 6. View Logs

To follow the logs of all services:

```bash
docker-compose logs -f
```

To view logs for a specific service, e.g., `todoapp`:

```bash
docker-compose logs -f todoapp
```

## 7. Stopping Containers

### Graceful Shutdown

To stop all running containers without removing them:

```bash
docker-compose stop
```

This will send a SIGTERM signal to each container and then SIGKILL if they do not exit within the default timeout (10 seconds).

### Stop and Remove Containers, Networks, and Volumes

To stop and remove all containers, networks, and named volumes defined in the Compose file:

```bash
docker-compose down
```

- By default, `down` will remove:

  - Containers
  - Networks
  - Default and user-defined networks

#### Preserve Volumes

If you want to remove containers and networks but keep the named volumes (e.g., database data), add the `--volumes` flag:

```bash
docker-compose down --volumes
```

## 8. Additional Useful Commands

- **Rebuild and restart:**

  ```bash
  docker-compose up -d --build
  ```

  Rebuilds images before starting containers.

- **Execute a command inside a running container:**

  ```bash
  docker-compose exec todoapp bash
  ```

  Opens an interactive shell in the `todoapp` container.

- **Remove unused images and volumes:**

  ```bash
  docker system prune --volumes
  ```

  Cleans up unused Docker data.

---

You now have all the commands needed to manage your Docker-based development environment for the Todolist project. Happy coding!
