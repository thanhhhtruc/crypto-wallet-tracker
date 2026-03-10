# COS30049 Crypto Wallet Tracker - Backend

Fast, scalable NestJS backend for a cryptocurrency wallet tracking platform with EdgeDB and Neo4j integration.

## 🌐 Live Deployment

**API Documentation**: [https://cos30049-be.onrender.com/docs](https://cos30049-be.onrender.com/docs)

> ⚠️ **Note**: The backend is hosted on Render's free tier and may take ~1 minute to wake up from sleep mode on the first request.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Database Setup](#database-setup)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Available Scripts](#available-scripts)
- [Project Structure](#project-structure)
- [Common Issues](#common-issues)

## 🎯 Overview

This is the backend service for the Crypto Wallet Tracker platform. It provides RESTful APIs for wallet management, transaction tracking, user authentication, and cryptocurrency analytics. The service integrates with EdgeDB for primary data storage and Neo4j for graph-based relationship queries.

## ✨ Features

- **RESTful API**: Comprehensive REST API with Swagger documentation
- **Authentication & Authorization**: JWT-based authentication with refresh tokens
- **Wallet Management**: CRUD operations for cryptocurrency wallets
- **Transaction Tracking**: Monitor and analyze blockchain transactions
- **Exchange Rates**: Real-time cryptocurrency exchange rate tracking
- **Graph Database**: Neo4j integration for complex relationship queries
- **Data Seeding**: Automated database seeding with sample data
- **Type Safety**: Full TypeScript support with generated EdgeDB types
- **Hot Reload**: Fast development with webpack HMR

## 🛠 Tech Stack

- **Framework**: NestJS 10
- **Language**: TypeScript 5
- **Primary Database**: EdgeDB 5.x
- **Graph Database**: Neo4j 5.x (Aura)
- **Authentication**: Passport.js with JWT strategy
- **Validation**: Zod with nestjs-zod
- **API Documentation**: Swagger/OpenAPI
- **Logging**: Pino logger with pretty print
- **HTTP Client**: Axios with NestJS integration

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 18+ (LTS recommended)
- **pnpm** package manager
  ```bash
  npm install -g pnpm
  ```
- **EdgeDB** 5.x
  ```bash
  # macOS
  brew install edgedb
  
  # Or install using the CLI
  curl --proto '=https' --tlsv1.2 -sSf https://sh.edgedb.com | sh
  ```
- **Neo4j** 5.x (optional for local development - can use Neo4j Aura cloud instance)
- **Git**

## 🚀 Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd crypto-wallet-tracker/cos30049-be
   ```

2. **Install dependencies**

   ```bash
   pnpm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root directory. See [Environment Variables](#environment-variables) section below.

## 🔐 Environment Variables

Create a `.env` file in the `cos30049-be` directory with the following configuration:

```properties
# ============================================
# Swagger API Documentation Configuration
# ============================================
SWAGGER_API_TITLE=Crypto Wallet Tracker API
SWAGGER_API_DESCRIPTION=API for cryptocurrency wallet tracking and analysis
SWAGGER_API_VERSION=1.0.0
SWAGGER_API_PREFIX=/docs

# ============================================
# Server Configuration
# ============================================
# Global API prefix for all routes (e.g., /api/users)
GLOBAL_API_PREFIX=/api

# Server port
PORT=4000

# ============================================
# JWT Authentication Configuration
# ============================================
# Secret key for signing access tokens (CHANGE IN PRODUCTION!)
# Generate a secure random string: openssl rand -base64 32
JWT_ACCESS_TOKEN_SECRET=your-super-secret-access-token-key-change-in-production

# Secret key for signing refresh tokens (CHANGE IN PRODUCTION!)
JWT_REFRESH_TOKEN_SECRET=your-super-secret-refresh-token-key-change-in-production

# Access token expiration time in milliseconds (1 hour = 3600000ms)
JWT_ACCESS_TOKEN_EXPIRATION_MS=3600000

# Refresh token expiration time in milliseconds (24 hours = 86400000ms)
JWT_REFRESH_TOKEN_EXPIRATION_MS=86400000

# ============================================
# Frontend Configuration
# ============================================
# Frontend URL for authentication redirects
AUTH_UI_REDIRECT_URL=http://localhost:3000/callback

# For production:
# AUTH_UI_REDIRECT_URL=https://cos30049-fe-six.vercel.app/callback

# ============================================
# Neo4j Graph Database Configuration
# ============================================
# Neo4j connection URI (use neo4j+s:// for secure connection to Aura)
NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io

# Neo4j username (default is 'neo4j')
NEO4J_USERNAME=neo4j

# Neo4j password (from Neo4j Aura or your local instance)
NEO4J_PASSWORD=your-neo4j-password

# Neo4j Aura instance details (if using Neo4j Aura)
AURA_INSTANCEID=your-instance-id
AURA_INSTANCENAME=your-instance-name

# ============================================
# EdgeDB Configuration (Auto-configured)
# ============================================
# EdgeDB credentials are managed by the EdgeDB CLI
# Run 'edgedb project init' to configure
```

### 🔒 Security Best Practices

1. **Never commit the `.env` file** to version control (already in `.gitignore`)
2. **Use strong, random secrets** for JWT tokens:
   ```bash
   # Generate secure random strings
   openssl rand -base64 32
   ```
3. **Change all default values** before deploying to production
4. **Use different secrets** for access and refresh tokens
5. **Keep Neo4j credentials secure** and rotate them regularly

### 📝 Example .env for Different Environments

**Local Development:**
```properties
PORT=4000
GLOBAL_API_PREFIX=/api
AUTH_UI_REDIRECT_URL=http://localhost:3000/callback
NEO4J_URI=neo4j://localhost:7687  # If running Neo4j locally
```

**Production:**
```properties
PORT=4000
GLOBAL_API_PREFIX=/api
AUTH_UI_REDIRECT_URL=https://cos30049-fe-six.vercel.app/callback
NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io
```

## 💾 Database Setup

### EdgeDB Setup

1. **Initialize EdgeDB project**

   ```bash
   edgedb project init
   ```

   This will:
   - Create a new EdgeDB instance
   - Link it to your project
   - Set up connection credentials

2. **Run database migrations**

   ```bash
   pnpm run db:migrate
   ```

   This command will:
   - Create new migrations if schema changed
   - Apply migrations to the database
   - Generate TypeScript interfaces

3. **Generate TypeScript types** (if not done by migrate)

   ```bash
   pnpm run db:generate
   ```

### Neo4j Setup

The project uses Neo4j Aura cloud instance. Credentials are in the `.env` file.

If you want to use a local Neo4j instance:

1. Install Neo4j Desktop or run via Docker:
   ```bash
   docker run -p 7474:7474 -p 7687:7687 -e NEO4J_AUTH=neo4j/your-password neo4j:5
   ```

2. Update `.env` with local credentials:
   ```properties
   NEO4J_URI=neo4j://localhost:7687
   NEO4J_USERNAME=neo4j
   NEO4J_PASSWORD=your-password
   ```

### Database Seeding

#### Option 1: Seed with Generated Data

```bash
pnpm run db:edgedb-seed
```

This will populate the database with:
- Sample users
- Cryptocurrencies
- Wallets
- Transactions
- Exchange rates

#### Option 2: Seed from CSV Files

```bash
pnpm run db:csv-seed
```

This will:
- Import data from CSV files in `src/common/seeder/csv-data/`
- Automatically seed Neo4j graph database

#### Seed Neo4j Only

```bash
pnpm run db:neo4j-seed
```

## 🏃 Running the Application

### Development Mode

Start the server with hot reload (recommended for development):

```bash
pnpm run dev
```

The server will start at `http://localhost:4000`

### Production Mode

Build and run the production version:

```bash
# Build the application
pnpm run build

# Start production server
pnpm run start
```

### Debug Mode

Run with debugging enabled:

```bash
pnpm run debug
```

Attach your debugger to the process (default port: 9229)

## 📖 API Documentation

### Swagger UI

Once the application is running, access the interactive API documentation:

- **Local**: [http://localhost:4000/docs](http://localhost:4000/docs)
- **Production**: [https://cos30049-be.onrender.com/docs](https://cos30049-be.onrender.com/docs)

The Swagger UI provides:
- Complete API endpoint documentation
- Request/response schemas
- Interactive API testing
- Authentication flow testing

### API Endpoints Overview

Main endpoint groups:

- **`/api/auth`** - Authentication (login, register, refresh token)
- **`/api/users`** - User management
- **`/api/wallets`** - Wallet operations
- **`/api/transactions`** - Transaction tracking
- **`/api/currencies`** - Cryptocurrency information
- **`/api/exchange-rates`** - Exchange rate data
- **`/api/neo4j`** - Graph database queries

## 📝 Available Scripts

```bash
# Development
pnpm run dev              # Start dev server with hot reload
pnpm run start            # Start production server
pnpm run build            # Build for production
pnpm run debug            # Start with debugging

# Database
pnpm run db:migrate       # Create and apply migrations + generate types
pnpm run db:generate      # Generate TypeScript interfaces from EdgeDB schema
pnpm run db:edgedb-seed   # Seed database with generated data
pnpm run db:csv-seed      # Seed from CSV files + Neo4j
pnpm run db:neo4j-seed    # Seed Neo4j graph database only

# Code Quality
pnpm run lint             # Lint code with ESLint
pnpm run format           # Format code with Prettier
```

## 📁 Project Structure

```
cos30049-be/
├── dbschema/                 # EdgeDB schema and migrations
│   ├── default.esdl          # Main schema definition
│   ├── interfaces.ts         # Generated TypeScript interfaces
│   ├── migrations/           # Database migrations
│   └── edgeql-js/            # Generated EdgeDB query builder
│
├── src/
│   ├── main.ts               # Application entry point
│   │
│   ├── common/               # Shared utilities
│   │   ├── decorators/       # Custom decorators (API response, etc.)
│   │   ├── interceptors/     # Response interceptors
│   │   ├── logger/           # Logging configuration
│   │   ├── pagination/       # Pagination utilities
│   │   └── seeder/           # Database seeding scripts
│   │       ├── csv-data/     # CSV data files
│   │       ├── *.seeder.ts   # Seeder implementations
│   │       └── seeder.ts     # Main seeder orchestrator
│   │
│   └── modules/              # Feature modules
│       ├── app.module.ts     # Root application module
│       │
│       ├── auth/             # Authentication module
│       │   ├── auth.controller.ts
│       │   ├── auth.service.ts
│       │   ├── auth.dto.ts
│       │   ├── guards/       # Auth guards
│       │   └── strategies/   # Passport strategies
│       │
│       ├── user/             # User management module
│       ├── wallet/           # Wallet operations module
│       ├── transaction/      # Transaction tracking module
│       ├── currency/         # Currency management module
│       ├── exchange-rate/    # Exchange rate module
│       ├── edgedb/           # EdgeDB integration module
│       └── neo4j/            # Neo4j integration module
│
├── docs/                     # Documentation
│   ├── architecture.md
│   ├── data-models.md
│   ├── api-documentation.md
│   └── data-model-documentation.md
│
├── .env                      # Environment variables (not in git)
├── .eslintrc.js              # ESLint configuration
├── .prettierrc               # Prettier configuration
├── edgedb.toml               # EdgeDB project configuration
├── nest-cli.json             # NestJS CLI configuration
├── package.json              # Dependencies and scripts
├── tsconfig.json             # TypeScript configuration
└── webpack-hmr.config.js     # Webpack HMR configuration
```

## 🐛 Common Issues

### EdgeDB Connection Error

**Problem**: Cannot connect to EdgeDB

**Solution**:
```bash
# Ensure EdgeDB is running
edgedb instance status

# Re-initialize project if needed
edgedb project init
```

### Database Migration Fails

**Problem**: Migration creation or application fails

**Solution**:
```bash
# Run migration in dev mode to see detailed errors
edgedb migration create --dev-mode

# Check schema syntax
edgedb migration status
```

### Hot Reload Not Working

**Problem**: Changes not reflected during development

**Solution**:
1. Check that `webpack-hmr.config.js` is properly configured
2. Ensure you're running with `pnpm run dev`
3. Try restarting the development server

### Neo4j Connection Error

**Problem**: Cannot connect to Neo4j

**Solution**:
1. Verify credentials in `.env` file
2. Check that Neo4j instance is running
3. Ensure URI format is correct (`neo4j+s://` for Aura, `neo4j://` for local)
4. Test connection in Neo4j Browser

### Port Already in Use

**Problem**: Port 4000 is already in use

**Solution**:
```bash
# Find and kill the process using port 4000
lsof -ti:4000 | xargs kill -9

# Or change the port in .env
PORT=4001
```

### Module Not Found Errors

**Problem**: TypeScript cannot find modules

**Solution**:
```bash
# Clear dependencies and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Regenerate EdgeDB types
pnpm run db:generate
```

### Seeding Fails

**Problem**: Database seeding throws errors

**Solution**:
1. Ensure database is empty or reset it
2. Check that all migrations are applied
3. Verify CSV files are in correct location
4. Run seeders individually to identify the issue

## 📚 Additional Documentation

- [Architecture Overview](docs/architecture.md) - System design and architecture patterns
- [Data Models](docs/data-models.md) - Database schema and relationships
- [API Documentation](docs/api-documentation.md) - Detailed API reference
- [Data Model Documentation](docs/data-model-documentation.md) - In-depth data model guide

## 🚀 Deployment

The backend is deployed on Render. To deploy your own instance:

1. Create a new Web Service on Render
2. Connect your GitHub repository
3. Configure settings:
   - **Root Directory**: `cos30049-be`
   - **Build Command**: `pnpm install && pnpm run build`
   - **Start Command**: `pnpm run start`
4. Add environment variables from `.env` file
5. Deploy

> **Note**: Render free tier spins down after inactivity. First request may take ~1 minute.

## 📄 License

This project is licensed under the MIT License.

---

**Built with ❤️ using NestJS, EdgeDB, and Neo4j**
