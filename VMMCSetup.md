# CHT Sync Setup for VMMC

This document outlines the steps required to set up CHT sync for VMMC. Since this is still a work in progress, you may need to point to different branches instead of the main branch during setup.

### 1. Setting Up Environment Variables

Begin by setting up your environment variables. You’ll need to create a `.env` file either at the root of the repository or in the same directory as your `docker-compose` files.

#### How to Create the `.env` File

You can copy the provided example file and modify it as needed:

```bash
cp .env.example .env
```

Next, open the `.env` file and configure the following variables:

#### PostgreSQL Configuration

- **POSTGRES_USER**: The username for the PostgreSQL database.
- **POSTGRES_PASSWORD**: The password for the PostgreSQL database.
- **POSTGRES_DB**: The name of the PostgreSQL database.
- **POSTGRES_SCHEMA**: The default schema for the pipeline.
- **POSTGRES_TABLE**: The source table in the database where `couch2pg` will insert CouchDB documents.
- **POSTGRES_HOST**: The host of the PostgreSQL service.
- **POSTGRES_PORT**: The port for the PostgreSQL service.

#### DBT Configuration

- **DBT_POSTGRES_USER**: Typically the same as `POSTGRES_USER`, used by DBT to access the database.
- **DBT_POSTGRES_PASSWORD**: Typically the same as `POSTGRES_PASSWORD`, used by DBT to access the database.
- **DBT_POSTGRES_SCHEMA**: Typically the same as `POSTGRES_SCHEMA`, used by DBT to access the database.
- **DBT_POSTGRES_HOST**: Typically the same as `POSTGRES_HOST`, used by DBT to access the database.
- **CHT_PIPELINE_BRANCH_URL**: The URL of the GitHub repository where the pipeline code is fetched by CHT Sync.
- **DATAEMON_INTERVAL**: The interval (in seconds) for data synchronization between CouchDB and PostgreSQL.

#### CouchDB Configuration

- **COUCHDB_USER**: The username for CouchDB, used by `couch2pg` to access CHT data.
- **COUCHDB_PASSWORD**: The password for CouchDB, used by `couch2pg` to access CHT data.
- **COUCHDB_DBS**: A space-separated list of CouchDB databases you want to sync (e.g., `"medic medic_sentinel"`).
- **COUCHDB_HOST**: The host for CouchDB, used by `couch2pg` to access CHT data.
- **COUCHDB_PORT**: The port for CouchDB, used by `couch2pg` to access CHT data.
- **COUCHDB_SECURE**: Set to `true` if using a secure connection to CouchDB, otherwise `false`.

### 2. Starting Services

#### Starting the PostgreSQL Service

To start the PostgreSQL service, run:

```bash
docker-compose -f docker-compose-postgres.yml up -d
```

#### Starting CHT Sync Services

Once PostgreSQL is running, start the rest of the CHT sync services with:

```bash
docker-compose up -d
```
