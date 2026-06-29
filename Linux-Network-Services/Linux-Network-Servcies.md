Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 3002 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp02:3002 command from jump host.

Note: Please do not try to alter the existing index.html code, as it will lead to task failure.

Solution :

1. Check in which server apache is not working using curl

```
curl http://stapp01:3002
curl http://stapp02:3002
curl http://stapp03:3002
```

2. Login into the affected server (in my case it was app server 1) and install netstat

```
ssh tony@stapp01
sudo su
sudo dnf install netools -y
```

3. Check logs and restart the apache on the server.

```
sudo systemctl status httpd
sudo systemctl restart httpd

journalctl -xeu httpd.service

# In my case it was port is already alloted issue was in the logs
```

4. Check which service is using port 3002 and terminate it.

```
sudo netstat -tulpn | grep:3002

# PID was 35873
sudo kill -9 35873
```

5. Insert/Update firewall rule to accept traffic in port 3002

```
sudo iptables -I INPUT 2 -p tcp --dport 3002 -j ACCEPT
sudo iptables-save | sudo tee /etc/sysconfig/iptables

# To verify
sudo iptables -L INPUT -n --line-numbers
```

6. Verify the task.

```
ssh thor@jump-host
curl http://stapp01:3002
```
