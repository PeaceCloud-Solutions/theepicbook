# Persistence and Backup Strategy

**Name:** Peace Nwadinachi Offor  
**Assignment:** Assignment 7

## Database Persistence

The EpicBook MySQL database uses a Docker named volume called `theepicbook_db_data`.

The volume stores database data independently of the lifecycle of the MySQL container. This allows the database container to be stopped, removed, and recreated without losing application data.

The persistence test was performed using:

docker compose down

docker compose up -d

After the containers were recreated, the `BACKUP_RESTORE_TEST` record was queried successfully, confirming that the database data persisted.

## Backup Strategy

Database backups are created using `mysqldump`.

Example:

docker exec epicbook-database sh -c 'exec mysqldump --no-tablespaces -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' > backups/epicbook-before-delete.sql

The backup should be created before destructive database operations and stored separately from the database container.

## Restore Procedure

A database backup can be restored using:

docker exec -i epicbook-database sh -c 'exec mysql -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' < backups/epicbook-before-delete.sql

After restoration, the data should be queried to confirm that the required records have been recovered.

## Recovery Test

A controlled recovery test was completed by:

1. Creating a test database record.
2. Creating a database backup.
3. Deleting the test record.
4. Restoring the database from the backup.
5. Confirming that the deleted record was recovered.
6. Restarting the Docker Compose stack and confirming that the record persisted.

## Important Precaution

`docker compose down -v` should not be used during a normal restart because the `-v` option removes named volumes and can delete persistent database data.
