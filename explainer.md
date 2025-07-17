# Blossom: A World-Class Web Application Foundation

## What is Blossom?

Blossom is a **full-stack web application platform** that provides everything you need to build professional, scalable web applications. Think of it as the foundation upon which you can build your business - all the hard infrastructure problems are already solved.

## Why is This Different?

Most web applications are built like this:
```
Start simple → Add features → Everything breaks → Rewrite everything
```

Blossom is built like this:
```
Start with professional foundation → Add features → Everything still works → Scale to millions of users
```

## The Core Philosophy

### **Platform vs Product**
- **Platform** = The foundation (authentication, database, security, deployment)
- **Product** = Your unique business logic (what makes your app special)

Blossom provides the **platform** so you can focus on the **product**.

### **Built for Growth**
Every decision in this codebase assumes you'll eventually have:
- Thousands of users
- Hundreds of companies using your app
- A team of developers working together
- Enterprise security requirements

## Key Features That Make This Exceptional

### 1. **Multi-Tenant Architecture**
```
One codebase → Serves many companies → Each company's data is completely isolated
```

**Why this matters:** You can serve thousands of companies from one application without them ever seeing each other's data.

**How it works:** Database-level security (Row Level Security) automatically filters data based on which company the user belongs to.

### 2. **Type Safety Across the Full Stack**
```
Database Schema → Python Types → TypeScript Types → UI Components
```

**Why this matters:** When you change the database, the frontend automatically knows about it. Entire categories of bugs simply cannot happen.

**How it works:** Custom RPC system generates TypeScript types from Python functions automatically.

### 3. **Enterprise-Grade Security**
- **Row Level Security**: Database automatically prevents data leaks
- **Session-based Authentication**: More secure than JWT tokens
- **Encrypted Storage**: Sensitive data is encrypted at rest
- **Audit Trails**: Track who did what and when

### 4. **Developer Experience**
- **One Command Setup**: `nix develop` gives you entire development environment
- **Hot Reloading**: See changes instantly
- **Automated Testing**: Catch bugs before they reach production
- **Visual Testing**: Automatically detect UI regressions
- **Code Generation**: Keep frontend/backend in sync automatically

### 5. **Production-Ready Infrastructure**
- **Container Orchestration**: Nomad for deployment
- **Database Migrations**: Version-controlled schema changes
- **Connection Pooling**: Optimized database performance
- **Code Splitting**: Fast frontend loading
- **CI/CD Pipeline**: Automated testing and deployment

## Architecture Overview

### Backend (Python)
```
foundation/
├── rpc/           # API framework with type generation
├── database/      # Connection pooling, migrations
├── auth/          # Authentication system
├── vault/         # Encrypted storage
└── testing/       # Test utilities

product/
├── authn/         # Login/logout functionality
├── users/         # User management
└── tenants/       # Company management
```

### Frontend (TypeScript/React)
```
foundation/
├── rpc/           # Type-safe API client
├── ui/            # Design system components
├── theme/         # Design tokens and theming
├── routing/       # Client-side routing
├── forms/         # Form handling
└── auth/          # Authentication state

product/
├── app/           # Main application shell
├── login/         # Login page
├── home/          # Dashboard
└── notfound/      # 404 page
```

## How It All Connects

### 1. **User Authentication Flow**
```
User enters credentials → Backend validates → Creates session → Frontend gets user data
```

### 2. **Multi-Tenant Data Access**
```
User logs in → Session tied to specific company → Database filters all queries automatically
```

### 3. **Type-Safe API Calls**
```
Python function → RPC system → TypeScript types → Frontend components
```

### 4. **Development Workflow**
```
Write code → Tests run automatically → Types generated → Deploy with confidence
```

## Real-World Benefits

### **For Startups**
- **Faster time to market**: Skip infrastructure, focus on business logic
- **Professional quality**: Built with enterprise patterns from day one
- **Investor confidence**: Shows technical sophistication

### **For Growing Companies**
- **Scales automatically**: Multi-tenant architecture handles growth
- **Team productivity**: Clear boundaries let developers work independently
- **Lower maintenance**: Well-organized code is easier to maintain

