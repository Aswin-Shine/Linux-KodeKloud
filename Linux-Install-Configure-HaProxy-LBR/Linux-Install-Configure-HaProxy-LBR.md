There is a static website running in Stratos Datacenter. They have already configured the app servers and code is already deployed there. To make it work properly, they need to configure LBR server. There are number of options for that, but team has decided to go with HAproxy. FYI, apache is running on port 8087 on all app servers. Complete this task as per below details.

a. Install and configure HAproxy on LBR server using yum only and make sure all app servers are added to HAproxy load balancer. HAproxymust serve on default http port (Note: Please do not remove stats socket /var/lib/haproxy/stats entry from haproxy default config.).

b. Once done, you can access the website using curl http://localhost:80 on the LBR server.

Solution :

1. SSH into Load Balancer Server.

```
ssh loki@stlb01
```

2. Install and enable the haproxy on the server.

```
sudo yum install -y haproxy
sudo systemctl enable haproxy
```

3. Check for the ip address of the app server

```
getent hosts stapp01 stapp02 stapp03
```

4. Change the haproxy configure file according to the task.

```
sudo vi /etc/haproxy/haproxy.cfg

# Change frontend bind port to 80 from 5000

# Comment use_backend static

# Add this to the backend section
server        stapp01 10.244.221.67:8087 check
server        stapp02 10.244.226.15:8087 check
server        stapp03 10.244.164.79:8087 check
```

5. Resatrt the haproxy and check the status.

```
sudo systemctl restart haproxy
sudo systemctl status haproxy
```

6. Verify the task.

```
curl http://localhost:80
```
