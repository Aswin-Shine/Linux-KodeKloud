xFusionCorp Industries has an application running on Nautlitus infrastructure in Stratos Datacenter. The monitoring tool recognised that there is an issue with the haproxy service on the LBR server. That needs to fixed to make the application work properly.

Troubleshoot and fix the issue, and make sure haproxy service is running on the Nautilus LBR server. Once fixed, make sure you are able to access the website by running the command curl http://stlb01:80/ in the terminal.

Solution :

1. SSH into load balancer server.

```
ssh loki@stlb01
```

2. Check the status of the haproxy and try to restart it.

```
sudo systemctl status haproxy
sudo systemctl restart haproxy
```

3. Remove the override.conf found in the status error code.

```
sudo rm -rf /etc/systemd/system/haproxy.service.d
sudo systemctl daemon-reload
```

4. Check for the ip address of the app server

```
getent hosts stapp01 stapp02 stapp03
```

5. Now edit the config file haproxy.

```
sudo vi /etc/haproxy/haproxy.cfg

# Change frontend main
             bind *:80

# Comment use_backend static

# Comment whole backend section also.

# Add this to the backend section
server        stapp01 10.244.221.67:8080 check
server        stapp02 10.244.226.15:8080 check
server        stapp03 10.244.164.79:8080 check
```

6. Verify the task.

```
curl http://stlb01:80/
```
