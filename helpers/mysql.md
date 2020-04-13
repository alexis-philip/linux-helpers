# Mysql

## Log in to mysql as root

```bash
mysql -u root -p
```

## Show MySQL users

```sql
SELECT * FROM mysql.user
```

## Create a MYSQL user

{server}:
 - `%` to allow this user to connect from everywhere (not through PHPMyAdmin);
 - `localhost` to allow this user to connect only from PHPMyAdmin.

```sql
CREATE USER '{mysql_user}'@'{server}' IDENTIFIED BY '{password}';
```

## Grant privileges for MYSQL

```sql
GRANT {privileges} ON {database_name}.{table_name} TO 'database_user'@'localhost';
```

Common privileges are:
 - `ALL PRIVILEGES` - Grants all privileges to a user account.
 - `CREATE` - The user account is allowed to create databases and tables.
 - `DROP` - The user account is allowed to drop databases and tables.
 - `DELETE` - The user account is allowed to delete rows from a specific table.
 - `INSERT` - The user account is allowed to insert rows into a specific table.
 - `SELECT` - The user account is allowed to read a database.
 - `UPDATE` - The user account is allowed to update table rows.

## Show grants from MYSQL user

```sql
SHOW GRANTS FOR 'database_user'@'localhost';
```

## Revoke privileges from MYSQL user

```sql
REVOKE privileges ON 'db_name'.'*' FROM 'mysql_user'@'server';
```

## Delete MYSQL user

```sql
DROP USER 'user'@'localhost'
```

