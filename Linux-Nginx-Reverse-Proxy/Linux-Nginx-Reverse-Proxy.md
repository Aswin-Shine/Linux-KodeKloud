Nautilus system admin's team is planning to deploy a front end application for their backup utility on Nautilus Backup Server, so that they can manage the backups of different websites from a graphical user interface. They have shared requirements to set up the same; please accomplish the tasks as per detail given below:

a. Install Apache Server on Nautilus Backup Server and configure it to use 3001 port (do not bind it to 127.0.0.1 only, keep it default i.e let Apache listen on server's IP, hostname, localhost, 127.0.0.1 etc).

b. Install Nginx webserver on Nautilus Backup Server and configure it to use 8094.

c. Configure Nginx as a reverse proxy server for Apache.

d. There is a sample index file /home/thor/index.html on Jump Host, copy that file to Apache's document root.

e. Make sure to start Apache and Nginx services.

f. You can test final changes using curl command, e.g curl http://<backup server IP or Hostname>:8094.

Solution :

1. Copy the sample file onto the backup server

```
scp /home/thor/index.html clint@stbkp01:/tmp/
```

2. SSH into the backup server

```
ssh clont@stbkp01
sudo su
```

3. Install and configure the apache on the server

```
sudo yum install -y httpd
sudo vi /etc/httpd/conf/httpd.conf

# Change Listen from 80 ------> 3001
```

4. Move the sample file from tmp directory to apache's directory

```
sudo mv /tmp/index.html /var/www/html/index.html
sudo chmod 644 /var/www/html/index.html
```

5. Install niginx and configure on to the server

```
sudo yum install -y nginx
sudo vi /etc/nginx/nginx.conf

# Add this in the server block
server {
    listen       8094 default_server;
    listen       [::]:8094 default_server;
    server_name  _;
    root         /usr/share/nginx/html;

    # Proxy all root traffic to the Apache backend container
    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

6. Test and enable the services

```
sudo nginx -t

sudo systemctl enable --now httpd
sudo systemctl enable --now nginx
```

7. Verify the task

```
curl http://stbkp01:8094
```
