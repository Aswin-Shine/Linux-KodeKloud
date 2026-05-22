The system admin team at xFusionCorp Industries has streamlined access management by implementing group-based access control. Here's what you need to do:

a. Create a group named nautilus_sftp_users across all App servers within the Stratos Datacenter.

b. Add the user kano into the nautilus_sftp_users group on all App servers. If the user doesn't exist, create it as well.

Solution :

1. SSH into all the servers one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Group and user creation command.

```
sudo groupadd nautilus_sftp_users && sudo adduser -G nautilus_sftp_users kano
```

3. Verify the group and user has created. 

```
id kano
```
