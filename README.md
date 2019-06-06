# sql-server-drop-table-issue
This project demonstrates an issue in Laravel when using a sqlsrv database connection and running the RefreshDatabase trait on tests or manually runing php artisan migrate:fresh.
Laravel uses the following command to disable foreign keys before dopping all tables:
```EXEC sp_msforeachtable "ALTER TABLE ? NOCHECK CONSTRAINT all";```
The problem is that this sql server command only disables the constraints on INSERT and DELETE and does not work for TRUNCATE or DROP TABLE.

To replicate this error, create an .env file with a DB_CONNECTION=sqlsrv and run phpunit multiple times. 
