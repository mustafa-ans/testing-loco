# Testing Loco POC

## Overview
This repository contains a Proof of Concept (POC) for building a REST API using the [Loco](https://github.com/loco-rs/loco) web framework in Rust. The goal of this POC was to explore Loco's capabilities, set up a basic REST API, and integrate it with PostgreSQL as the database.

---

## Steps Completed
1. **Project Initialization**:
   - Created a new Loco project using the command:
     ```bash
     loco new
     ```
   - Selected the following options during setup:
     - **App Name**: `testing-loco`
     - **Type**: REST API with PostgreSQL.

2. **Configuration**:
   - Verified that the `config/development.yaml` file was generated with default settings.
   - Ensured that PostgreSQL was installed and running locally.
   - Updated the `DATABASE_URL` in the configuration file to match my local PostgreSQL credentials.

3. **Build and Start**:
   - Built the project using:
     ```bash
     cargo build
     ```
   - Attempted to start the application using:
     ```bash
     cargo loco start
     ```

---

## Issue Encountered

When starting the application, I encountered the following error:

```
2025-02-10T12:10:42.355974Z  INFO app: loco_rs::config: loading environment from selected_path="config\\development.yaml" environment=development
2025-02-10T12:10:42.359611Z  WARN app: loco_rs::boot: pretty backtraces are enabled (this is great for development but has a runtime cost for production. disable with `logger.pretty_backtrace` in your config yaml) environment=development
Error: DB(Conn(SqlxError(PoolTimedOut)))
error: process didn't exit successfully: `target\debug\testing-loco-cli.exe start` (exit code: 1)
```

### Observations:
- The error appears to be related to SQLx's connection pool timing out while waiting for an open connection.
- The PostgreSQL server is running, and the credentials in `config/development.yaml` are correct.
- This might be caused by misconfiguration in PostgreSQL or improper handling of database connections in the application.


### Section: How to Recreate the Issue

To help others reproduce the issue, include the following steps in your README or issue report:

1. **Set up a new Loco project**:
   - Run the following command to create a new project:
     ```bash
     loco new
     ```
   - Select **REST API with PostgreSQL** when prompted for the project type.
   - Provide a name for the project (e.g., `testing-loco`).

2. **Navigate to the project directory**:
   ```bash
   cd testing-loco
   ```

3. **Start the development server**:
   Run the following command to start the server:
   ```bash
   cargo loco start
   ```

4. **Observe the error**:
   The error occurs during startup and looks like this:
   ```
   Error: DB(Conn(SqlxError(PoolTimedOut)))
   error: process didn't exit successfully: `target\debug\testing-loco-cli.exe start` (exit code: 1)
   ```
---

## Next Steps

1. Opened an issue on Loco's GitHub repository to get assistance from maintainers and contributors. Issue link: [GitHub Issue](https://github.com/loco-rs/loco).

3. Once resolved, continue implementing basic REST API endpoints and test CRUD operations with PostgreSQL.

---

## Repository Structure

```
testing-loco/
├── src/
│   ├── app.rs         # Main application logic
│   ├── bin/
│   │   └── main.rs    # Entry point for the application
│   └── ...            # Other modules and files
├── config/
│   ├── development.yaml  # Development environment configuration
│   └── ...               # Other environment configurations (if any)
├── migrations/        # Database migration files (if generated)
└── Cargo.toml         # Rust project dependencies and metadata
```

---

## References

- [Loco Documentation](https://github.com/loco-rs/loco)