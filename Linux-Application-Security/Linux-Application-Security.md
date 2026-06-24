We have a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are 6400 and 8099, respectively. We have to install the iptables firewall on the server. Make the appropriate changes to fulfill the requirements mentioned below:

We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.

Solution :

1.SSH into backup storage server.

```
ssh clint@stbkp01
```

2. Install iptables and iptables-service

```
sudo yum install -y iptables iptables-services
```

3. Check for the current table length (in my case it was 0)

```
sudo iptables -L INPUT -n --line-numbers
```

4. Add nginx and apache firewall rule according to the task.

```
sudo iptables -A INPUT -p tcp --dport 8099 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 6400 -j DROP
```

5. Save the table configuration.

```
sudo iptables-save | sudo tee /etc/sysconfig/iptables
```

6. Enable and restart the iptables.

```
sudo systemctl enable iptables
sudo systemctl restart iptables
```

7. Verify the task.

```
sudo iptables -L INPUT -n --line-numbers
```
