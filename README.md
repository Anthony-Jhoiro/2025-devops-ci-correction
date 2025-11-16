Welcome to your new TanStack app!

# Getting Started

This project uses **pnpm** as the package manager instead of npm. If you're new to Node.js, pnpm is a faster and more efficient alternative to npm that saves disk space by sharing packages between projects.

## Prerequisites

Before you start, make sure you have:

1. **Node.js** installed (version 18 or higher recommended)
2. **pnpm** installed globally: `npm install -g pnpm`
3. **PostgreSQL** database running (version 16 or higher recommended)

## First Time Setup

### 1. Install Dependencies

When you first clone or download this project, you need to install all the dependencies:

```bash
pnpm install
```

This command reads the `package.json` file and downloads all the required packages into a `node_modules` folder. You only need to run this once, or whenever new dependencies are added to the project.

### 2. Environment Configuration

Create your environment variables file by copying the example:

```bash
cp .env.example .env
```

Then edit the `.env` file with your database configuration:

```bash
# Database connection string
DATABASE_URL=postgres://username:password@host:port/database_name
```

**Examples:**

- Local PostgreSQL: `DATABASE_URL=postgres://postgres:postgres@localhost:5432/todos`
- Docker PostgreSQL: `DATABASE_URL=postgres://postgres:postgres@localhost:5432/todos`
- Cloud database: `DATABASE_URL=postgres://user:pass@db.example.com:5432/todos`

**Important:** Never commit your `.env` file to version control as it contains sensitive information.

### 3. Database Setup

After configuring your environment variables, set up your database schema:

```bash
# Generate migration files (if needed)
pnpm db:generate

# Apply migrations to your database
pnpm db:push
```

**Note:** For development, `pnpm db:push` is usually sufficient as it directly syncs your schema with the database.

# Available Commands

Below are all the commands you can run in this project. In the terminal, always prefix them with `pnpm` (e.g., `pnpm dev`).

## Development Commands

### `pnpm dev`

**What it does:** Starts the development server on port 3000  
**When to use:** This is your main command for developing the app  
**Prerequisites:** Must run `pnpm install` first  
**What happens:** Opens a local server at `http://localhost:3000` with hot-reload (automatically refreshes when you save files)

### `pnpm storybook`

**What it does:** Starts Storybook development server on port 6006  
**When to use:** When you want to develop and test individual components in isolation  
**Prerequisites:** Must run `pnpm install` first  
**What happens:** Opens Storybook at `http://localhost:6006` where you can see all your components

## Building Commands

### `pnpm build`

**What it does:** Creates an optimized production build of your app  
**When to use:** Before deploying your app to production  
**Prerequisites:** Must run `pnpm install` first  
**Output:** Creates files in a build/dist folder that can be deployed to a web server

### `pnpm build-storybook`

**What it does:** Creates a static build of your Storybook  
**When to use:** When you want to deploy your component library documentation  
**Prerequisites:** Must run `pnpm install` first  
**Output:** Creates static files that can be hosted anywhere

## Running Built Applications

### `pnpm start`

**What it does:** Runs the production build of your app  
**When to use:** To test the production build locally  
**Prerequisites:** Must run `pnpm build` first  
**Note:** This runs the optimized version, not the development version

### `pnpm serve`

**What it does:** Serves the built app locally for testing  
**When to use:** Alternative way to test your production build  
**Prerequisites:** Must run `pnpm build` first

## Testing Commands

### `pnpm test`

**What it does:** Runs all tests once and shows results  
**When to use:** To check if all tests pass (great before committing code)  
**Prerequisites:** Must run `pnpm install` first

### `pnpm test:watch`

**What it does:** Runs tests and keeps watching for file changes  
**When to use:** While developing - tests automatically re-run when you save files  
**Prerequisites:** Must run `pnpm install` first  
**How to stop:** Press `Ctrl+C` in the terminal

### `pnpm test:coverage`

**What it does:** Runs all tests and shows how much of your code is tested  
**When to use:** To see which parts of your code need more tests  
**Prerequisites:** Must run `pnpm install` first  
**Output:** Creates a coverage report showing percentages

### `pnpm test:e2e`

**What it does:** Runs end-to-end (e2e) tests using Playwright  
**When to use:** To test your entire application flow from a user's perspective  
**Prerequisites:** Must run `pnpm install` first  
**What it tests:** Real browser interactions, full user workflows, integration between frontend and backend  
**Note:** These tests are slower than unit tests but test the complete application

### `pnpm test:e2e:ui`

**What it does:** Runs Playwright tests with a visual UI interface  
**When to use:** When developing e2e tests or debugging test failures  
**Prerequisites:** Must run `pnpm install` first  
**What happens:** Opens Playwright's test runner UI where you can see tests running in real browsers  
**How to stop:** Close the UI window or press `Ctrl+C` in the terminal

## Database Commands

These commands manage your database schema and migrations using Drizzle ORM:

### `pnpm db:generate`

