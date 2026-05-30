In the daily standup, it was noted that the timezone settings across the Nautilus Application Servers in the Stratos Datacenter are inconsistent with the local datacenter's timezone, currently set to Asia/Makassar.

Synchronize the timezone settings to match the local datacenter's timezone (Asia/Makassar).

Solution :

1. SSH to all the app server one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Command to set timezone.

```
sudo timedatectl set-timezone Asia/Makassar
```

3. Verify the command.

```
timedatectl
```
