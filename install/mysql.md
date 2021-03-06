# mysql install in ubuntu

```
sudo apt-get update
sudo apt-get install mysql-server
sudo mysql_secure_installation

sudo apt-get update
sudo apt-get install mysql-server

sudo mysql_secure_installation

systemctl status mysql.service
mysqladmin -p -u root version
```

```bash
mysql -u root -p # login in as root user
```

```sql
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'password'; # could be localhost/%/192.168.1.3
GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost';
FLUSH PRIVILEGES;

CREATE DATABASE colorpk2
  DEFAULT CHARACTER SET utf8
  DEFAULT COLLATE utf8_general_ci;

UPDATE
  mysql.user
SET
  authentication_string = PASSWORD('<new password>')
WHERE
  User = 'username';

QUIT;  // check ufw if possible
```
