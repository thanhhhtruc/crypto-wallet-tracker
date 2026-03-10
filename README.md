# Crypto Wallet Tracker

A full-stack blockchain cryptocurrency wallet tracking and analysis platform with transaction visualization and analytics capabilities.

## 🌐 Live Deployments

- **Frontend**: [https://cos30049-fe-six.vercel.app/](https://cos30049-fe-six.vercel.app/)
- **Backend API**: [https://cos30049-be.onrender.com/docs](https://cos30049-be.onrender.com/docs)

> ⚠️ **Note**: The backend is hosted on Render's free tier and may take ~1 minute to wake up from sleep mode on first request.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Deployment](#deployment)
- [Documentation](#documentation)

## 🎯 Overview

This project is a comprehensive cryptocurrency wallet tracker that allows users to monitor blockchain transactions, analyze wallet activities, and visualize transaction flows using graph-based representations. The platform integrates with blockchain networks and provides real-time insights into cryptocurrency movements.

## ✨ Features

- **Wallet Management**: Track and analyze cryptocurrency wallets
- **Transaction Visualization**: Interactive graph-based transaction flow visualization
- **Real-time Analytics**: Monitor wallet balances and transaction history
- **Multi-Currency Support**: Support for various cryptocurrencies
- **Exchange Rate Tracking**: Real-time cryptocurrency exchange rates
- **User Authentication**: Secure JWT-based authentication
- **Graph Database Integration**: Neo4j for complex relationship queries
- **Responsive Design**: Mobile-friendly interface

## 🛠 Tech Stack

### Frontend (cos30049-fe)
- **Framework**: Next.js 15 with App Router
- **UI Library**: React 19
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Components**: Radix UI, shadcn/ui
- **Visualization**: Recharts, React Flow
- **Blockchain**: Viem
- **Animation**: Framer Motion

### Backend (cos30049-be)
- **Framework**: NestJS
- **Database**: EdgeDB 5.x
- **Graph Database**: Neo4j 5.x
- **Authentication**: Passport.js with JWT
- **API Documentation**: Swagger/OpenAPI
- **Language**: TypeScript

## 📁 Project Structure

```
crypto-wallet-tracker/
├── cos30049-fe/          # Frontend Next.js application
│   ├── src/
│   │   ├── app/          # Next.js App Router pages
│   │   ├── components/   # Reusable UI components
│   │   ├── actions/      # Server actions
│   │   └── lib/          # Utilities and types
│   ├── public/           # Static assets
│   └── docs/             # Frontend documentation
│
└── cos30049-be/          # Backend NestJS application
    ├── src/
    │   ├── modules/      # Feature modules
    │   │   ├── auth/     # Authentication
    │   │   ├── user/     # User management
    │   │   ├── wallet/   # Wallet operations
    │   │   ├── transaction/  # Transaction handling
    │   │   ├── currency/ # Currency management
    │   │   └── neo4j/    # Graph database integration
    │   └── common/       # Shared utilities
    ├── dbschema/         # EdgeDB schema and migrations
    └── docs/             # Backend documentation
```

## 🚀 Getting Started

### Prerequisites

- **Node.js** 18+ (LTS recommended)
- **pnpm** package manager
- **EdgeDB** 5.x
- **Neo4j** 5.x (optional for local development)
- **Git**

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd crypto-wallet-tracker
   ```

2. **Setup Backend**

   ```bash
   cd cos30049-be
   
   # Install dependencies
   pnpm install
   
   # Create environment file (see Environment Variables section)
   cp .env.example .env
   # Edit .env with your configuration
   
   # Initialize EdgeDB
   edgedb project init
   
   # Run database migrations
   pnpm run db:migrate
   
   # Generate TypeScript interfaces
   pnpm run db:generate
   
   # Seed the database (optional)
   pnpm run db:edgedb-seed
   # OR seed from CSV
   pnpm run db:csv-seed
   
   # Start development server
   pnpm run dev
   ```

   The backend will be available at `http://localhost:4000`
   API documentation: `http://localhost:4000/docs`

3. **Setup Frontend**

   ```bash
   cd ../cos30049-fe
   
   # Install dependencies
   pnpm install
   
   # Create environment file (see Environment Variables section)
   touch .env
   # Add: NEXT_PUBLIC_API_URL=http://localhost:4000/api
   
   # Start development server
   pnpm run dev
   ```

   The frontend will be available at `http://localhost:3000`

## 🔐 Environment Variables

### Backend (.env)

Create a `.env` file in the `cos30049-be` directory with the following variables:

```properties
# Swagger API Documentation
SWAGGER_API_TITLE=Crypto Wallet Tracker API
SWAGGER_API_DESCRIPTION=API for cryptocurrency wallet tracking and analysis
SWAGGER_API_VERSION=1.0.0
SWAGGER_API_PREFIX=/docs

# API Configuration
GLOBAL_API_PREFIX=/api
PORT=4000

# JWT Authentication
JWT_ACCESS_TOKEN_SECRET=your-secret-key-change-in-production
JWT_REFRESH_TOKEN_SECRET=your-refresh-secret-key-change-in-production
JWT_ACCESS_TOKEN_EXPIRATION_MS=3600000
JWT_REFRESH_TOKEN_EXPIRATION_MS=86400000

# Frontend Redirect URL (for authentication callbacks)
AUTH_UI_REDIRECT_URL=http://localhost:3000/callback

# Neo4j Configuration (optional for local development)
NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your-neo4j-password
AURA_INSTANCEID=your-instance-id
AURA_INSTANCENAME=your-instance-name
```

**Security Notes:**
- Change all secret keys before deploying to production
- Never commit the `.env` file to version control
- Use strong, random values for JWT secrets

### Frontend (.env)

Create a `.env` file in the `cos30049-fe` directory:

```properties
# Backend API URL
NEXT_PUBLIC_API_URL=http://localhost:4000/api
```

For production deployment:
```properties
NEXT_PUBLIC_API_URL=https://cos30049-be.onrender.com/api
```

## 📦 Available Scripts

### Backend Scripts

```bash
# Development
pnpm run dev              # Start development server with hot reload
pnpm run start            # Start production server
pnpm run build            # Build for production

# Database
pnpm run db:migrate       # Create and run migrations
pnpm run db:generate      # Generate TypeScript types
pnpm run db:edgedb-seed   # Seed database with generated data
pnpm run db:csv-seed      # Seed from CSV files
pnpm run db:neo4j-seed    # Seed Neo4j graph database

# Code Quality
pnpm run lint             # Lint code
pnpm run format           # Format code with Prettier
```

### Frontend Scripts

```bash
# Development
pnpm run dev              # Start development server
pnpm run build            # Build for production
pnpm run start            # Start production server

# Code Quality
pnpm run lint             # Lint code

# Type Generation
pnpm run typegen          # Generate TypeScript types from API
```

## 🌍 Deployment

### Frontend (Vercel)

The frontend is deployed on Vercel at: [https://cos30049-fe-six.vercel.app/](https://cos30049-fe-six.vercel.app/)

To deploy your own instance:
1. Push your code to GitHub
2. Import the project in Vercel
3. Set the root directory to `cos30049-fe`
4. Add environment variable: `NEXT_PUBLIC_API_URL=https://cos30049-be.onrender.com/api`
5. Deploy

### Backend (Render)

The backend is deployed on Render at: [https://cos30049-be.onrender.com/docs](https://cos30049-be.onrender.com/docs)

To deploy your own instance:
1. Create a new Web Service on Render
2. Connect your GitHub repository
3. Set the root directory to `cos30049-be`
4. Configure build command: `pnpm install && pnpm run build`
5. Configure start command: `pnpm run start`
6. Add all environment variables from the .env section
7. Deploy

> ⚠️ **Free Tier Limitation**: Render free tier services spin down after inactivity. First request may take ~1 minute to wake up.

## 📚 Documentation

### Backend Documentation
- [Architecture Overview](cos30049-be/docs/architecture.md)
- [Data Models](cos30049-be/docs/data-models.md)
- [API Documentation](cos30049-be/docs/api-documentation.md)
- [Data Model Documentation](cos30049-be/docs/data-model-documentation.md)

### Frontend Documentation
- [Architecture Documentation](cos30049-fe/docs/architecture-documentation.md)
- [Technical Documentation](cos30049-fe/docs/technical-documentation.md)

### API Reference
- Swagger UI: [https://cos30049-be.onrender.com/docs](https://cos30049-be.onrender.com/docs)
- Local: `http://localhost:4000/docs`

## 🐛 Troubleshooting

### Backend Issues

- **EdgeDB Connection Error**: Ensure EdgeDB is running and properly initialized
  ```bash
  edgedb project init
  ```

- **Database Migration Fails**: Run migrations in dev mode
  ```bash
  edgedb migration create --dev-mode
  ```

- **Neo4j Connection Error**: Verify Neo4j credentials in `.env` file

### Frontend Issues

- **API Connection Error**: Check that backend is running and `NEXT_PUBLIC_API_URL` is correct

- **Blank Screen**: Clear browser cache and reload

- **Slow Loading**: Backend may be waking up from sleep (wait ~1 minute)

### Common Issues

- **Port Already in Use**: Change the port in `.env` or kill the process using the port
  ```bash
  # Kill process on port 4000 (backend)
  lsof -ti:4000 | xargs kill -9
  
  # Kill process on port 3000 (frontend)
  lsof -ti:3000 | xargs kill -9
  ```

- **Module Not Found**: Clear node_modules and reinstall
  ```bash
  rm -rf node_modules pnpm-lock.yaml
  pnpm install
  ```