**What it does:** Creates migration files based on your schema changes  
**When to use:** After you modify your database schema in `src/db/schema.ts`  
**Prerequisites:** Must run `pnpm install` first  
**Run this before:** `pnpm db:migrate` or `pnpm db:push`

### `pnpm db:migrate`

**What it does:** Applies database migrations to update your database structure  
**When to use:** After generating migrations to update your actual database  
**Prerequisites:** Must run `pnpm db:generate` first  
**Important:** This modifies your database, so be careful in production

### `pnpm db:push`

**What it does:** Directly pushes schema changes to the database (skips migrations)  
**When to use:** For development when you want quick schema updates  
**Prerequisites:** Must run `pnpm install` first  
**Warning:** Use with caution - doesn't create migration history

### `pnpm db:studio`

**What it does:** Opens a visual database browser in your web browser  
**When to use:** When you want to see and edit your database data visually  
**Prerequisites:** Must run `pnpm install` first  
**What happens:** Opens a web interface to browse your database tables

## Environment Variables

This application uses environment variables for configuration. All environment variables should be defined in a `.env` file in the root directory.

### Required Environment Variables

| Variable       | Description                  | Example                                             |
| -------------- | ---------------------------- | --------------------------------------------------- |
| `DATABASE_URL` | PostgreSQL connection string | `postgres://postgres:postgres@localhost:5432/todos` |

### Environment Variable Format

The `DATABASE_URL` follows this format:

```
postgres://[username]:[password]@[host]:[port]/[database_name]
```

### Environment Setup Examples

**Local Development:**

```bash
DATABASE_URL=postgres://postgres:postgres@localhost:5432/todos
```

**Docker PostgreSQL:**

```bash
DATABASE_URL=postgres://postgres:postgres@localhost:5432/todos
```

**Production (example with cloud database):**

```bash
DATABASE_URL=postgres://myuser:mypassword@db.example.com:5432/todos_production
```

### Security Notes

- Never commit your `.env` file to version control
- The `.env` file is already in `.gitignore`
- Use strong passwords for production databases
- Consider using connection pooling for production environments

## Code Quality Commands

### `pnpm lint`

**What it does:** Checks your code for style and potential errors  
**When to use:** To find code issues before committing  
**Prerequisites:** Must run `pnpm install` first  
**Output:** Lists any linting errors or warnings

### `pnpm lint:fix`

**What it does:** Automatically fixes linting errors that can be fixed  
**When to use:** When you have linting errors and want to auto-fix them  
**Prerequisites:** Must run `pnpm install` first  
**Note:** Some errors need manual fixing

### `pnpm format`

**What it does:** Automatically formats your code to follow consistent style  
**When to use:** To make your code look clean and consistent  
**Prerequisites:** Must run `pnpm install` first  
**What it formats:** JavaScript, TypeScript, JSON, CSS, and Markdown files

### `pnpm format:check`

**What it does:** Checks if your code is properly formatted (doesn't change files)  
**When to use:** To see if your code needs formatting  
**Prerequisites:** Must run `pnpm install` first  
**Output:** Shows which files need formatting

## Typical Development Workflow

For beginners, here's the usual order of commands:

1. **First time setup:**

```bash
pnpm install
cp .env.example .env
# Edit .env with your database configuration
pnpm db:push
```

2. **Daily development:**

```bash
pnpm dev
```

(Keep this running while you code)

3. **Before committing code:**

```bash
pnpm test          # Run unit tests
pnpm test:e2e      # Run end-to-end tests
pnpm lint          # Check code style
pnpm format        # Format code
```

4. **Working with database:**

```bash
# After changing schema:
pnpm db:generate
pnpm db:push

# To view data:
pnpm db:studio
```

5. **Before deployment:**

```bash
pnpm build
pnpm start  # to test the build
```

## Troubleshooting

### Database Connection Issues

If you encounter database connection errors, check the following:

1. **PostgreSQL is running:**

   ```bash
   # Check if PostgreSQL is running (macOS/Linux)
   pg_isready -h localhost -p 5432

   # Or check running processes
   ps aux | grep postgres
   ```

2. **Environment variables are correct:**

   ```bash
   # Check your .env file exists and has correct format
   cat .env
   ```

3. **Database exists:**

   ```bash
   # Connect to PostgreSQL and check if database exists
   psql -h localhost -U postgres -l
   ```

4. **Network connectivity (for cloud databases):**
   ```bash
   # Test connection to remote database
   pg_isready -h your-db-host.com -p 5432
   ```

### Common Error Messages

- **"database does not exist"**: Create the database or update `DATABASE_URL`
- **"password authentication failed"**: Check username/password in `DATABASE_URL`
- **"connection refused"**: PostgreSQL is not running or wrong host/port
- **"too many connections"**: Database has reached connection limit

### Docker PostgreSQL Quick Commands

```bash
# Start existing container
docker start todo-postgres

# Stop container
docker stop todo-postgres

# Remove container (data will be lost)
docker rm todo-postgres

# View container logs
docker logs todo-postgres
```
