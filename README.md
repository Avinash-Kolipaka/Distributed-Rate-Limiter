# Distributed Rate Limiting Control Plane for Scalable API Systems

A cloud-native distributed rate limiting system designed to control API traffic, prevent abuse, and maintain system stability under high concurrency.

This project implements a production-style Token Bucket rate limiter using Redis Lua scripting for atomic operations, Dockerized infrastructure, AWS deployment, observability with Prometheus and Grafana.

---

## 🚀 Features

- Distributed Token Bucket Rate Limiting
- Atomic Redis Lua Script Operations
- API Key–Based User Tier Limits
- Redis Caching Layer
- MongoDB Request Logging
- Dockerized Infrastructure
- AWS EC2 Cloud Deployment
- Prometheus Metrics Collection
- Grafana Monitoring Dashboard
- GitHub Actions CI/CD Automation
- High-Concurrency Request Handling

---

## 🏗️ System Architecture

```text
Client
   ↓
Node.js + Express API Server
   ↓
Rate Limiter Middleware
   ↓
Redis (Token Storage + Lua Scripts)
   ↓
MongoDB Atlas (Logs + Config)

Monitoring Stack:
Prometheus → Grafana  
```

---

## ⚙️ Tech Stack

### Backend
- Node.js
- Express.js
- TypeScript

### Data Layer
- Redis (Lua Scripting)
- MongoDB Atlas

### Cloud and DevOps
- Docker
- Docker Compose
- AWS EC2
- GitHub Actions (CI/CD)

### Monitoring
- Prometheus
- Grafana

### Core Concepts
- Distributed Systems
- Token Bucket Algorithm
- Concurrency Control
- Atomic Operations
- Observability

---

## 🔥 Problem Statement

In distributed systems, uncontrolled API traffic can:

- Overload servers
- Cause denial-of-service issues
- Create unfair resource consumption

This project solves that problem by implementing a scalable distributed rate limiter capable of enforcing configurable request limits across multiple services and users.

---

## 📋 Getting Started

### Prerequisites
- Docker and Docker Compose
- Node.js 16+
- Redis
- MongoDB Atlas Account
- AWS Account (for deployment)

### Installation

1. Clone the repository
```bash
git clone https://github.com/Avinash-Kolipaka/Distributed-Rate-Limiter.git
cd Distributed-Rate-Limiter
```

2. Install dependencies
```bash
npm install
```

3. Set up environment variables
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. Start with Docker Compose
```bash
docker-compose up
```

---

## 📊 Monitoring

Access the monitoring dashboards:
- **Prometheus**: http://localhost:9090
- **Grafana**: http://localhost:3000

---

## 🚀 Deployment

### AWS EC2 Deployment

1. Build Docker image
```bash
docker build -t distributed-rate-limiter .
```

2. Push to AWS ECR
```bash
aws ecr get-login-password | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
docker tag distributed-rate-limiter:latest <account-id>.dkr.ecr.<region>.amazonaws.com/distributed-rate-limiter:latest
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/distributed-rate-limiter:latest
```

3. Deploy to EC2 instance
```bash
ssh -i your-key.pem ec2-user@your-instance
docker pull <account-id>.dkr.ecr.<region>.amazonaws.com/distributed-rate-limiter:latest
docker run -d -p 3000:3000 --env-file .env <account-id>.dkr.ecr.<region>.amazonaws.com/distributed-rate-limiter:latest
```

---

## 🧪 Testing

Run tests with:
```bash
npm test
```

Run concurrent load tests:
```bash
npm run test:load
```

---

## 📝 API Documentation

### Endpoints

#### 1. Rate Limit Check
```
POST /api/rate-limit
Content-Type: application/json

{
  "apiKey": "your-api-key",
  "userId": "user-123"
}
```

Response:
```json
{
  "allowed": true,
  "remaining": 95,
  "resetAt": 1234567890,
  "limit": 100
}
```

#### 2. Admin Endpoints
- `POST /admin/users` - Create user with tier limits
- `GET /admin/users/:id` - Get user details
- `PUT /admin/users/:id/limits` - Update rate limits
- `DELETE /admin/users/:id` - Delete user

---

## 🔐 Security

- API Key validation
- JWT-based authentication
- Rate limit enforcement at middleware level
- CORS configuration for frontend

---

## 📚 Project Structure

```
.
├── src/
│   ├── middleware/
│   │   └── rateLimiter.ts
│   ├── routes/
│   │   ├── admin.ts
│   │   └── api.ts
│   ├── services/
│   │   ├── redisService.ts
│   │   ├── mongoService.ts
│   │   └── metricsService.ts
│   ├── config/
│   │   └── index.ts
│   └── app.ts
├── tests/
├── docker-compose.yml
├── Dockerfile
└── package.json
```

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 👥 Authors

- **Avinash Kolipaka** - Initial creator
- **Tej Praval** - Core development and features

---

## 📞 Support

For support, email avinashkolipaka@gmail.com or create an issue on GitHub.

---

## 🙏 Acknowledgments

- Redis for atomic scripting capabilities
- Express.js community
- Docker for containerization
- AWS for cloud infrastructure
