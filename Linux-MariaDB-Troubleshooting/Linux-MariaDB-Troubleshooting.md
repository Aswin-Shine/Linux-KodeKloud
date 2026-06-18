There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.

Solution :

1. SSH into Database Server and become root user

```
ssh peter@stdb01
sudo su
```

2. Try to start MariaDB and check status

```
systemctl start mariadb
systemctl stauts mariadb -l
```

3. Check logs for why it is failing to start the service.

```
tail -n 50 /var/log/mariadb/mariadb.log
```

4. My fix was about mariadb not getting permissions and stale sock file was there.

```
sudo rm -f /var/lib/mysql/mysql.sock
sudo mkdir -p /run/mariadb
sudo chown -R mysql:mysql /run/mariadb
sudo chmod 755 /run/mariadb
chown -R mysql:mysql /var/lib/mysql
chmod -R 755 /var/lib/mysql
```

5. Start MariaDB

```
systemctl start mariadb
systemctl status mariadb
```
