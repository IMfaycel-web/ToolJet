# ToolJet

ToolJet is an open-source low-code platform for building and deploying internal tools, dashboards, business applications, and operational workflows.

It provides a visual application builder, reusable UI components, database and API integrations, a built-in database, collaborative editing, workflow execution, custom plugins, and support for JavaScript and Python logic.

## Overview

ToolJet enables teams to build internal applications by connecting user interfaces to existing data sources and services without creating a complete frontend and backend from scratch.

Applications can combine visual components, queries, transformations, events, permissions, and workflows in a single workspace.

The platform is suitable for:

- Internal administration panels
- Operations dashboards
- Customer-support tools
- CRUD applications
- Approval workflows
- Inventory interfaces
- Reporting dashboards
- Database management tools
- API-driven business applications
- Team productivity tools

## Features

### Visual Application Builder

- Drag-and-drop application development
- More than 60 responsive UI components
- Multi-page applications
- Tables, forms, lists, charts, buttons, modals, and navigation components
- Component properties and event handlers
- Responsive layouts
- Reusable application logic
- JavaScript expressions
- Python execution support
- Application preview and publishing

### Data Sources

ToolJet can connect applications to databases, APIs, storage systems, and SaaS platforms.

Supported integration categories include:

- PostgreSQL
- MySQL
- Microsoft SQL Server
- MongoDB
- Redis
- Elasticsearch
- REST APIs
- GraphQL APIs
- Google Sheets
- Amazon S3
- Cloud storage
- CRM platforms
- Analytics systems
- Messaging services
- Business SaaS applications

The plugin system provides the foundation for additional connectors and data-source extensions.

### ToolJet Database

ToolJet includes a built-in database experience for application data.

Capabilities include:

- Table creation
- Column configuration
- Record creation and updates
- Query operations
- Application integration
- PostgREST-backed access
- Database reconfiguration support
- Configurable statement timeouts

### Queries and Logic

Applications can execute:

- Database queries
- REST requests
- GraphQL operations
- JavaScript
- Python
- Plugin-defined operations
- Data transformations

Query results can be bound directly to components and used in application events.

### Workflows

ToolJet supports server-side workflow execution for automated business processes.

Workflow capabilities include:

- Multi-step execution
- Scheduled processing
- Background job handling
- BullMQ queues
- Redis-backed execution
- Workflow monitoring
- JavaScript and Python logic
- Data-source operations

Worker mode can be enabled independently for deployments that separate web traffic from background execution.

### Collaboration

- Multi-user workspaces
- Multiplayer application editing
- Inline comments
- Mentions
- Application sharing
- Workspace-level access controls
- User session management
- Configurable signup behavior

### Security

- Encrypted data-source credentials
- Configurable session expiry
- Authentication controls
- Google OAuth support
- Git-based OAuth configuration
- Single sign-on configuration
- CORS controls
- Private and public application embedding controls
- Optional administrative API authentication
- Request throttling
- Security headers
- Audit-oriented server logging

### Extensibility

- TypeScript plugin framework
- Custom data-source connectors
- ToolJet CLI support
- Client and server plugin entry points
- Plugin installation and reload workflows
- Custom operations
- Marketplace-oriented integrations

## Tech Stack

| Area | Technologies |
| --- | --- |
| Runtime | Node.js 22.15.1 |
| Package manager | npm 10.9.2 |
| Language | TypeScript, JavaScript |
| Frontend | React 18 |
| Routing | React Router 6 |
| Frontend build | Webpack 5 |
| Styling | Sass, PostCSS, Tailwind CSS |
| Backend | NestJS 11 |
| HTTP platform | Express |
| ORM | TypeORM |
| Primary database | PostgreSQL 13 |
| Built-in database API | PostgREST 12 |
| Cache and queues | Redis 7 |
| Background processing | BullMQ |
| Scheduling | NestJS Schedule |
| Authentication | JWT, Passport, OAuth, SAML, LDAP |
| Authorization | CASL |
| Real-time communication | NestJS WebSockets |
| Observability | OpenTelemetry, Sentry, Prometheus |
| Backend testing | Jest |
| Frontend testing | Jest |
| End-to-end testing | Cypress |
| Component development | Storybook |
| Quality tooling | ESLint, Prettier, TypeScript |
| Deployment | Docker, Docker Compose, Kubernetes-compatible containers |

## Installation

Docker Compose is the recommended way to run the complete development stack.

### Requirements

- Git
- Docker Engine or Docker Desktop
- Docker Compose
- Node.js 22.15.1 for direct source development
- npm 10.9.2 for direct source development

### Create Environment Files

Copy the example configuration:

```bash
cp .env.example .env
```

The test environment expects a separate file:

