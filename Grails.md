# Introduction #

The intent of this plugin is to be somewhat similar to 'rake migrate' but a little more sophisticated.

# Scripts #

There are two scripts included with this plugin.  The first `create-migration` will automatically interrogate your database and create the next migration in sequence for you to fill in with database changes.  These migrations will be named `migratefromN.sql` where N is the version of the database you are migrating from.  They are placed in the `grails-app/migrations/[database product name]` directory within your application.  If you don't have a `db_version` table in your database you must create that table as the first order of business:

```
CREATE TABLE db_version (version integer NOT NULL)
```

Finally, when you want to ensure that your database is at the latest version, simple execute the other script, `grails migrate`.