## MySQL notes

### Installation and start/stop

- Install:

      brew install mysql

- To start server:

      mysql.server start

- To connect:

      mysql -uroot

- To have launchd start mysql at login:

      ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents

- Then to load mysql now:

      launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist

- To shutdown server:

      mysql.server stop


### Basics

```
SHOW DATABASES;
CREATE DATABASE [db];
USE [db];
DROP DATABASE [db];
SHOW TABLES;
DESCRIBE [table name];
DROP TABLE [tablename];
```

### Creating a table

```
CREATE TABLE user (
    user_id BIGINT UNSIGNED NOT NULL PRIMARY KEY,
    user_name CHAR(10) NOT NULL,
    last_name VARCHAR(30),
    first_name VARCHAR(30),
    office CHAR(2) NOT NULL DEFAULT 'NY');
```

### Inserting

```
INSERT INTO user VALUES(1, 'kbroman', 'Broman', 'karl', 'AA');
INSERT INTO user (user_id, user_name, office) VALUES(2, 'joe', 'AB');
```

## Updating

```
UPDATE user SET last_name='Smith', first_name='Joe' WHERE user_id=2;
SELECT * FROM user WHERE user_id<5;
```