```bash
cp .env.example .env.test
```

Replace all placeholder database credentials and application secrets before starting the services.

### Minimum Local Configuration

A development `.env` should define values for the application host, PostgreSQL database, credential encryption, and application signing.

```env
TOOLJET_EDITION=ce
TOOLJET_HOST=local_application_origin

LOCKBOX_MASTER_KEY=replace_with_64_character_secret
SECRET_KEY_BASE=replace_with_secure_secret

PG_DB=tooljet
PG_USER=tooljet
PG_HOST=postgres
PG_PASS=replace_with_database_password

REDIS_HOST=redis
REDIS_PORT=6379
```

For Docker Compose, `PG_HOST` should use the PostgreSQL service name and `REDIS_HOST` should use the Redis service name.

Do not use example encryption keys or secrets in a deployed environment.

### Start the Development Stack

```bash
docker compose up -d
```

The development stack includes:

- ToolJet frontend
- ToolJet backend
- PostgreSQL
- Redis
- PostgREST

Default development ports:

```text
Frontend:  8082
Backend:   3000
PostgREST: 3001
```

### View Service Status

```bash
docker compose ps
```

### View Logs

```bash
docker compose logs -f
```

View backend logs only:

```bash
docker compose logs -f server
```

### Stop the Stack

```bash
docker compose down
```

Persistent PostgreSQL and Redis data remain in Docker volumes unless those volumes are explicitly removed.

## Development from Source

### Install Root Dependencies

```bash
npm install
```

### Install Plugin Dependencies

```bash
npm run install:plugins
```

### Install Frontend Dependencies

```bash
npm --prefix frontend install
```

### Install Backend Dependencies

```bash
npm --prefix server install
```

### Prepare the Database

Create and migrate the application database:

```bash
npm run db:setup
```

Run only migrations:

```bash
npm run db:migrate
```

Seed development data when required:

```bash
npm run db:seed
```

Reset the development database:

```bash
npm run db:reset
```

### Start the Frontend

```bash
npm --prefix frontend start
```

The Webpack development server runs on port `8082`.

### Start the Backend

```bash
npm --prefix server run start:dev
```

### Start a Workflow Worker

```bash
npm --prefix server run worker:dev
```

## Usage

### Create an Application

1. Sign in to a workspace.
2. Create a new application.
3. Add components to the application canvas.
4. Configure component properties.
5. Create a data source.
6. Add database, API, or plugin queries.
7. Bind query results to components.
8. Configure component events.
9. Preview the application.
10. Publish it when the workflow is ready.

### Bind Query Data

Components can consume query results through ToolJet expressions.

```text
query_name.data
```

Expressions can also reference component values, variables, transformations, and query state.

### Execute Custom Logic

Application logic can use JavaScript for transformations and event-driven behavior.

Server-side workflows can also use JavaScript or Python execution where enabled.

### Build a Workflow

1. Create a workflow.
2. Add trigger and processing nodes.
3. Connect data-source operations.
4. Add JavaScript or Python logic.
5. Configure error handling.
6. Test the workflow.
7. Enable scheduling or external invocation as required.
8. Run dedicated workers for production workflow processing.

## Configuration

ToolJet reads runtime settings primarily from environment variables.

### Application and Security

| Variable | Purpose |
| --- | --- |
| `TOOLJET_EDITION` | Selects Community or Enterprise edition behavior |
| `TOOLJET_HOST` | Public application origin |
| `SERVER_HOST` | Backend hostname |
| `LOCKBOX_MASTER_KEY` | Encrypts stored data-source credentials |
| `SECRET_KEY_BASE` | Application signing secret |
| `TJ_ADMIN_API_KEY` | Optional workspace-admin API key |
| `USER_SESSION_EXPIRY` | User session lifetime |
| `DISABLE_SIGNUPS` | Disables new user registration |
| `ENABLE_CORS` | Enables cross-origin access |
| `DISABLE_APP_EMBED` | Disables application embedding |
| `ENABLE_PRIVATE_APP_EMBED` | Allows private app embedding |

### PostgreSQL

| Variable | Purpose |
| --- | --- |
| `PG_DB` | Application database name |
| `PG_USER` | Database username |
| `PG_HOST` | PostgreSQL host |
| `PG_PASS` | PostgreSQL password |
| `ORM_LOGGING` | Controls ORM logging |

### ToolJet Database

| Variable | Purpose |
| --- | --- |
| `TOOLJET_DB` | Built-in database name |
| `TOOLJET_DB_USER` | Built-in database user |
| `TOOLJET_DB_HOST` | Built-in database host |
| `TOOLJET_DB_PASS` | Built-in database password |
| `TOOLJET_DB_RECONFIG` | Enables ToolJet database reconfiguration |
| `TOOLJET_DB_STATEMENT_TIMEOUT` | Query timeout in milliseconds |
| `PGRST_HOST` | PostgREST host |
| `PGRST_JWT_SECRET` | PostgREST JWT secret |
| `PGRST_DB_PRE_CONFIG` | PostgREST pre-configuration function |

