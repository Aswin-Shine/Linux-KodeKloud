We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 8085 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.

2. Block incoming port 8085 on all apps for everyone except for LBR host.

3. Make sure the rules remain, even after system reboot.

Solution :

1. Check the ip address of the LBR server.

```
sudo ping -c 1 stlb01
```

2. Login into the app server one by one

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

3. Install and enbale the iptables on the server.

```
sudo yum install iptables -y
sudo systemctl start iptables
sudo systemctl enable iptables
sudo systemctl status iptables
```

4. Add the firewall config

```
# 1. Allow the Load Balancer (stlb01) to hit port 8085
sudo iptables -I INPUT 1 -p tcp -s 10.244.97.183 --dport 8085 -j ACCEPT

# 2. Block all other incoming traffic trying to hit port 8085
sudo iptables -I INPUT 2 -p tcp --dport 8085 -j REJECT

# 3. Save the active rules memory state permanently to disk
sudo iptables-save | sudo tee /etc/sysconfig/iptables
```

5. Verify the task.

```
sudo iptables -L INPUT -n --line-numbers
```
