Some users of the monitoring app have reported issues with xFusionCorp Industries mail server. They have a mail server in Stork DC where they are using postfix mail transfer agent. Postfix service seems to fail. Try to identify the root cause and fix it.

Solution :

1. SSH into mail server.

```
ssh groot@stmail01
```

2. Check weather postifx is running or not and try restarting it.

```
sudo systemctl status postfix
sudo systemctl restart postfix

sudo systemctl stauts postfix
```

3. Edit the postfix config file (in my case it was line 135)

```
sudo vi /etc/postfix/main.cf

# Comment the extra inet_interfaces
```

4. Stop and start the postfix.

```
sudo systemctl stop postfix
sudo systemctl start postfix
sudo systemctl enable postfix
```

5. Verift the task.

```
sudo systemctl status postfix
```
