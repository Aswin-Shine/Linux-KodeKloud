Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

Solution :

1. SSH into all app server one by one

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Command to change the direct root SSH Login

```
sudo vi /etc/ssh/sshd_config

* Change PermitRootLogin to no *

sudo systemctl restart sshd
```

3. To verify new config is applied

```
sudo sshd -T | grep -i permitrootlogin
```