### **For Enterprises**
- **Security compliance**: Row Level Security, audit trails, encryption
- **Performance**: Optimized for scale from day one
- **Reliability**: Battle-tested patterns and comprehensive testing

## What Problems Does This Solve?

### **The "Rewrite Problem"**
Most apps need complete rewrites when they grow. This architecture scales from 1 to 1,000,000 users without fundamental changes.

### **The "Integration Problem"**
Frontend and backend stay in sync automatically. No more "it works on my machine" issues.

### **The "Security Problem"**
Multi-tenant security is built into the database itself. Data leaks are nearly impossible.

### **The "Team Problem"**
Clear package boundaries mean developers can work independently without conflicts.

### **The "Maintenance Problem"**
Code is organized so clearly that new team members can understand it immediately.

## Technologies Used

### **Backend**
- **Python**: Primary language
- **Quart**: Async web framework
- **PostgreSQL**: Database with advanced features
- **sqlc**: Type-safe database queries
- **Pydantic**: Data validation

### **Frontend**
- **TypeScript**: Type-safe JavaScript
- **React**: UI framework
- **Vite**: Fast build tool
- **vanilla-extract**: CSS-in-JS
- **Jotai**: State management

### **Infrastructure**
- **Nix**: Reproducible development environments
- **Nomad**: Container orchestration
- **GitHub Actions**: CI/CD pipeline
- **Tailscale**: Secure networking

## Getting Started

### **Prerequisites**
1. Install Nix (package manager)
2. Enable Nix Flakes
3. Install direnv
4. Run `direnv allow` in project root

### **Development**
```bash
# Start development environment
nix develop

# Start backend
cd backend && make dev

# Start frontend
cd frontend && pnpm dev

# Run tests
make test
```

### **Key Commands**
```bash
# Backend
make dev        # Start development server
make test       # Run tests
make codegen    # Generate TypeScript types

# Frontend
pnpm dev        # Start development server
pnpm test       # Run tests
pnpm lint       # Check code quality
pnpm storybook  # View component stories
```

## Code Quality Features

### **Automated Testing**
- **Unit tests**: Test individual functions
- **Integration tests**: Test API endpoints
- **Visual tests**: Catch UI regressions
- **Parallel execution**: Fast feedback

### **Code Standards**
- **ESLint**: Consistent code style
- **TypeScript**: Type safety
- **Prettier**: Automatic formatting
- **Semgrep**: Security scanning

### **Documentation**
- **Type annotations**: Code documents itself
- **Component stories**: Interactive documentation
- **README files**: Context for each package

## Deployment

### **Local Development**
- Docker Compose for database
- Hot reloading for both frontend and backend
- Shared test database for fast testing

### **Production**
- Nomad for container orchestration
- GitHub Actions for CI/CD
- Tailscale for secure networking
- Automated health checks and rollbacks

## When to Use This

### **Perfect For:**
- **B2B SaaS applications**
- **Multi-tenant systems**
- **Applications requiring strong security**
- **Teams of 2+ developers**
- **Long-term projects (2+ years)**

### **Might Be Overkill For:**
- **Simple landing pages**
- **Single-user applications**
- **Prototypes or proof-of-concepts**
- **Projects with < 6 month timeline**

## Learning Path

### **For Beginners**
1. Understand the folder structure
2. Follow a simple feature from backend to frontend
3. Make small changes and see how types update
4. Learn about multi-tenancy concepts

### **For Experienced Developers**
1. Study the RPC system
2. Understand Row Level Security implementation
3. Explore the build and deployment pipeline
4. Learn about the testing strategies

## Support and Community

### **Getting Help**
- Read package README files
- Examine test files for usage examples
- Study the component stories
- Look at database migrations for schema evolution

### **Contributing**
- Follow existing code patterns
- Add tests for new features
- Update TypeScript types
- Document new packages

## Conclusion

Blossom represents **years of experience** building production web applications, distilled into a reusable foundation. It's the kind of codebase that successful companies are built on - professional, scalable, and maintainable.

Whether you're building the next unicorn startup or modernizing enterprise software, Blossom provides the foundation you need to focus on what makes your application unique, rather than solving infrastructure problems that have already been solved.

**This is how professional software is built.**