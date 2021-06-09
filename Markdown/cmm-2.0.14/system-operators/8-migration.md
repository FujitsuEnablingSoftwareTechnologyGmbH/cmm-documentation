## 8 Migration

This chapter describes the process of migration from CMM v2.0.13 to CMM v2.0.14

## 8.1 MySQL Database Migration

> **Note 1:** The migration process of MySQL Database from CMM v2.0.13 to CMM v2.0.14 is based on the
  [MySQL Database Backup and Recovery](./4-operation-and-maintenance.md#mysql-database)
  Steps.

> **Note 2:** It is assumed that the tenant and its tenant-id used for monitoring have not changed..

### Back up CMM v2.0.13 MySQL database:

1. Log in to the CMM node with v2.0.13 as a user with root privileges.
2. Stop all CMM agents and services:
```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml stop
```

3. Start the `mysql` service:
```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml up -d mysql
```

4. Backup the database. To create the backup from your local machine, execute the following
   command:
```
docker exec <container_id> mysqldump -u root --password=secretmysql mon > <backup_dir>/<name>
```

Replace:
- `<container_id>` by the ID of the container in which the database is running.
- `<db_name>` by the name of the database.
- `<backup_dir>` by the directory you have mounted for storing the backup file.
- `<name>` by the name of the backup file to be created.

For the `--password` parameter, check the `MYSQL_ROOT_PASSWORD` specified in the
`docker-compose-metric.yml` file.

The following example creates a backup of the `mon` database, running in container
`07e9007e0be8`, in `/backup/mon.sql`:
```
docker exec 07e9007e0be8 mysqldump -u root --password=secretmysql mon > /backup/mon.sql
```

5. Check whether the backup was created successfully. In order to see its content you can
   use vim:
```
vim /backup/mon.sql
```

### Restore MySQL database in CMM v2.0.14:

> **Note:** In this step it is assumed that the CMM node with v 2.0.14 was successfully installed and
  all containers are running as described in chapter
  [2.3 Installing the Monitoring Service](./2-installation.md#23-installing-the-monitoring-service)

1. Log in to the new CMM node with v2.0.14 as a user with root privileges and
   transfer the file `mon.sql`.
2. Stop all CMM agents and services:
```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml stop
```

3. Start the mysql service:
```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml up -d mysql
```

4. Restore the database:

```
cat <backup_dir>/<name> | docker exec -i <container_id> mysql -u root --password=secretmysql mon
```

Replace:
- `<backup_dir>` by the directory where the backup file is stored.
- `<name>` by the name of the file.
- `<container_id>` by the ID of the container in which the database is running.

For the `--password` parameter, check the `MYSQL_ROOT_PASSWORD` specified in the
`docker-compose-metric.yml` file.

The following example restores the mon database, running in container `07e9007e0be8`, from `/
backup/mon.sql`:

```
cat /backup/mon.sql | docker exec -i 07e9007e0be8 mysql -u root --password=secretmysql mon
```

5. Stop the `mysql` service:

```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml stop mysql
```

6. Start all CMM agents and services:

```
docker-compose -f docker-compose-metric.yml -f docker-compose-log.yml up -d
```

For additional information on backing up and restoring a MySQL database with `mysqldump`, refer
to the *MySQL documentation*.
