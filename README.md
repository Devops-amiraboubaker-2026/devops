# devops-scripts

DevOps automation scripts for provisioning and deploying the application stack.

## Directory Structure

```
devops-scripts/
├── frontend/              # Frontend Docker Compose stack
│   └── docker-compose.yml
├── backend/               # Backend Docker Compose stack
│   ├── docker-compose.yml
│   └── .env
└── provision/             # Ansible provisioning playbook
    ├── playbook.yml
    ├── inventory.ini
    └── roles/
        ├── docker/
        ├── nginx/
        ├── certbot/
        ├── mongo/
        ├── postgres/
        ├── redis/
        └── monitoring/
```

## Components

### Frontend Stack
- Docker Compose configuration for the frontend application
- Exposes the app on port 3000
- Uses pre-built Docker image: `amira100/frontend-session18`

### Backend Stack
- Docker Compose configuration for the backend API and MongoDB
- Backend API service with environment variable support
- MongoDB database container with persistent volume
- Mongo-Express admin interface available

### Provisioning (Ansible)
Automated VPS provisioning playbook that installs and configures:
- **Docker** and Docker Compose
- **Nginx** web server
- **Certbot** for SSL/TLS certificates
- **MongoDB** database
- **PostgreSQL** database
- **Redis** cache
- **Monitoring** stack (Prometheus)

## Usage

### Provision a VPS
```bash
ansible-playbook -i provision/inventory.ini provision/playbook.yml
```

### Deploy Frontend Stack
```bash
cd devops-scripts/frontend
docker compose up -d
```

### Deploy Backend Stack
```bash
cd devops-scripts/backend
docker compose up -d
```

## Configuration
- Copy `.env.example` to `.env` and fill in your values before deploying the backend stack
- Edit `provision/inventory.ini` to add or modify target VPS servers