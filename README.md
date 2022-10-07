# Migrate-from-database-with-postgres


In this repository, I will explain step by step how you can migrate your database PostgreSQL.

* 1 - First, you needed have installed Postgres on your computer.
    -  In some cases when you are on a machine different from the servers will be interesting to have the same version of Postgres, because in some moments of a process this can be required.
    
* 2 - We will prepare our new database, install Postgres, and create a database, don't need to create the tables, only the database will serve.
So now we will be exporting data from the old base.	

`create database new_db;`

* 3 - Use the pg_dump tool to export the database into an SQL file.

`pg_dump --username=<DB_USER> --host=<DB_ADDRESS> --port=<DB_PORT> --format=plain --file=<BACKUP_FILE> <DB_NAME>`

- DB_USER indicates the database username.
- DB_ADDRESS indicates the database address.

- DB_PORT indicates the database port.

- BACKUP_FILE indicates the name of the file to which the data will be
exported.

- DB_NAME indicates the name of the database to be migrated.

Enter the database password when prompted.

Example:

`$ pg_dump --username=postgres --host=192.168.151.18 --port=5432 --format=plain --file=backup.sql old_db`


After this command is executed, the " backup.sql file will be generated.

* 4 -  With the backup prepared, the time has come from the import data to the new base.

* 5 - Again, Ensure that the destination database to which data will be imported exists.

* 6 - Import the exported file into new_db with this command.

`psql --host=<DB_ADDRES> --port=<DB_PORT> --username=<DB_USER> -- dbname=<DB_NAME> --file=<BACKUP_DIR>/backup.sql`

- DB_ADDRESS indicates the IP address of the DB instance.
- DB_PORT indicates the  DB instance port.
- DB_USER indicates the database username.
- DB_NAME indicates the name of the database to which data is to be imported. Ensure that the database exists. 
- BACKUP_DIR indicates the directory where the backup.sql file is stored. 

Enter the password for the DB instance when prompted. 

Example:

`$ psql --host=172.16.66.198 --port=5432 --username=postgres --dbname=new_db --file=backup.sql`

* 7  - Now, verify if the data are in the new database and enjoy your win.

