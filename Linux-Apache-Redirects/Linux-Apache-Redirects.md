The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:

1.) httpd is already installed on app server 1. Configure Apache to listen on port 5004.

Configure Apache to add some redirects as mentioned below:

a.) Redirect http://stapp01.stratos.xfusioncorp.com:<Port>/ to http://www.stapp01.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301

b.) Redirect http://www.stapp01.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp01.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.

Solution :

1. SSH into app server 1.

```
ssh tony@stapp01
```

2. Edit the apache config file.

```
sudo vi /etc/httpd/conf/httpd.conf

# Add this line (at top of the file)
LoadModule rewrite_module modules/mod_rewrite.so

# Change Listen port
Listen Port 5004

# Change AllOverride (at line 150)
AllowOverride All

# Add this at the bottom of the file
# Force a clean rewrite engine start globally
RewriteEngine On

# Block 1: Catch all non-www traffic and 301 redirect
<VirtualHost *:5004>
    ServerName stapp01.stratos.xfusioncorp.com

    RewriteEngine On
    RewriteRule ^(.*)$ http://www.stapp01.stratos.xfusioncorp.com:5004$1 [R=301,L]
</VirtualHost>

# Block 2: Main block for canonical www traffic and 302 redirect
<VirtualHost *:5004>
    ServerName www.stapp01.stratos.xfusioncorp.com
    DocumentRoot /var/www/html

    Redirect 302 /blog/ http://www.stapp01.stratos.xfusioncorp.com:5004/news/
</VirtualHost>
```

4. Check the config and restart the apache.

```
sudo httpd -t
sudo systemctl restart httpd
```

5. Verify the task.

```
curl -I http://stapp01.stratos.xfusioncorp.com:5004/
curl -I http://www.stapp01.stratos.xfusioncorp.com:5004/blog/
```
