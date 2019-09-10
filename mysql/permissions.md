# MYSQL Permissions

- Adding permissions
```sql
GRANT <privilege_type> ON <database> . <table> TO 'some-user'@'localhost';
```

- Reload all the privileges
```bash
FLUSH PRIVILEGES;
```

- Review Privileges
```sql
SHOW GRANTS username;
```

- Revoking privileges
```sql
REVOKE <privilege_type> ON <database> . <table> FROM 'some-user'@'localhost';
```

- Dropping users
```sql
DROP USER 'username'@'localhost';
```

## Types of privileges
- ALL PRIVILEGES
- CREATE
- DROP
- DELETE
- INSERT
- SELECT
- UPDATE
- GRANT OPTION
