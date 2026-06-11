To secure our Nautilus infrastructure in Stratos Datacenter, we have decided to install and configure firewalld on one of the app servers named App Server 3. We have Apache and Nginx services running on these apps. Nginx is running as a reverse proxy server for Apache. We might have more robust firewall settings in the future, but for now we have decided to go with the given requirements listed below:

a. Allow all incoming connections on Nginx port, i.e 80.

b. Block all incoming connections on Apache port, i.e 8085.

c. All rules must be permanent.

d. Zone should be public.

e. If Apache or Nginx services aren't running already, please make sure to start them.

Solution :

1. SSH into app server 3.

```
ssh banner@stapp03
```

2. Check the nginx and https is running in the server.

```
sudo systemctl status httpd
sudo systemctl status ngnix
```

3. If nignx is not running it's because httpd (apache) is running on port 80, you need to change the config file of httpd (in my case this happened)

```
sudo vi /etc/httpd/conf/httpd.conf

# Change Listen 80 to 8085
```

4. Restart the httpd and nginx then check for the status.

```
sudo systemctl restart httpd
sudo systemctl restart nginx

sudo systemctl status httpd
sudo systemctl status nginx
```

5. Now install ans enable the firewall in the app server.

```
sudo yum install -y firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

6. Configure firewall to allow traffic into port 80 and deny traffic to port 8085

```
sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" port port="8085" protocol="tcp" drop' --permanent
sudo firewall-cmd --reload
```

7. Verify the task.

```
sudo firewall-cmd --zone=public --list-all
```
