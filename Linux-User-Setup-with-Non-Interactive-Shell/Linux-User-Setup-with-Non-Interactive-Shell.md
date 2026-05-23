To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell. Here's your task:

Create a user named yousuf with a non-interactive shell on App Server 1.

Solution :

1. SSH into app server 1

```
ssh tony@stapp01
```

2. Command for creating user with non-interactive shell

```
sudo useradd -s /sbin/nologin yousuf
```

3. Verfiy the user creation

```
grep yousuf /etc/passwd
```
