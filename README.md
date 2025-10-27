# CodeCraft Summit 2025

[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-16.0-black.svg)](https://nextjs.org/)
[![Fastify](https://img.shields.io/badge/Fastify-5.6+-green.svg)](https://www.fastify.io/)
[![License](https://img.shields.io/badge/License-ISC-purple.svg)](LICENSE)

> **Português:** [Documentação em Português](./docs/README-pt.md)

A modern, full-stack event management system for the CodeCraft Summit 2025, featuring user subscriptions, referral tracking, and real-time rankings. Built with cutting-edge technologies and designed for scalability and performance.

## 🚀 Project Overview

CodeCraft Summit 2025 is a comprehensive event management platform that enables seamless user registration and referral tracking. The system features a sophisticated invitation-based referral system where participants can earn points by inviting others, compete in rankings, and track their statistics in real-time.

### Key Features

- **🎫 Smart Registration System** - Streamlined user subscription with form validation
- **🔗 Referral Program** - Invite tracking with unique referral links and click analytics
- **🏆 Real-time Rankings** - Dynamic leaderboard showing top referrers
- **📊 Personal Analytics** - Individual statistics dashboard for each subscriber
- **📱 Responsive Design** - Mobile-first approach with beautiful UI components
- **🔒 Type-Safe APIs** - Fully typed backend with Zod validation
- **⚡ High Performance** - Fast database queries with optimized caching

## 🏗️ Architecture

This project follows a modern monorepo structure with clear separation between frontend and backend:

```
devstage-events/
├── web/                 # Next.js 16 frontend application
│   ├── src/
│   │   ├── app/        # App Router pages and layouts
│   │   ├── components/ # Reusable UI components
│   │   ├── http/       # API client with generated types
│   │   └── assets/     # Static assets and images
│   └── orval.config.ts # OpenAPI client generation config
├── server/              # Fastify backend API
│   ├── src/
│   │   ├── routes/     # API endpoint definitions
│   │   ├── functions/  # Business logic functions
│   │   ├── drizzle/    # Database schema and migrations
│   │   └── redis/      # Redis client configuration
│   └── env.ts          # Environment variable validation
└── docs/               # Documentation
```

## 🛠️ Technology Stack

### Frontend (Next.js 16)
- **Framework**: Next.js 16 with App Router
- **Language**: TypeScript 5.0+
- **Styling**: Tailwind CSS 4.1 with custom design system
- **UI Components**: Custom component library with Lucide React icons
- **Forms**: React Hook Form with Zod validation
- **HTTP Client**: Auto-generated from OpenAPI spec using Orval
- **Linting**: Biome for code formatting and linting

### Backend (Fastify)
- **Framework**: Fastify 5.6 with Zod type provider
- **Language**: TypeScript 5.9+
- **Database**: PostgreSQL with Drizzle ORM
- **Cache**: Redis for performance optimization
- **API Documentation**: OpenAPI 3.0 with Swagger UI
- **Validation**: Zod schemas for request/response validation
- **Code Quality**: Biome for consistent code formatting

### Infrastructure & Tools
- **Package Manager**: npm
- **Build Tools**: tsup for backend, Next.js for frontend
- **Development**: tsx for hot reloading during development
- **Database Migrations**: Drizzle Kit
- **Environment**: Environment variable validation with Zod
- **Containerization**: Docker Compose for database services (PostgreSQL & Redis)

## 📋 Prerequisites

Before running this project, ensure you have the following installed:

- **Node.js** 18.0 or higher
- **PostgreSQL** 13 or higher (or use Docker)
- **Redis** 6 or higher (or use Docker)
- **npm** (comes with Node.js)
- **Docker** (optional, for database services)
- **Docker Compose** (optional, for database services)

## 🚀 Quick Start

### Option 1: Using Docker for Database Services (Recommended)

The easiest way to get PostgreSQL and Redis running is using Docker Compose:

```bash
# Start database services (PostgreSQL and Redis)
cd server
docker compose up -d

# View logs
docker compose logs -f

# Stop database services
docker compose down
```

### Option 2: Local Development

### 1. Clone the Repository

```bash
git clone https://github.com/MiguelMachado-dev/devstage-events.git
cd devstage-events
```

### 2. Install Dependencies

```bash
# Install backend dependencies
cd server
npm install

# Install frontend dependencies
cd ../web
npm install
```

### 3. Environment Setup

Create environment files for both services:

**Backend Environment** (`server/.env`):
```env
PORT=3333
POSTGRES_URL=postgresql://docker:docker@localhost:5432/connect
REDIS_URL=redis://localhost:6379
WEB_URL=http://localhost:3000
```

**Frontend Environment** (`web/.env.local`):
```env
NEXT_PUBLIC_API_URL=http://localhost:3333
```

### 4. Database Setup

If you're using Docker Compose for database services, the databases are already configured. Just run migrations:

```bash
cd server
npx drizzle-kit push
```

If you prefer to use local database installations, update the `POSTGRES_URL` and `REDIS_URL` in your `.env` file accordingly.

### 5. Start Development Servers

Run both services in separate terminals:

```bash
# Terminal 1: Start backend server
cd server
npm run dev

# Terminal 2: Start frontend server
cd web
npm run dev
```

The application will be available at:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3333
- **API Documentation**: http://localhost:3333/docs

## 🎯 Usage Guide

### User Registration Flow

1. **Home Page**: Users access the landing page with event information
2. **Registration**: Fill out the subscription form with name and email
3. **Referral Link**: Receive a unique referral link after successful registration
4. **Share & Track**: Share the referral link and track invitations
5. **Rankings**: View real-time rankings and personal statistics

### API Endpoints

The API provides the following endpoints:

- `POST /subscriptions` - Register a new subscriber
- `GET /invites/{subscriberId}` - Access invite link (redirects to main site)
- `GET /subscribers/{subscriberId}/ranking/clicks` - Get click count for referrals
- `GET /subscribers/{subscriberId}/ranking/count` - Get referral count
- `GET /subscribers/{subscriberId}/ranking/position` - Get ranking position
- `GET /ranking` - Get top referrers ranking

### Development Features

- **Hot Reloading**: Both frontend and backend support hot reloading during development
- **Type Safety**: Full TypeScript support with generated API types
- **API Documentation**: Interactive Swagger UI available at `/docs`
- **Database Migrations**: Drizzle Kit for schema management
- **Code Formatting**: Automatic code formatting with Biome

## 🔧 Configuration

### Database Configuration

The project uses PostgreSQL as the primary database. The connection is configured through environment variables:

```typescript
// server/env.ts
const envSchema = z.object({
  POSTGRES_URL: z.url(),
  // ... other variables
})
```

### Redis Configuration

Redis is used for caching and performance optimization:

```typescript
// server/src/redis/client.ts
import Redis from 'ioredis'
export const redis = new Redis(process.env.REDIS_URL)
```

### API Documentation

The backend automatically generates OpenAPI documentation. Access it at:
- **Swagger UI**: http://localhost:3333/docs
- **OpenAPI JSON**: http://localhost:3333/docs/json

## 🧪 Development Workflow

### Code Quality

This project uses Biome for code formatting and linting:

```bash
# Format code
npx biome format --write .

# Check code quality
npx biome check .
```

### Database Migrations

To manage database schema changes:

```bash
# Generate migrations
npx drizzle-kit generate

# Apply migrations
npx drizzle-kit push

# View migrations
npx drizzle-kit studio
```

### API Client Generation

The frontend API client is automatically generated from the OpenAPI spec:

```bash
cd web
npx orval
```

## 📦 Build & Deployment

### Production Build

```bash
# Build backend
cd server
npm run build

# Build frontend
cd ../web
npm run build
```

### Deployment Considerations

- Ensure all environment variables are set in production
- Run database migrations before starting the application
- Configure proper CORS settings for the frontend domain
- Set up Redis for production caching
- Consider using CDN for static assets
- Use HTTPS and configure SSL certificates
- Set up proper monitoring and logging
- Configure backup strategies for PostgreSQL

### Docker Compose for Database Services

The project includes Docker Compose configuration for easy database setup:

#### Available Services

- **service-pg**: PostgreSQL database (port 5432)
- **service-redis**: Redis cache (port 6379)

#### Database Environment Variables

```bash
# Database (PostgreSQL)
POSTGRES_USER=docker
POSTGRES_PASSWORD=docker
POSTGRES_DB=connect

# Redis
ALLOW_EMPTY_PASSWORD=yes
```

#### Using Docker Compose

```bash
# Start database services
cd server
docker compose up -d

# View logs
docker compose logs -f

# Stop services
docker compose down
```

## 🔍 Monitoring & Debugging

### Health Checks

The API provides built-in health checks. Monitor:
- Database connectivity
- Redis connection status
- API response times

### Logging

The application uses console logging in development. For production:
- Implement structured logging
- Set up log aggregation
- Monitor error rates and performance metrics

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Run tests and linting (`npx biome check .`)
5. Commit your changes (`git commit -m 'Add some amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## 📄 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 🙋‍♂️ Support

For support and questions:
- Create an issue in the repository
- Check the API documentation at `/docs`
- Review the code comments and type definitions

---

**Built with ❤️ for the CodeCraft Summit 2025 community**
