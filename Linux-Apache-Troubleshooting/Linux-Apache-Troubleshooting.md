xFusionCorp Industries uses some monitoring tools to check the status of every service, application, etc running on the systems. Recently, the monitoring system identified that Apache service is not running on some of the Nautilus Application Servers in Stratos Datacenter.

1. Identify the faulty Nautilus Application Server and fix the issue. Also, make sure Apache service is up and running on all Nautilus Application Servers. Do not try to stop any kind of firewall that is already running.

2. Apache is running on 5004 port on all Nautilus Application Servers and its document root must be /var/www/html on all app servers.

3. Finally you can test from jump host using curl command to access Apache on all app servers and it should be reachable and you should get some static page. E.g. curl http://stapp01:5004/.

Solution :

1. Use curl command to check in which server httpd is not running.

```
curl http://stapp01:5004/
curl http://stapp02:5004/
curl http://stapp03:5004/
```

3. In app server 1 (tony@stapp01)

```
# All I needed to do is restart the httpd

sudo systemctl status httpd
sudo systemctl start httpd
sudo systemctl status httpd
```

4. In app server 2 (steve@stapp02)

```
# I need to change something in the conf file.

sudo systemctl status httpd
sudo systemctl start httpd

journalctl -xeu httpd.service

sudo vi /etc/httpd/conf/httpd.conf

# Change ServerRoot /etc/httpd;  to ServerRoot "/etc/httpd"

sudo systemctl start httpd
```

5. In app server 3 (banner@stapp03)

```
# I need to change something in the conf file.

sudo systemctl status httpd
sudo systemctl start httpd

journalctl -xeu httpd.service

sudo vi /etc/httpd/conf/httpd.conf

# Change Listen "5004" to Listen 5004
# Change DocumentRoot /var/www/html to DocumentRoot "/var/www/html"

sudo systemctl start httpd
```

6. Verify the task

```
curl http://stapp01:5004/
curl http://stapp02:5004/
curl http://stapp03:5004/
```
