The Nautilus system administrators team has rolled out a web UI application for their backup utility on the Nautilus application server 2 within the Stratos Datacenter. This application runs on port 8082and appropriate firewall rules must be configured to allow incoming traffic. To achieve this, firewalld needs to be installed and configured on the application server. To ensure proper functionality, the following requirements have been identified:

Install and enable the firewalld service.
Allow all incoming connections on port 8082/tcp.
Ensure the zone is set to public.

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Install and start firewalld in the app server.

```
sudo yum install -y firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

3. Configure the firwalld to run on port 8082.

```
sudo firewall-cmd --zone=public --add-port=8082/tcp --permanent
sudo firewall-cmd --reload
```

4. Verify the task by

```
sudo firewall-cmd --state
sudo firewall-cmd --zone=public --list-all
```
