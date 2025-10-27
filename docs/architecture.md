# System Architecture

## Overview
DevOps Simulator follows a microservices architecture designed for high availability and scalability.  
This document covers both **production** and **development** configurations.

---

## Components

### 1. Application Server
- **Technology**: Node.js + Express
- **Production Port**: 8080  
- **Development Port**: 3000  
- **Scaling**: Horizontal auto-scaling (production only)  
- **Development Features**: Hot reload, Chrome DevTools debugger on port 9229  
- **Notes**: Runs in Docker Compose during development for faster iteration.

---

### 2. Database Layer
- **Database**: PostgreSQL 14  
- **Production**:
  - Master-slave replication  
  - Automated daily backups  
  - Encrypted connections  
- **Development**:
  - Single local instance  
  - Auto-seeds test data on startup  
  - Manual backups only  
- **Backup Retention**: 30 days (production)  

---

### 3. Monitoring System
- **Production**:
  - Prometheus + Grafana dashboards  
  - Email alerts for critical issues  
  - Metrics tracked: CPU, Memory, Disk, Network  
- **Development**:
  - Console logging with verbose output  
  - Optional Prometheus integration  
  - Additional metric: Build time  
  - Dashboard: In-development web interface  
- **Experimental**: AI-powered log analysis and anomaly detection

---

### 4. Container Orchestration
- **Production**: Kubernetes (rolling updates)  
- **Development**: Docker Compose (local orchestration)  
- **Services**: Application, Database, Redis cache  
- **Features**: Hot reload via volume mounts  

---

### 5. Authentication System (Beta)
- **Method**: OAuth2 + JWT  
- **Providers**: Google, GitHub (for testing)  
- **Session Storage**: Redis-based  
- **Production**: Strict access controls  
- **Development**: Relaxed authentication and open CORS  

---

## Deployment Strategy

### Production
- **Method**: Rolling updates (Kubernetes)
- **Zero-downtime**: Yes
- **Rollback**: Automated on failure
- **Region**: us-east-1
- **Load Balancing**: Enabled with health checks

### Development
- **Method**: Docker Compose with hot reload
- **Features**: Instant feedback loop, code watch
- **Testing**: Automated unit tests before deployment
- **Rollback**: Git checkout to previous commit

---

## Development Workflow
1. Make code changes locally  
2. Auto-reload triggers rebuild  
3. Run tests automatically (`npm test`)  
4. Monitor console logs  
5. Commit changes when stable  

---

## Security

### Production
- SSL/TLS encryption  
- Encrypted database connections  
- Strict access controls  
- Regular security audits  

### Development
- SSL/TLS disabled (local use only)  
- Plaintext credentials  
- CORS enabled for all origins  
- Debug endpoints and source maps enabled  

---

## Experimental Features
⚠️ **Warning**: The following are experimental and not for production use:
- Multi-cloud deployment support  
- AI-powered log analysis  
- Automatic rollback on anomaly detection  

---

_Last updated: Combined version (Production + Development)_
