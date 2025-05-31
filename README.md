# A-Team Digital Platform

## Overview
This monorepo contains the digital platform for A-Team companies, starting with A-Team Excavation (a-team-x.com) and expanding to include SpringsRooter.com and A-Team Concrete in the future. The platform is designed to share core functionality while maintaining separate brand identities and content.

## Project Structure
```
.
├── README.md
├── DesignDocs.md              # Design documentation and guidelines
├── .cursor/                   # Cursor IDE settings and chat history
├── packages/                  # Shared packages
│   ├── core/                 # Core functionality and types
│   ├── ui/                   # Shared UI components
│   └── utils/                # Shared utilities
├── apps/                     # Individual applications
│   ├── a-team-excavation/    # A-Team Excavation website
│   ├── springs-rooter/       # SpringsRooter website (future)
│   └── a-team-concrete/      # A-Team Concrete website (future)
├── services/                 # Backend services
│   ├── cms/                 # Content Management System
│   ├── auth/                # Authentication service
│   └── api/                 # API Gateway
└── infrastructure/          # Infrastructure as code and configs
```

## System Architecture
```mermaid
graph TB
    subgraph Frontend
        A1[A-Team Excavation]
        A2[SpringsRooter]
        A3[A-Team Concrete]
    end

    subgraph Backend
        B1[API Gateway]
        B2[CMS Service]
        B3[Auth Service]
        B4[File Storage]
        B5[Database]
    end

    subgraph Shared
        S1[Core Package]
        S2[UI Components]
        S3[Utils]
    end

    A1 & A2 & A3 --> S1 & S2 & S3
    A1 & A2 & A3 --> B1
    B1 --> B2 & B3 & B4 & B5
```

## Technical Stack
### Backend
- **CMS**: Payload CMS (TypeScript-based)
- **API**: Node.js/TypeScript or .NET Core (TBD)
- **Database**: PostgreSQL
- **File Storage**: TBD (AWS S3 or similar)
- **Testing**: Jest for Node.js, xUnit for .NET

### Infrastructure
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Hosting**: TBD (AWS, Azure, or similar)
- **Monitoring**: TBD

## Development Guidelines
1. **TypeScript First**: All new code must be written in TypeScript
2. **Testing Requirements**:
   - Unit tests for all business logic
   - Integration tests for API endpoints
   - E2E tests for critical user flows
   - Minimum 80% test coverage for core packages
3. **Code Quality**:
   - ESLint + Prettier for code formatting
   - Husky for pre-commit hooks
   - Conventional Commits for version control
4. **Documentation**:
   - JSDoc for all public APIs
   - Storybook for UI components
   - API documentation with OpenAPI/Swagger

## Important Decisions & Discussions
### [Date: 2024-03-19]
- **Topic**: Monorepo Structure and Multi-Site Strategy
- **Decision**: Implement as a monorepo with shared packages and services
- **Rationale**: 
  - Code reuse across multiple sites
  - Consistent development experience
  - Simplified dependency management
  - Shared infrastructure and services
- **Key Considerations**:
  - Modular architecture for independent scaling
  - Shared authentication and user management
  - Common CMS for all sites
  - Separate content and branding per site
  - TypeScript for type safety and better developer experience

## Development Notes
- Current site: a-team-x.com (WordPress on DreamHost)
- Need to analyze current site structure and content before finalizing stack
- Consider migration strategy from WordPress to new platform
- Budget and hosting requirements to be determined
- Initial focus on A-Team Excavation, with architecture supporting future sites

## Getting Started
[To be added after stack finalization]

## Contributing
[To be added]

## License
[To be added]

## Development Workflow
### Branch Strategy
- `main` branch: Production-ready code
- `develop` branch: Development and testing
- Feature branches: Created from `develop` for new features/fixes

### CI/CD Pipeline
1. **Development Flow**:
   - Work happens on `develop` branch
   - CI runs on every push and PR
   - Tests and builds must pass
   - Environment: ATX_Dev

2. **Production Flow**:
   - Code moves to `main` via PR
   - Stricter checks on `main`
   - Environment: ATX_Deploy

### Testing the Workflow
1. **Local Development**:
   ```bash
   # Create feature branch
   git checkout -b feature/test-workflow
   
   # Make changes
   # Test locally
   # Commit changes
   git add .
   git commit -m "test: workflow testing"
   
   # Push to remote
   git push origin feature/test-workflow
   ```

2. **CI Checks**:
   - Linting
   - Testing
   - Building
   - Environment-specific rules

3. **Deployment**:
   - Develop branch: Development environment
   - Main branch: Production environment 

## Onboarding & Setup Instructions

### 1. Prerequisites
- **Node.js**: v20 or higher (includes Corepack by default)
- **Git**: for version control

### 2. Clone the Repository
```bash
git clone https://github.com/JLO-Creative-Studio/A_Team.git
cd A_Team
```

### 3. Enable Corepack (Yarn 4+)
Corepack is included with Node.js 16.9+ and is required for Yarn 4+ monorepos.
```bash
corepack enable
```

### 4. Install Dependencies
Run this from the project root:
```bash
yarn install
```
This will:
- Install all dependencies for the monorepo and workspaces
- Generate a `yarn.lock` file (if not present)
- Set up the `.yarn/` directory for Yarn 4 config

### 5. Commit Lockfile and Yarn Config
Always commit `yarn.lock` and the `.yarn/` directory to version control:
```bash
git add yarn.lock .yarn
```

### 6. Running Scripts
- **Development:**
  ```bash
  yarn dev
  ```
- **Build:**
  ```bash
  yarn build
  ```
- **Lint:**
  ```bash
  yarn lint
  ```
- **Test:**
  ```bash
  yarn test
  ```

### 7. CI/CD
- All pushes and PRs to `develop` and `main` branches trigger the CI workflow
- The workflow requires a valid `yarn.lock` and `.yarn` config
- See the "Development Workflow" section below for more details 