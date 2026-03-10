# COS30049 Crypto Wallet Tracker - Frontend

A modern, responsive, and user-friendly frontend application for cryptocurrency wallet tracking and blockchain transaction visualization. Built using Next.js with the App Router, providing server-side rendering capabilities, optimized client-side navigation, and a component-based architecture.

## 🌐 Live Deployment

**Application URL**: [https://cos30049-fe-six.vercel.app/](https://cos30049-fe-six.vercel.app/)

> ⚠️ **Note**: The backend may take ~1 minute to wake up from sleep on first request (hosted on Render's free tier).

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Available Scripts](#available-scripts)
- [Project Structure](#project-structure)
- [Key Features](#key-features)
- [Troubleshooting](#troubleshooting)
- [Deployment](#deployment)

## 🎯 Overview

The Crypto Wallet Tracker frontend is a comprehensive web application that enables users to track cryptocurrency wallets, visualize transaction flows, and analyze blockchain activities. It features interactive graphs, real-time data updates, and an intuitive user interface built with modern React practices.

## ✨ Features

- **Wallet Management**: Create, view, and manage blockchain wallets
- **Transaction Visualization**: Interactive graph-based transaction flow using React Flow
- **Real-time Analytics**: View wallet balances, transaction history, and trends
- **Transaction Tracking**: Detailed transaction information with filtering and sorting
- **Exchange Rate Monitoring**: Real-time cryptocurrency exchange rates
- **Responsive Design**: Fully optimized for desktop, tablet, and mobile devices
- **Server-Side Rendering**: Fast initial page loads with Next.js SSR
- **Interactive Charts**: Beautiful data visualizations using Recharts
- **Dark/Light Mode**: (If implemented) Adaptive theming support

## 🛠 Tech Stack

### Core Technologies
- **Framework**: Next.js 15 with App Router
- **UI Library**: React 19
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 3

### UI Components & Libraries
- **Component Library**: Radix UI (headless, accessible components)
- **UI Components**: shadcn/ui
- **Charts**: Recharts 2
- **Graph Visualization**: React Flow (@xyflow/react)
- **Tables**: TanStack Table 8
- **Carousel**: Embla Carousel
- **Icons**: Lucide React
- **Animations**: Framer Motion 12

### Blockchain & Data
- **Blockchain Interaction**: Viem 2 (TypeScript interface for Ethereum)
- **Date Handling**: date-fns 4
- **Error Handling**: React Error Boundary

### Development Tools
- **Type Generation**: openapi-typescript
- **Code Quality**: ESLint with Next.js config
- **Package Manager**: pnpm

## 🚀 Getting Started

### Prerequisites

- **Node.js** 18+ (LTS version recommended)
  ```bash
  node --version  # Should be v18 or higher
  ```
- **pnpm** package manager
  ```bash
  npm install -g pnpm
  ```
- **Git**

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd crypto-wallet-tracker/cos30049-fe
   ```

2. **Install dependencies**

   ```bash
   pnpm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root directory:

   ```bash
   # Create .env file
   touch .env
   ```

   Add the following content (see [Environment Variables](#environment-variables) section for details):

   ```properties
   NEXT_PUBLIC_API_URL=http://localhost:4000/api
   ```

4. **Start the development server**

   ```bash
   pnpm run dev
   ```

5. **Open the application**

   Navigate to [http://localhost:3000](http://localhost:3000) in your browser

## 🔐 Environment Variables

Create a `.env` file in the `cos30049-fe` directory:

### Local Development

```properties
# Backend API URL for local development
NEXT_PUBLIC_API_URL=http://localhost:4000/api
```

### Production

```properties
# Backend API URL for production (Render deployment)
NEXT_PUBLIC_API_URL=https://cos30049-be.onrender.com/api
```

### Environment Variable Explanation

- **`NEXT_PUBLIC_API_URL`**: The base URL for the backend API
  - **Prefix `NEXT_PUBLIC_`**: Exposes the variable to the browser (required for client-side API calls)
  - **Local**: Points to your local backend server
  - **Production**: Points to the deployed backend on Render

### Security Notes

1. **Never commit `.env` file** to version control (already in `.gitignore`)
2. **Use different URLs** for development and production
3. **Verify API URL** before building for production
4. Only `NEXT_PUBLIC_*` variables are exposed to the browser

## 📝 Available Scripts

```bash
# Development
pnpm run dev          # Start development server (http://localhost:3000)
                      # - Hot module replacement enabled
                      # - Fast refresh for instant updates

# Production
pnpm run build        # Build optimized production bundle
                      # - Generates static and server-rendered pages
                      # - Optimizes images and assets
                      # - Type-checks and lints code

pnpm run start        # Start production server
                      # - Serves the built application
                      # - Requires 'pnpm run build' first

# Code Quality
pnpm run lint         # Run ESLint to check code quality
                      # - Checks for code style issues
                      # - Validates TypeScript types
                      # - Enforces Next.js best practices

# Type Generation
pnpm run typegen      # Generate TypeScript types from OpenAPI schema
                      # - Fetches API schema from backend
                      # - Generates type-safe API client types
                      # - Ensures frontend/backend type consistency
```

### Development Workflow

```bash
# 1. Start development server
pnpm run dev

# 2. Make changes to code
# ... edit files ...

# 3. Check code quality
pnpm run lint

# 4. Generate types (when API changes)
pnpm run typegen

# 5. Build for production
pnpm run build

# 6. Test production build locally
pnpm run start
```

## 📁 Project Structure

```
cos30049-fe/
├── src/
│   ├── app/                      # Next.js App Router
│   │   ├── layout.tsx            # Root layout (global styles, fonts)
│   │   ├── page.tsx              # Homepage
│   │   ├── loading.tsx           # Global loading UI
│   │   ├── globals.css           # Global styles and Tailwind imports
│   │   │
│   │   ├── _components/          # Homepage components
│   │   │   ├── landing-page.tsx
│   │   │   ├── section-hero.tsx
│   │   │   ├── section-features.tsx
│   │   │   ├── mock-*.tsx        # Mock charts and visualizations
│   │   │   └── ...
│   │   │
│   │   ├── _api-types/           # Generated API types
│   │   │   ├── transactions.ts
│   │   │   └── wallets.ts
│   │   │
│   │   ├── wallets/              # Wallets feature
│   │   │   ├── page.tsx          # Wallet list page
│   │   │   ├── loading.tsx       # Loading state
│   │   │   ├── _components/      # Wallet-specific components
│   │   │   └── [address]/        # Dynamic wallet detail pages
│   │   │       ├── page.tsx
│   │   │       └── _components/
│   │   │
│   │   └── news/                 # News feature
│   │       └── page.tsx
│   │
│   ├── components/               # Reusable UI components
│   │   ├── ui/                   # shadcn/ui components
│   │   │   ├── button.tsx
│   │   │   ├── card.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── table.tsx
│   │   │   └── ...               # Other UI primitives
│   │   │
│   │   ├── base-node.tsx         # React Flow node component
│   │   ├── tooltip-node.tsx      # Graph tooltip
│   │   ├── zoom-slider.tsx       # Zoom controls
│   │   └── loading-circle.tsx    # Loading indicator
│   │
│   ├── actions/                  # Server actions
│   │   ├── action.const.ts       # Action constants
│   │   ├── action.type.ts        # Action types
│   │   └── wallet/
│   │       └── search-wallet.ts  # Wallet search action
│   │
│   └── lib/                      # Utilities and helpers
│       ├── utils.ts              # Utility functions (cn, etc.)
│       ├── types.ts              # Shared TypeScript types
│       └── typegen.ts            # API type generation script
│
├── public/                       # Static assets
│   ├── images/                   # Images
│   │   ├── homepage/             # Homepage images
│   │   └── news/                 # News images
│   ├── fonts/                    # Custom fonts
│   │   ├── Figtree/
│   │   └── Poppins/
│   └── *.svg                     # SVG icons
│
├── docs/                         # Documentation
│   ├── architecture-documentation.md
│   └── technical-documentation.md
│
├── .env                          # Environment variables (not in git)
├── .eslintrc.json                # ESLint configuration
├── .gitignore                    # Git ignore rules
├── components.json               # shadcn/ui configuration
├── next.config.ts                # Next.js configuration
├── package.json                  # Dependencies and scripts
├── postcss.config.mjs            # PostCSS configuration
├── tailwind.config.ts            # Tailwind CSS configuration
└── tsconfig.json                 # TypeScript configuration
```

### Directory Conventions

- **`app/`**: Next.js App Router pages and layouts
  - Files starting with `_` are not routes (components, utilities)
  - `[param]` folders are dynamic routes
- **`components/`**: Reusable components across the app
- **`actions/`**: Server-side actions for data fetching
- **`lib/`**: Utility functions and shared code
- **`public/`**: Static files served from root URL

## 🎨 Key Features

### 1. Wallet Tracking
- **Search Functionality**: Search for wallets by address
- **Wallet Details**: View comprehensive wallet information
- **Balance Overview**: See current balances across multiple cryptocurrencies
- **Transaction History**: Complete transaction history with filtering

### 2. Transaction Visualization
- **Interactive Graph**: React Flow-based transaction flow visualization
- **Node-based UI**: Drag and zoom through transaction networks
- **Relationship Mapping**: Visual representation of wallet connections
- **Custom Nodes**: Beautiful, interactive node designs with tooltips

### 3. Analytics & Charts
- **Trading Volume**: Visualize trading volumes over time
- **Expenditure Tracking**: Monitor spending patterns
- **Exchange Rates**: Real-time currency conversion rates
- **Interactive Charts**: Hover for detailed information

### 4. User Experience
- **Fast Loading**: Server-side rendering for optimal performance
- **Responsive Design**: Works seamlessly on all devices
- **Loading States**: Skeleton loaders and loading indicators
- **Error Handling**: Graceful error boundaries and user feedback
- **Smooth Animations**: Framer Motion animations for polish

## � Troubleshooting

### Common Issues

#### 1. Blank Screen or White Page

**Problem**: Application shows a blank screen

**Solutions**:
- Clear browser cache and hard reload (Ctrl+F5 or Cmd+Shift+R)
- Check browser console for errors (F12 → Console tab)
- Ensure backend is running and accessible
- Verify `NEXT_PUBLIC_API_URL` in `.env` is correct

#### 2. Slow Loading or Timeout Errors

**Problem**: Pages take a long time to load or show timeout errors

**Solutions**:
- Wait ~1 minute for backend to wake up (Render free tier limitation)
- Check backend status at: https://cos30049-be.onrender.com/docs
- Verify internet connection
- Try refreshing the page after waiting

#### 3. API Connection Errors

**Problem**: "Failed to fetch" or network errors

**Solutions**:
```bash
# Check .env file exists and has correct URL
cat .env

# Should show:
# NEXT_PUBLIC_API_URL=http://localhost:4000/api (for local)
# OR
# NEXT_PUBLIC_API_URL=https://cos30049-be.onrender.com/api (for production)

# If wrong, update .env and restart dev server
pnpm run dev
```

#### 4. Type Errors During Development

**Problem**: TypeScript shows type errors for API responses

**Solutions**:
```bash
# Regenerate types from latest API schema
pnpm run typegen

# If backend is not running, start it first
cd ../cos30049-be
pnpm run dev
```

#### 5. Build Fails

**Problem**: `pnpm run build` fails with errors

**Solutions**:
```bash
# Clear Next.js cache
rm -rf .next

# Clear node_modules and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Try building again
pnpm run build
```

#### 6. Module Not Found Errors

**Problem**: Import errors or "Cannot find module"

**Solutions**:
```bash
# Clear and reinstall dependencies
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Check TypeScript paths in tsconfig.json
```

#### 7. Styling Issues

**Problem**: Styles not applying or Tailwind classes not working

**Solutions**:
```bash
# Check that Tailwind CSS is running
# Restart dev server
pnpm run dev

# If in production, rebuild
pnpm run build
```

### Getting Help

If you encounter issues not listed here:

1. Check the browser console for error messages
2. Review the [Technical Documentation](docs/technical-documentation.md)
3. Verify all prerequisites are installed
4. Ensure backend is running and accessible
5. Try the troubleshooting steps in order

## 🚀 Deployment

The frontend is deployed on Vercel at: [https://cos30049-fe-six.vercel.app/](https://cos30049-fe-six.vercel.app/)

### Deploy Your Own Instance

#### Using Vercel (Recommended)

1. **Push to GitHub**
   ```bash
   git push origin main
   ```

2. **Import to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Configure project:
     - **Framework Preset**: Next.js
     - **Root Directory**: `cos30049-fe`
     - **Build Command**: `pnpm run build` (auto-detected)
     - **Output Directory**: `.next` (auto-detected)

3. **Add Environment Variables**
   - Go to Project Settings → Environment Variables
   - Add: `NEXT_PUBLIC_API_URL` = `https://cos30049-be.onrender.com/api`
   - Apply to: Production, Preview, Development

4. **Deploy**
   - Click "Deploy"
   - Wait for build to complete
   - Your app will be live at `https://your-project.vercel.app`

#### Using Other Platforms

**Build the application:**
```bash
pnpm run build
```

**Start the production server:**
```bash
pnpm run start
```

The application will run on the port specified in your environment (default: 3000).

### Environment Variables for Deployment

**Production:**
```properties
NEXT_PUBLIC_API_URL=https://cos30049-be.onrender.com/api
```

**Staging:**
```properties
NEXT_PUBLIC_API_URL=https://your-staging-backend.com/api
```

## 📚 Additional Documentation

- [Architecture Documentation](docs/architecture-documentation.md) - System architecture and design patterns
- [Technical Documentation](docs/technical-documentation.md) - In-depth technical details and implementation
- [API Documentation](https://cos30049-be.onrender.com/docs) - Backend API reference

## 🔧 Development Best Practices

### Code Style

- Follow TypeScript best practices
- Use functional components with hooks
- Implement proper error boundaries
- Add loading states for async operations
- Use semantic HTML elements

### Component Guidelines

```typescript
// Use TypeScript interfaces for props
interface ComponentProps {
  title: string;
  onAction: () => void;
}

// Functional component with proper typing
export function Component({ title, onAction }: ComponentProps) {
  return (
    <div>
      <h1>{title}</h1>
      <button onClick={onAction}>Action</button>
    </div>
  );
}
```

### State Management

- Use React hooks (useState, useEffect, etc.)
- Implement server actions for data fetching
- Keep state close to where it's used
- Use context for global state when needed

### Performance

- Use Next.js Image component for images
- Implement code splitting with dynamic imports
- Lazy load components when appropriate
- Optimize bundle size

## 📦 Technologies Used

### Core
- [Next.js 15](https://nextjs.org/) - React framework with App Router
- [React 19](https://react.dev/) - UI library
- [TypeScript](https://www.typescriptlang.org/) - Type-safe JavaScript
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework

### UI & Visualization
- [Radix UI](https://www.radix-ui.com/) - Unstyled, accessible components
- [shadcn/ui](https://ui.shadcn.com/) - Re-usable components
- [Recharts](https://recharts.org/) - Composable charting library
- [React Flow](https://reactflow.dev/) - Library for node-based UIs
- [Framer Motion](https://www.framer.com/motion/) - Animation library

### Data & Tables
- [TanStack Table](https://tanstack.com/table/latest) - Headless UI for tables
- [Embla Carousel](https://www.embla-carousel.com/) - Lightweight carousel

### Blockchain
- [Viem](https://viem.sh/) - TypeScript interface for Ethereum

### Icons & Assets
- [Lucide React](https://lucide.dev/) - Beautiful, consistent icons
