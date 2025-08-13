# Docker

## Preset
- Created by Solomon Hykes in 2013, open-sourced by Docker Inc.
- Containerization platform for packaging applications and dependencies
- Official docs: [docs.docker.com](https://docs.docker.com)

## Table of Contents

- [Core Concepts](#core-concepts)
- [Docker Architecture](#docker-architecture)
- [Images vs Containers](#images-vs-containers)
- [Dockerfile](#dockerfile)
- [Docker Commands](#docker-commands)
- [Container Lifecycle](#container-lifecycle)
- [Networking](#networking)
- [Volumes & Storage](#volumes--storage)
- [Docker Compose](#docker-compose)
- [Docker Swarm](#docker-swarm)
- [Security](#security)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Interview Questions](#interview-questions)

## Core Concepts

| Concept | Description | Example |
|---------|-------------|---------|
| **Container** | Lightweight, portable package containing application + dependencies | Running instance of an image |
| **Image** | Read-only template used to create containers | `ubuntu:20.04`, `nginx:latest` |
| **Dockerfile** | Text file with instructions to build an image | `FROM ubuntu` → `RUN apt update` |
| **Registry** | Storage and distribution system for Docker images | Docker Hub, AWS ECR, Google GCR |
| **Volume** | Persistent data storage mechanism | Database data, log files |
| **Network** | Communication layer between containers | Bridge, host, overlay networks |

### Containerization vs Virtualization

| Aspect | Containerization | Virtualization |
|--------|------------------|----------------|
| **Resource Usage** | Lightweight, shares host OS kernel | Heavy, each VM has full OS |
| **Startup Time** | Seconds | Minutes |
| **Isolation** | Process-level isolation | Hardware-level isolation |
| **Performance** | Near-native performance | Performance overhead |
| **Use Case** | Microservices, CI/CD, scaling | Legacy apps, different OS requirements |

## Docker Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Docker Client                            │
│  (docker CLI commands: run, build, pull, push, etc.)        │
└─────────────────────┬───────────────────────────────────────┘
                      │ REST API / Unix Socket
┌─────────────────────▼───────────────────────────────────────┐
│                 Docker Daemon (dockerd)                     │
│  • Manages containers, images, networks, volumes            │
│  • Listens for Docker API requests                          │
│  • Communicates with other daemons                          │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                 Docker Registry                             │
│  • Stores and distributes Docker images                     │
│  • Docker Hub (public), Private registries                  │
└─────────────────────────────────────────────────────────────┘
```

### Key Components

| Component | Purpose | Location |
|-----------|---------|----------|
| **Docker Client** | User interface, sends commands to daemon | Local machine |
| **Docker Daemon** | Manages Docker objects (containers, images, networks) | Docker host |
| **Docker Registry** | Stores and distributes images | Remote servers |
| **Docker Host** | Machine running Docker daemon | Physical/virtual server |

## Images vs Containers

| Aspect | Image | Container |
|--------|-------|-----------|
| **Nature** | Static, read-only template | Dynamic, running instance |
| **Mutability** | Immutable | Mutable (can be modified) |
| **Storage** | Stored in registry/local cache | Exists in memory/disk while running |
| **Lifecycle** | Built once, used multiple times | Created, started, stopped, destroyed |
| **Size** | Fixed size | Variable (depends on runtime changes) |

```bash
# Image operations
docker images                    # List images
docker pull ubuntu:20.04        # Download image
docker build -t myapp:v1 .      # Build image from Dockerfile
docker rmi image_id              # Remove image

# Container operations  
docker ps                       # List running containers
docker ps -a                    # List all containers
docker run ubuntu:20.04         # Create and start container
docker stop container_id        # Stop container
docker rm container_id          # Remove container
```

## Dockerfile

### Essential Instructions

| Instruction | Purpose | Example |
|-------------|---------|---------|
| `FROM` | Base image | `FROM ubuntu:20.04` |
| `RUN` | Execute commands during build | `RUN apt-get update && apt-get install -y python3` |
| `COPY` | Copy files from host to image | `COPY app.py /app/` |
| `ADD` | Copy + extract archives/URLs | `ADD archive.tar.gz /app/` |
| `WORKDIR` | Set working directory | `WORKDIR /app` |
| `ENV` | Set environment variables | `ENV NODE_ENV=production` |
| `ARG` | Build-time variables | `ARG VERSION=1.0` |
| `EXPOSE` | Document port usage | `EXPOSE 8080` |
| `CMD` | Default command (can be overridden) | `CMD ["python3", "app.py"]` |
| `ENTRYPOINT` | Fixed command (always runs) | `ENTRYPOINT ["python3", "app.py"]` |

### Key Differences

| Comparison | RUN | CMD | ENTRYPOINT |
|------------|-----|-----|------------|
| **When executed** | Build time | Runtime | Runtime |
| **Purpose** | Install packages, setup | Default command | Fixed entry point |
| **Override** | Cannot override | Can override | Can override with --entrypoint |
| **Multiple allowed** | Yes | Only last one used | Only last one used |

```dockerfile
# Multi-stage build example
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:16-alpine AS runtime
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
USER node
CMD ["npm", "start"]
```

### COPY vs ADD

| Feature | COPY | ADD |
|---------|------|-----|
| **Basic copying** | ✅ | ✅ |
| **URL support** | ❌ | ✅ |
| **Auto-extract archives** | ❌ | ✅ |
| **Security** | More secure | Less secure |
| **Best practice** | Preferred for simple copying | Use only when extra features needed |

## Docker Commands

### Container Management

```bash
# Running containers
docker run -d --name myapp -p 8080:80 nginx          # Run detached with port mapping
docker run -it ubuntu:20.04 /bin/bash               # Interactive mode
docker run --rm alpine echo "Hello"                 # Remove after exit
docker run -v /host/path:/container/path nginx       # Mount volume
docker run --network mynet nginx                    # Custom network
docker run --memory="512m" --cpus="1.5" nginx       # Resource limits

# Container operations
docker start container_name                          # Start stopped container
docker stop container_name                           # Graceful stop
docker kill container_name                           # Force stop
docker restart container_name                        # Restart container
docker pause container_name                          # Pause processes
docker unpause container_name                        # Unpause processes

# Inspection and debugging
docker logs container_name                           # View logs
docker logs -f container_name                        # Follow logs
docker exec -it container_name /bin/bash            # Execute command in running container
docker inspect container_name                        # Detailed container info
docker stats                                         # Real-time resource usage
docker top container_name                            # Running processes
```

### Image Management

```bash
# Building and managing images
docker build -t myapp:v1 .                          # Build from Dockerfile
docker build -t myapp:v1 -f Dockerfile.prod .       # Custom Dockerfile
docker build --no-cache -t myapp:v1 .               # Build without cache
docker tag myapp:v1 myregistry.com/myapp:v1         # Tag image

# Registry operations
docker login                                         # Login to registry
docker push myapp:v1                                # Push to registry
docker pull ubuntu:20.04                            # Pull from registry
docker search nginx                                  # Search Docker Hub

# Image inspection
docker images                                        # List images
docker image ls                                      # List images (alternative)
docker history image_name                            # Image layer history
docker image inspect image_name                      # Detailed image info
```

### System Management

```bash
# Cleanup commands
docker system prune                                  # Remove unused data
docker system prune -a                              # Remove all unused images
docker container prune                               # Remove stopped containers
docker image prune                                   # Remove dangling images
docker volume prune                                  # Remove unused volumes
docker network prune                                 # Remove unused networks

# System information
docker version                                       # Docker version info
docker info                                          # System-wide information
docker system df                                     # Disk usage
docker system events                                 # Real-time events
```

## Container Lifecycle

```
┌─────────┐    docker run     ┌─────────┐    docker stop    ┌─────────┐
│ Created │ ──────────────────▶│ Running │ ──────────────────▶│ Stopped │
└─────────┘                   └─────────┘                   └─────────┘
     │                             │                             │
     │ docker start                │ docker pause                │ docker start
     │                             ▼                             │
     │                        ┌─────────┐                       │
     └────────────────────────│ Paused  │◀──────────────────────┘
                              └─────────┘
                                   │
                              docker unpause
                                   │
                                   ▼
                              ┌─────────┐    docker kill     ┌─────────┐
                              │ Running │ ──────────────────▶│ Killed  │
                              └─────────┘                   └─────────┘
                                                                 │
                                                            docker rm
                                                                 │
                                                                 ▼
                                                            ┌─────────┐
                                                            │ Removed │
                                                            └─────────┘
```

### Lifecycle Commands

| State | Command | Description |
|-------|---------|-------------|
| **Create** | `docker create` | Create container without starting |
| **Start** | `docker start` | Start existing container |
| **Run** | `docker run` | Create and start in one command |
| **Pause** | `docker pause` | Suspend all processes |
| **Unpause** | `docker unpause` | Resume paused processes |
| **Stop** | `docker stop` | Graceful shutdown (SIGTERM) |
| **Kill** | `docker kill` | Force shutdown (SIGKILL) |
| **Remove** | `docker rm` | Delete container |

## Networking

### Network Types

| Network Type | Description | Use Case | Command |
|--------------|-------------|----------|---------|
| **Bridge** | Default, isolated network | Single host communication | `docker run --network bridge` |
| **Host** | Share host network stack | High performance, no isolation | `docker run --network host` |
| **None** | No network access | Security, isolated containers | `docker run --network none` |
| **Overlay** | Multi-host networking | Docker Swarm, distributed apps | `docker network create -d overlay` |
| **Macvlan** | Assign MAC address to container | Legacy apps, direct network access | `docker network create -d macvlan` |

```bash
# Network management
docker network ls                                    # List networks
docker network create mynetwork                     # Create custom network
docker network create --driver bridge mybridge     # Create bridge network
docker network inspect mynetwork                    # Network details
docker network connect mynetwork container_name     # Connect container to network
docker network disconnect mynetwork container_name  # Disconnect from network
docker network rm mynetwork                         # Remove network

# Port mapping
docker run -p 8080:80 nginx                        # Map host:container port
docker run -p 127.0.0.1:8080:80 nginx             # Bind to specific interface
docker run -P nginx                                # Map all exposed ports randomly
```

### Container Communication

```bash
# Same network communication
docker network create myapp-network
docker run -d --name database --network myapp-network postgres
docker run -d --name webapp --network myapp-network myapp
# webapp can reach database using hostname "database"

# Legacy linking (deprecated)
docker run -d --name db postgres
docker run -d --name web --link db:database webapp
# web can reach db using hostname "database"
```

## Volumes & Storage

### Volume Types

| Type | Description | Persistence | Performance | Use Case |
|------|-------------|-------------|-------------|----------|
| **Named Volume** | Managed by Docker | High | Good | Database data, shared data |
| **Bind Mount** | Host directory mounted | High | Best | Development, config files |
| **tmpfs Mount** | Memory-based storage | None | Excellent | Temporary data, secrets |

```bash
# Volume management
docker volume create myvolume                       # Create named volume
docker volume ls                                    # List volumes
docker volume inspect myvolume                      # Volume details
docker volume rm myvolume                          # Remove volume

# Using volumes
docker run -v myvolume:/data nginx                  # Named volume
docker run -v /host/path:/container/path nginx      # Bind mount
docker run --tmpfs /tmp nginx                       # tmpfs mount
docker run --mount type=volume,source=myvolume,target=/data nginx  # Mount syntax

# Volume examples
docker run -d --name postgres -v pgdata:/var/lib/postgresql/data postgres
docker run -d --name webapp -v /host/logs:/app/logs myapp
```

### Storage Best Practices

```bash
# Read-only containers
docker run --read-only --tmpfs /tmp nginx

# Volume backup
docker run --rm -v myvolume:/data -v $(pwd):/backup alpine tar czf /backup/backup.tar.gz -C /data .

# Volume restore
docker run --rm -v myvolume:/data -v $(pwd):/backup alpine tar xzf /backup/backup.tar.gz -C /data
```

## Docker Compose

### Basic Structure

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    environment:
      - DEBUG=1
    depends_on:
      - db
      - redis
    networks:
      - app-network

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app-network

  redis:
    image: redis:alpine
    networks:
      - app-network

volumes:
  postgres_data:

networks:
  app-network:
    driver: bridge
```

### Compose Commands

```bash
# Basic operations
docker-compose up                                   # Start services
docker-compose up -d                               # Start in background
docker-compose down                                # Stop and remove containers
docker-compose down -v                             # Also remove volumes
docker-compose restart                             # Restart services

# Service management
docker-compose start service_name                  # Start specific service
docker-compose stop service_name                   # Stop specific service
docker-compose logs service_name                   # View service logs
docker-compose exec service_name bash              # Execute command in service

# Scaling and building
docker-compose up --scale web=3                    # Scale service
docker-compose build                               # Build images
docker-compose pull                                # Pull latest images
```

### Advanced Compose Features

```yaml
# Environment files
env_file:
  - .env
  - .env.local

# Health checks
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
  interval: 30s
  timeout: 10s
  retries: 3

# Resource limits
deploy:
  resources:
    limits:
      cpus: '0.5'
      memory: 512M
    reservations:
      cpus: '0.25'
      memory: 256M

# Secrets
secrets:
  db_password:
    file: ./db_password.txt
```

## Docker Swarm

### Swarm Mode

```bash
# Initialize swarm
docker swarm init                                   # Initialize swarm manager
docker swarm init --advertise-addr 192.168.1.100   # Specify IP

# Join swarm
docker swarm join --token <token> 192.168.1.100:2377  # Join as worker
docker swarm join-token worker                      # Get worker token
docker swarm join-token manager                     # Get manager token

# Node management
docker node ls                                      # List nodes
docker node inspect node_name                      # Node details
docker node update --availability drain node_name   # Drain node
docker node rm node_name                           # Remove node
```

### Service Management

```bash
# Service operations
docker service create --name web --replicas 3 -p 8080:80 nginx
docker service ls                                   # List services
docker service ps web                              # Service tasks
docker service inspect web                         # Service details
docker service update --replicas 5 web             # Scale service
docker service rm web                              # Remove service

# Stack deployment
docker stack deploy -c docker-compose.yml mystack  # Deploy stack
docker stack ls                                    # List stacks
docker stack services mystack                      # Stack services
docker stack rm mystack                           # Remove stack
```

### Swarm Networking

```bash
# Overlay networks
docker network create --driver overlay --attachable myoverlay
docker service create --network myoverlay --name web nginx

# Load balancing
docker service create --name web --replicas 3 --publish 8080:80 nginx
# Automatic load balancing across replicas
```

## Security

### Container Security Best Practices

| Practice | Command/Configuration | Purpose |
|----------|----------------------|---------|
| **Non-root user** | `USER 1000:1000` in Dockerfile | Reduce privilege escalation risk |
| **Read-only filesystem** | `docker run --read-only` | Prevent runtime modifications |
| **Drop capabilities** | `docker run --cap-drop ALL --cap-add NET_BIND_SERVICE` | Minimize privileges |
| **Security options** | `docker run --security-opt no-new-privileges:true` | Prevent privilege escalation |
| **Resource limits** | `docker run --memory="512m" --cpus="1.0"` | Prevent resource exhaustion |

```bash
# Security scanning
docker scan image_name                              # Scan for vulnerabilities
docker trust sign image_name                       # Sign image
docker trust inspect image_name                    # Verify signature

# Secure container execution
docker run --user 1000:1000 \
  --read-only \
  --cap-drop ALL \
  --cap-add NET_BIND_SERVICE \
  --security-opt no-new-privileges:true \
  --tmpfs /tmp \
  nginx

# Secrets management
docker secret create my_secret secret.txt          # Create secret
docker service create --secret my_secret nginx     # Use secret in service
```

### Dockerfile Security

```dockerfile
# Security-focused Dockerfile
FROM node:16-alpine

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nextjs -u 1001

# Install dependencies as root
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Copy application files
COPY --chown=nextjs:nodejs . .

# Switch to non-root user
USER nextjs

# Use specific port
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

CMD ["npm", "start"]
```

### Image Security

```bash
# Use official base images
FROM node:16-alpine                                 # Official, minimal image

# Multi-stage builds to reduce attack surface
FROM node:16-alpine AS builder
# ... build steps ...
FROM node:16-alpine AS runtime
COPY --from=builder /app/dist ./dist

# Scan images regularly
docker scan myapp:latest
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
  aquasec/trivy image myapp:latest
```

## Best Practices

### Image Optimization

| Practice | Example | Benefit |
|----------|---------|---------|
| **Use minimal base images** | `FROM alpine:3.14` | Smaller size, fewer vulnerabilities |
| **Multi-stage builds** | Build → Runtime stages | Exclude build tools from final image |
| **Layer caching** | Order instructions by change frequency | Faster builds |
| **Combine RUN commands** | `RUN apt update && apt install` | Fewer layers |
| **Clean up in same layer** | `RUN apt install && apt clean` | Smaller image size |

```dockerfile
# Optimized Dockerfile
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

FROM node:16-alpine AS runtime
RUN addgroup -g 1001 -S nodejs && adduser -S nextjs -u 1001
WORKDIR /app
COPY --from=builder --chown=nextjs:nodejs /app/node_modules ./node_modules
COPY --chown=nextjs:nodejs . .
USER nextjs
EXPOSE 3000
CMD ["npm", "start"]
```

### Performance Optimization

```bash
# Build optimization
docker build --build-arg BUILDKIT_INLINE_CACHE=1 -t myapp .
docker build --target runtime -t myapp .           # Build specific stage

# Runtime optimization
docker run --memory="512m" --cpus="1.0" myapp      # Resource limits
docker run --restart=unless-stopped myapp          # Auto-restart policy
docker run --log-driver=json-file --log-opt max-size=10m myapp  # Log rotation
```

### Development Workflow

```bash
# Development setup
docker run -it --rm -v $(pwd):/app -w /app node:16 npm install
docker run -it --rm -v $(pwd):/app -w /app -p 3000:3000 node:16 npm start

# Hot reload with bind mounts
docker run -d --name dev-app -v $(pwd):/app -p 3000:3000 myapp-dev

# Database for development
docker run -d --name dev-db -e POSTGRES_PASSWORD=dev -p 5432:5432 postgres:13
```

## Troubleshooting

### Common Issues and Solutions

| Issue | Symptoms | Solution |
|-------|----------|----------|
| **Container exits immediately** | `docker ps` shows no running containers | Check logs: `docker logs container_name` |
| **Port already in use** | `bind: address already in use` | Use different port or stop conflicting service |
| **Permission denied** | Cannot access files/directories | Check file permissions, use correct user |
| **Out of disk space** | Build fails, cannot pull images | Clean up: `docker system prune -a` |
| **Network connectivity** | Cannot reach other containers | Check network configuration, DNS resolution |

### Debugging Commands

```bash
# Container debugging
docker logs -f container_name                       # Follow logs
docker exec -it container_name /bin/sh             # Interactive shell
docker inspect container_name                       # Detailed info
docker stats container_name                         # Resource usage
docker top container_name                           # Running processes

# System debugging
docker system events                                # Real-time events
docker system df                                    # Disk usage
docker info                                         # System information
docker version                                      # Version details

# Network debugging
docker network ls                                   # List networks
docker network inspect network_name                 # Network details
docker exec container_name nslookup hostname        # DNS resolution
docker exec container_name ping container2          # Connectivity test
```

### Performance Monitoring

```bash
# Resource monitoring
docker stats                                        # All containers
docker stats container_name                         # Specific container
docker system df                                    # Disk usage
docker system events --filter container=myapp      # Filtered events

# Log analysis
docker logs --since="2h" container_name            # Recent logs
docker logs --tail=100 container_name              # Last 100 lines
docker logs --timestamps container_name            # With timestamps
```

## Interview Questions

### Entry Level Questions

**Q: What is Docker and how does it differ from virtual machines?**
A: Docker is a containerization platform that packages applications with their dependencies. Unlike VMs that virtualize hardware and run full operating systems, Docker containers share the host OS kernel, making them lightweight and faster to start.

**Q: Explain the difference between Docker image and container.**
A: A Docker image is a read-only template containing application code, dependencies, and configuration. A container is a running instance of an image that can be started, stopped, and modified.

**Q: What is a Dockerfile?**
A: A Dockerfile is a text file containing instructions to build a Docker image. It specifies the base image, dependencies, configuration, and commands needed to create the application environment.

**Q: How do you expose a port in Docker?**
A: Use the `-p` flag: `docker run -p host_port:container_port image_name`. For example, `docker run -p 8080:80 nginx` maps host port 8080 to container port 80.

### Mid-Level Questions

**Q: Explain the difference between RUN, CMD, and ENTRYPOINT.**
A: 
- `RUN`: Executes commands during image build, creates new layers
- `CMD`: Specifies default command, can be overridden at runtime
- `ENTRYPOINT`: Defines fixed command that always runs, arguments can be appended

**Q: What are Docker volumes and why are they important?**
A: Docker volumes provide persistent storage that survives container restarts and deletions. They enable data sharing between containers and host, and are essential for databases and stateful applications.

**Q: How do you optimize Docker images?**
A: Use multi-stage builds, minimal base images (Alpine), combine RUN commands, order layers by change frequency, remove unnecessary files, and use .dockerignore to exclude files.

**Q: Explain Docker networking modes.**
A: 
- Bridge: Default, isolated network for single host
- Host: Share host network stack, no isolation
- None: No network access
- Overlay: Multi-host networking for Swarm
- Macvlan: Assign MAC addresses to containers

### Senior-Level Questions

**Q: How would you implement zero-downtime deployment with Docker?**
A: Use rolling updates with Docker Swarm or orchestration platforms like Kubernetes. Implement health checks, use load balancers, and deploy new versions gradually while keeping old versions running until new ones are healthy.

**Q: Describe Docker security best practices.**
A: Use non-root users, minimal base images, scan for vulnerabilities, implement resource limits, use secrets management, enable content trust, apply security profiles (AppArmor/SELinux), and follow principle of least privilege.

**Q: How do you handle secrets in Docker?**
A: Use Docker secrets in Swarm mode, environment variables for development, external secret management systems (HashiCorp Vault, AWS Secrets Manager), and avoid embedding secrets in images.

**Q: Explain Docker Swarm vs Kubernetes.**
A: Docker Swarm is simpler, integrated with Docker, good for smaller deployments. Kubernetes is more complex but offers advanced features, better ecosystem, and is industry standard for large-scale container orchestration.

### Advanced Scenarios

**Q: How would you troubleshoot a container that keeps crashing?**
A: 
1. Check logs: `docker logs container_name`
2. Inspect container: `docker inspect container_name`
3. Check resource usage: `docker stats`
4. Run interactively: `docker run -it image_name /bin/sh`
5. Check health checks and dependencies
6. Review application logs and configuration

**Q: Design a multi-tier application deployment strategy.**
A: Use Docker Compose for development, implement service discovery, separate networks for different tiers, use volumes for data persistence, implement health checks, configure load balancing, and plan for scaling and monitoring.

**Q: How do you implement container monitoring and logging?**
A: Use centralized logging (ELK stack, Fluentd), implement metrics collection (Prometheus, Grafana), set up health checks, use log drivers for structured logging, and implement alerting for critical issues.

### Performance and Optimization

**Q: How do you optimize Docker build performance?**
A: Use build cache effectively, implement multi-stage builds, use .dockerignore, order Dockerfile instructions by change frequency, use specific tags instead of 'latest', and consider using BuildKit for advanced features.

**Q: Explain Docker layer caching and how to leverage it.**
A: Docker caches each layer during build. If a layer hasn't changed, Docker reuses the cached version. Optimize by placing frequently changing instructions (like COPY source code) after stable ones (like installing dependencies).

This comprehensive Docker guide covers all essential concepts needed to excel in Docker interviews, from basic containerization concepts to advanced orchestration and security practices.