# Blossom: Full-Stack Web Application Platform

## Overview

Blossom is a comprehensive full-stack web application platform that provides reusable "boilerplate" code for building modern web applications. It separates concerns between **product** (end-user features) and **platform** (infrastructure and tooling), allowing developers to focus on solving business problems while leveraging a robust, battle-tested foundation.

## Architecture

### Backend: Python Monolith
- **Framework**: Quart (async Python web framework) with Hypercorn ASGI server
- **Database**: PostgreSQL with sqlc for type-safe queries
- **Authentication**: Session-based with multi-tenant support
- **Security**: Row Level Security (RLS) for secure multi-tenancy
- **API**: Custom RPC framework with automatic TypeScript codegen
- **Testing**: pytest with parallelized tests and shared database fixtures

### Frontend: React SPA
- **Framework**: React 18 with TypeScript
- **Build System**: Vite with SWC, managed by Turborepo
- **Styling**: vanilla-extract CSS-in-JS with design tokens
- **State Management**: Jotai for client state, Tanstack Query for server state
- **Routing**: Wouter with code splitting and prefetching
- **Testing**: Vitest for unit tests, Playwright for visual testing

### Infrastructure
- **Development**: Nix flakes for reproducible environments
- **Deployment**: Nomad for service orchestration
- **CI/CD**: GitHub Actions with Tailscale networking
- **Package Management**: pnpm for frontend, Nix for backend

## Key Components & How They Connect

### 1. RPC System - The Communication Bridge
The custom RPC framework (`backend/foundation/rpc/`) is the backbone that connects frontend and backend:

```python
# Backend route definition
@route(authorization="user", errors=[InvalidCredentialsError])
async def login(req: Req[LoginIn]) -> None:
    # Authentication logic
```

This automatically generates TypeScript types and client bindings for the frontend, ensuring type safety across the full stack.

### 2. Authentication & Authorization Flow
- **Session Management**: HTTP-only cookies with session IDs stored in PostgreSQL
- **Multi-tenant Architecture**: Users can belong to multiple tenants, sessions are tenant-scoped
- **Row Level Security**: Database-level security ensures users only see their tenant's data
- **Authorization Levels**: `public`, `user`, `tenant` - enforced at the route decorator level

### 3. Database Layer
- **Schema Management**: SQL migrations in `backend/migrations/`
- **Type Safety**: sqlc generates Python models from SQL queries
- **Connection Pooling**: Async connection pool with separate admin/customer connections
- **Testing**: Shared test database with parallel test execution

### 4. Frontend Architecture
The frontend is organized into foundation packages and product packages:

**Foundation Packages** (reusable platform code):
- `auth/`: Authentication state management
- `rpc/`: API client with Jotai and Tanstack Query bindings
- `ui/`: Design system components (Button, TextField, etc.)
- `theme/`: Design tokens and theming system
- `routing/`: Client-side routing with prefetching
- `forms/`: Form validation and state management
- `layout/`: Page layout primitives

**Product Packages** (application-specific):
- `app/`: Main application shell
- `home/`, `login/`, `notfound/`: Individual page components

### 5. Design System Integration
- **Figma Tokens**: Design tokens exported from Figma and transformed into CSS variables
- **Component Library**: Storybook-like stories with visual regression testing
- **Theming**: Light/dark mode support with CSS custom properties
- **Icons**: SVG icons converted to React components with tokenized colors

### 6. Development Workflow
1. **Environment Setup**: `nix develop` provides all tools (Python, Node.js, PostgreSQL, etc.)
2. **Code Generation**: Backend changes trigger TypeScript type generation
3. **Testing**: Unit tests, integration tests, and visual regression tests
4. **Linting**: Consistent code style with ESLint, ruff, and Semgrep
5. **CI/CD**: Automated testing, building, and deployment

## Data Flow Example

1. **User Login Request**:
   - Frontend form submission → RPC client → Backend route
   - Authentication logic → Database query → Session creation
   - Response → Frontend state update → Route redirect

2. **Authenticated Page Load**:
   - Route guard checks authentication state
   - RPC call with session cookie → Backend authorization
   - Database query with RLS → Filtered tenant data
   - Response → Frontend component rendering

## Key Features

### Security
- **Row Level Security**: Database-enforced tenant isolation
- **Input Validation**: Pydantic validation on backend, form validation on frontend
- **Authentication**: Secure session management with proper cookie handling
- **Authorization**: Route-level permissions with user/tenant scoping

### Developer Experience
- **Type Safety**: End-to-end type safety from database to UI
- **Hot Reloading**: Fast development feedback with Vite
- **Testing**: Comprehensive test coverage with parallel execution
- **Linting**: Consistent code quality enforcement
- **Documentation**: Component stories and visual regression testing

### Performance
- **Code Splitting**: Route-based code splitting with prefetching
- **Optimized Builds**: SWC compilation and bundle analysis
- **Caching**: Efficient state management and query caching
- **Database**: Connection pooling and optimized queries

## Package Structure

The monorepo is organized by service type:
- `backend/`: Python backend services
- `frontend/`: TypeScript frontend packages
- `nix/`: Development environment and build definitions
- `nomad/`: Deployment configurations

Each service follows a consistent package structure:
- `foundation/`: Platform/infrastructure packages
- `product/`: Application-specific packages
- `codegen/`: Generated code from tooling

This architecture provides a solid foundation for building scalable, maintainable web applications while maintaining clear separation between platform concerns and product features.