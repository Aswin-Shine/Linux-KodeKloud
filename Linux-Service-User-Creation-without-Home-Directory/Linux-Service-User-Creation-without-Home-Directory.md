In response to the latest tool implementation at xFusionCorp Industries, the system admins require the creation of a service user account. Here are the specifics:

Create a user named mark in App Server 1 without a home directory.

Solution :

1. SSH into app server 1

```
ssh tony@stapp01
```

2. Create user without home directory.

```
sudo useradd -M mark
```

3. Verify the user creation by this command.

```
grep mark /etc/passwd
ls -d /home/mark
```
