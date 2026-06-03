During the monthly compliance meeting, it was pointed out that several servers in the Stratos DC do not have a valid banner. The security team has provided serveral approved templates which should be applied to the servers to maintain compliance. These will be displayed to the user upon a successful login.

Update the message of the day on all application servers for Nautilus. Make use of the approved template located at /home/thor/nautilus_banner on the jump host.

Solution :

1. Copy the banner file from jumphost to all the servers.

```
scp /home/thor/nautilus_banner tony@stapp01:/tmp/nautilus_banner
scp /home/thor/nautilus_banner steve@stapp02:/tmp/nautilus_banner
scp /home/thor/nautilus_banner banner@stapp03:/tmp/nautilus_banner
```

2. SSH into all the servers one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

3. Copy the file to /etc/motd directory.

```
sudo cp /tmp/nautilus_banner /etc/motd
```

4. Verify the task by logging into any app server.

```
ssh tony@stapp01
```
