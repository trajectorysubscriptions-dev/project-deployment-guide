# Project Deployment Guide

Comprehensive deployment instructions for the project-deployment-guide repository.

## 🚀 Quick Start

### Prerequisites
- Git installed
- Docker v20+ installed
- Node.js v18+ (for local development)
- Access to production environment credentials

### Clone & Setup
```bash
git clone https://github.com/trajectorysubscriptions-dev/project-deployment-guide.git
cd project-deployment-guide
cp .env.example .env
# Edit .env with your configuration values
```

## 📋 Deployment Steps

### Step 1: Environment Configuration
- Set `DATABASE_URL` for PostgreSQL connection
- Set `API_KEY` and `SECRET_KEY` for authentication
- Configure `REDIS_URL` for caching layer
- Set `NODE_ENV=production`

### Step 2: Build Application
```bash
npm install --production
npm run build
docker build -t project-deployment-guide:latest .
```

### Step 3: Run Database Migrations
```bash
npm run db:migrate
```

### Step 4: Deploy with Docker Compose
```bash
docker-compose -f docker-compose.prod.yml up -d
```

### Step 5: Verify Deployment
```bash
curl http://localhost:3000/health
docker-compose logs -f
```

## 🔄 CI/CD Pipeline
- Push to `main` triggers automated deployment
- Pull requests run tests and linting automatically
- Staging deploys on `develop` branch merges

## 🔙 Rollback
```bash
docker-compose -f docker-compose.prod.yml down
git checkout <previous-tag>
docker-compose -f docker-compose.prod.yml up -d
```

## 📊 Monitoring
- Health endpoint: `/health`
- Metrics endpoint: `/metrics`
- Logs: `docker-compose logs -f`

## 📝 License
MIT
