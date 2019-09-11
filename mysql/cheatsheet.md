# Cheatsheet for MYSQL

- Running a docker container
```bash
docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=pass --name mysql mysql
```

- Executing a MYSQL client shell
```bash
docker exec -it mysql mysql -p
```

## Creating a new user
```sql
CREATE USER 'some-user'@'localhost' IDENTIFIED BY 'some-password';
```

- Adding permissions
```sql
GRANT ALL PRIVILEGES ON * . * TO 'some-user'@'localhost';
```

- Reload all the privileges
```bash
FLUSH PRIVILEGES;
```

## Databases

Creating a Database
```sql
CREATE DATABASE some_database;
```

Using a Database
```sql
USE some_database;
```

Show currently used database
```sql
SELECT DATABASE ();
```