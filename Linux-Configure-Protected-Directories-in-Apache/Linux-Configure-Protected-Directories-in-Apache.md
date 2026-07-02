xFusionCorp Industries has hosted several static websites on Nautilus Application Servers in Stratos DC. There are some confidential directories in the document root that need to be password protected. Since they are using Apache for hosting the websites, the production support team has decided to use .htaccess with basic auth. There is a website that needs to be uploaded to /var/www/html/finance on Nautilus App Server 1. However, we need to set up the authentication before that.

1. Create /var/www/html/finance directory if doesn't exist.

2. Add a user jim in htpasswd and set its password to YchZHRcLkL.

3. There is a file /tmp/index.html present on Jump Server. Copy the same to the directory you created, please make sure default document root should remain /var/www/html. Also website should work on URL http://<app-server-hostname>:80/finance/

Solution :

1. Copy the index.html file on to the app server 1

```
scp /tmp/index.html tony@stapp01:/tmp/
```

2. SSH into the app server 1

```
ssh tony@stapp01
sudo su
```

3. Create user and password store

```
sudo htpasswd -cb /etc/httpd/.htpasswd jim YchZHRcLkL
```

4. Create the sub directory and access rule.

```
sudo mkdir -p /var/www/html/finance

sudo vi /var/www/html/finance/.htaccess

# Add this in the file
AuthType Basic
AuthName "Confidential Finance Area"
AuthUserFile /etc/httpd/.htpasswd
Require user jim
```

5. Allow directory override in apache config

```
sudo vi /etc/httpd/conf/httpd.conf

# Change AllowOverride None ---------> All
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```

6. Move that index.html file into the sub directory

```
sudo mv /tmp/index.html /var/www/html/finance/index.html
sudo chown -R apache:apache /var/www/html/finance
sudo chmod 644 /var/www/html/finance/index.html
```

7. Verify and relaod the apache

```
sudo httpd -t
sudo systemctl restart httpd
```

8. Verify the task

```
ssh thor@jump-host

# Unauthorized access will show
curl -I http://stapp01:80/finance/

# Will show the content of index.html
curl -u jim:YchZHRcLkL http://stapp01:80/finance/
```
