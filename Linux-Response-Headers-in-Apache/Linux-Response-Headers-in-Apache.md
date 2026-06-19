We are working on hardening Apache web server on all app servers. As a part of this process we want to add some of the Apache response headers for security purpose. We are testing the settings one by one on all app servers. As per details mentioned below enable these headers for Apache:

Install httpd package on App Server 2 using yum and configure it to run on 5002 port, make sure to start its service.

Create an index.html file under Apache's default document root i.e /var/www/html and add below given content in it.

Welcome to the xFusionCorp Industries!

Configure Apache to enable below mentioned headers:

X-XSS-Protection header with value 1; mode=block

X-Frame-Options header with value SAMEORIGIN

X-Content-Type-Options header with value nosniff

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Install and configure apache on the server.

```
sudo yum install -y httpd

sudo vi /etc/httpd/conf/httpd.conf

# Change Listen port from 80 to 5002
```

3. Create the web content

```
echo "Welcome to the xFusionCorp Industries!" | sudo tee /var/www/html/index.html
```

4. Inject security response headers

```
sudo vi /etc/httpd/conf.d/security_headers.conf

# Add this in the file
<IfModule mod_headers.c>
    Header set X-XSS-Protection "1; mode=block"
    Header set X-Frame-Options "SAMEORIGIN"
    Header set X-Content-Type-Options "nosniff"
</IfModule>
```

5. Verify the config file and start the apache.

```
sudo httpd -t
sudo systemctl start httpd
sudo systemctl enbale https
```

6. Verify the task.

```
curl -I http://localhost:5002/
```