### Redis and Workflows

| Variable | Purpose |
| --- | --- |
| `REDIS_HOST` | Redis host |
| `REDIS_PORT` | Redis port |
| `REDIS_USERNAME` | Optional Redis username |
| `REDIS_PASSWORD` | Optional Redis password |
| `REDIS_DB` | Redis database number |
| `REDIS_TLS` | Enables Redis TLS |
| `WORKER` | Enables worker-mode processing |
| `TOOLJET_QUEUE_DASH_PASSWORD` | Workflow queue dashboard password |
| `TOOLJET_WORKFLOW_SANDBOX_BYPASS` | Disables Python isolation when explicitly required |

Disabling the workflow sandbox reduces isolation and should be avoided unless the hosting environment cannot support the required sandbox capability.

### Email and Authentication

| Variable | Purpose |
| --- | --- |
| `DEFAULT_FROM_EMAIL` | Default email sender |
| `SMTP_DISABLED` | Disables SMTP |
| `SMTP_USERNAME` | SMTP username |
| `SMTP_PASSWORD` | SMTP password |
| `SMTP_DOMAIN` | SMTP server |
| `SMTP_PORT` | SMTP port |
| `GOOGLE_CLIENT_ID` | Google OAuth client identifier |
| `GOOGLE_CLIENT_SECRET` | Google OAuth client secret |
| `SSO_GOOGLE_OAUTH2_CLIENT_ID` | Workspace Google SSO identifier |
| `SSO_GIT_OAUTH2_CLIENT_ID` | Git-based SSO identifier |
| `SSO_GIT_OAUTH2_CLIENT_SECRET` | Git-based SSO secret |
| `SSO_ACCEPTED_DOMAINS` | Restricts accepted SSO domains |

### Observability

| Variable | Purpose |
| --- | --- |
| `APM_VENDOR` | Selects application performance monitoring integration |
| `SENTRY_DNS` | Sentry configuration |
| `SENTRY_DEBUG` | Controls Sentry debugging |
| `ENABLE_METRICS` | Enables Prometheus metrics |
| `SLOW_QUERY_LOGGING_THRESHOLD` | Slow-query threshold |

### Telemetry

Relevant controls include:

```text
CHECK_FOR_UPDATES
DISABLE_TOOLJET_TELEMETRY
```

Review these settings for restricted or offline environments.

## Build and Deployment

### Build All Components

```bash
npm run build
```

The root build compiles plugins, frontend assets, and backend code.

### Build Frontend

```bash
npm run build:frontend
```

### Build Backend

```bash
npm run build:server
```

### Build Plugins

```bash
npm run build:plugins:prod
```

### Start Production Server

```bash
npm run start:prod
```

### Start Production Worker

```bash
npm run worker:prod
```

Production deployments should:

- Use unique encryption and signing secrets
- Protect PostgreSQL, Redis, and PostgREST from public access
- Use persistent database storage
- Configure HTTPS
- Restrict application origins
- Run migrations before application startup
- Separate workers for workflow-heavy installations
- Use secure Redis authentication when required
- Configure SMTP deliberately
- Back up PostgreSQL regularly
- Monitor queues, database performance, and worker failures
- Prefer stable or LTS releases for production upgrades

## Testing

### Backend Tests

```bash
npm --prefix server test
```

Run coverage:

```bash
npm --prefix server run test:cov
```

Run backend end-to-end tests:

```bash
npm --prefix server run test:e2e
```

### Frontend Tests

```bash
npm --prefix frontend test
```

### Type Checking

```bash
npm --prefix frontend run typecheck
```

### Frontend Linting

```bash
npm --prefix frontend run lint
```

### Backend Linting

```bash
npm --prefix server run lint
```

### Storybook

```bash
npm --prefix frontend run storybook
```

## Contributing

ToolJet uses a pull-request-based development workflow.

Before starting implementation:

- Select an existing issue or propose a focused change
- Coordinate on the issue before beginning substantial work
- Create the branch from `main`
- Use a clear branch prefix such as `feature`, `fix`, `docs`, or `chore`

Before submitting a pull request:

- Keep the branch synchronized with `main`
- Add or update tests
- Run affected test suites
- Run linting
- Run frontend type checks when applicable
- Update documentation for user-facing behavior
- Include screenshots or recordings for interface changes
- Keep the change limited to one clear purpose
- Avoid committing credentials or environment files
- Target the `main` branch
