# Table of Contents

- [Redis](#redis)
  - [Connect](#connect)
  - [Get value](#get-value)
- [PostgreSQL](#postgresql)
  - [Save backup file](#save-backup-file)
  - [Restore to DB](#restore-to-db)
  - [Commands](#commands)
- [MongoDB](#mongodb)
  - [Save backup file](#save-backup-file-1)
  - [Restore to DB](#restore-to-db-1)

# Redis

## Connect

```bash
redis-cli
```

## Get value

```bash
get ${KEY}
```

# PostgreSQL

## Save backup file

https://www.postgresql.org/docs/current/app-pgdump.html

### Without Docker

```bash
pg_dump -h ${PSQL_HOST} -p ${PSQL_PORT} -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME} > ${BACKUP_NAME}.sql
```

### With Docker

```bash
docker exec ${CONTAINER_NAME} pg_dump -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME} > ${BACKUP_NAME}.sql
```

## Restore to DB

### Without Docker

```bash
psql -h ${PSQL_HOST} -p ${PSQL_PORT} -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME} < ${BACKUP_NAME}.sql
```

Or

```bash
pg_restore -h ${PSQL_HOST} -p ${PSQL_PORT} -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME} < ${BACKUP_NAME}.sql
```

### With Docker

```bash
docker exec -i ${CONTAINER_NAME} psql -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME} < ${BACKUP_NAME}.sql
```

## Commands

### Connect

#### With psql

```bash
psql -h ${PSQL_HOST} -p ${PSQL_PORT} -U ${PSQL_USER_NAME}
```

#### With docker

```bash
docker exec -it ${CONTAINER_NAME} bash
psql -U ${PSQL_USER_NAME} -d ${PSQL_DB_NAME}
```

### Listing all databases

```bash
\l
```

### Switch database

```bash
\c ${PSQL_DB_NAME}
```

### Listing all tables

```bash
\dt
```

### Listing all table's columns

```bash
SELECT table_name, column_name, data_type FROM information_schema.columns WHERE table_name='${TABLE_NAME}';
```

### Import database

```bash
\i /path-of-file
```

# MongoDB

## Save backup file

```bash
mongodump --uri "mongodb+srv://<user>:<password>@<server-uri>/<db-name>" -o ./mongo-backup --collection=<collection-name> --gzip --authenticationDatabase=admin
```

## Restore to DB

```bash
mongorestore --uri "mongodb://<user>:<password>@127.0.0.1:27017" --authenticationDatabase=admin ./mongo-backup/
```

---
