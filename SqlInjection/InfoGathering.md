# Information Gathering

## General

In MySQL, the database called `INFORMATION_SCHEMA` contains metadata on the rest of the databases on the server.
You can see what other databases there are using `INFORMATION_SCHEMA.SCHEMATA`.

You can find info on a specific table using `INFORMATION_SCHEMA.TABLES`.

There is also info on all columns in the databases stored in `INFORMATION_SCHEMA.COLUMNS`.

### Permissions

In MySQL, you can check if the current user on the database has super admin permissions with `SELECT super_priv FROM mysql.user`.

You can see what other privileges you have using `SELECT sql_grants FROM information_schema.sql_show_grants`.

## Files

Keep in mind that you'll likely have to use the below commands with a UNION operator.

### Reading

If the OS user running the database server has the right permissions, you can read from files on the server's machine using `LOAD_FILE(file_path)`.

### Writing

In order to write, the database server's user needs to have file permissions, `secure_file_priv` must be disabled, and the OS user needs write access to wherever it is you want to write to on the machine.

You can check if `secure_file_priv` is enabled using `SHOW VARIABLES LIKE 'secure_file_priv';`.

You can also output the result of a query into a file using `into outfile`, e.g. `SELECT 1, 2, 3, 4 INTO OUTFILE '/var/etc/';`.
