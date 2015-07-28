# Description #
Similar to 'rake migrate' for Ruby on Rails this library lets you manage database upgrades for your Java applications.

# Setup #

  1. Choose a version table name for your database.  The default is `db_version`.
  1. Choose a package within which you will store all your classes and scripts for migrations.
  1. Create a directory within that package named after your database (in lowercase, e.g. `mysql`).
  1. Create a script in that directory named `migrate0.sql` and in that script create the version table and insert version 1, e.g:

```
CREATE TABLE db_version (version integer not null) ENGINE=InnoDB;
INSERT INTO db_version VALUES (1);
```

# Runtime #

  1. Before accessing your database in your programs you need to create a `Migrate` instance with the appropriate database configuration.
  1. Make sure the version is set to the version of the program accessing the database.
  1. Call `migrate()` on your Migrate instance to ensure that your client version matches the database version.  If you have enabled 'auto' and don't specify a client version it will look at the database version it will scan for more recent migrations.  You have a few options for defining migrations.  As far as code they can be either Java, Groovy or SQL.  As far as version transition they can define either 'to' or 'from' flavors. The 'from' flavor is used when you may want to skip versions while the 'to' flavor is for when you want the target database version to be the same as the version number in script and don't mind the reduced flexibility.

  * Attempt to use a migration class: `packageName + databaseName + ".Migrate(To/From)" + dbVersion`
  * If class in 1 not found, use a migration script: `pacakge dir + "/" + databaseName + "/migrate(to/from)" + dbVersion + ".sql"`
  * If script in 2 not found, attempt to use a generic migration class: `packageName + ".Migrate(To/From)" + dbVersion`
  * If class in 3 not found, use a generic migration script: `pacakge dir + "/migrate(to/from)" + dbVersion + ".sql"`

  1. It will return once the client version and database version are equal.  It will throw an exception if anything happens that stops that from being true. It is safe to run the migration from many different programs at the same time due to the locking that it does (in most databases).  It is also safe to run it multiple times.

# Implementation #

  1. Always migrate before the first access to your database in a program
  1. Never upgrade a database in use without a strategy for discovering that its been upgraded
  1. Try to use generic DDL whenever you can if you expect to use more than one type of database with your application

# Future #

  * DDL layer that understands different databases
  * Integration with JPA and other data access frameworks

# LOC #

![http://www.javarants.com/dbmigrate-stats/loc.png](http://www.javarants.com/dbmigrate-stats/loc.png)