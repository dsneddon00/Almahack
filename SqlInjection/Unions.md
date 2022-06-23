# Unions

UNION is used to combine two queries, and you can use it to select information from just about any table in the database; you just have to make sure that the results of each query have the same number of columns.
E.g. `SELECT first_name, last_name FROM users UNION SELECT city, country FROM regions;`
