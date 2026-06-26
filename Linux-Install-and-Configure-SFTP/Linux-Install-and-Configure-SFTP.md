Some of the developers from Nautilus project team have asked for SFTP access to at least one of the app server in Stratos DC. After going through the requirements, the system admins team has decided to configure the SFTP server on App Server 2 server in Stratos Datacenter. Please configure it as per the following instructions:

a. Create a SFTP user kareem and set its password to dCV3szSGNA. There is already a group called ftp, you can utilise the same.

b. Password authentication should be enabled for this user.

c. SFTP user should only be allowed to make SFTP connections.

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Create and add user karem to the group.

```
sudo useradd -g ftp -s /sbin/nologin kareem
echo "kareem:dCV3szSGNA" | sudo chpasswd
```

3. Configure the Chroot Directory System Structure

```
# Create the chroot jail foundation directory
sudo mkdir -p /var/sftp/kareem

# Enforce strict root ownership on the jail path
sudo chown root:root /var/sftp /var/sftp/kareem
sudo chmod 755 /var/sftp /var/sftp/kareem

# Create an incoming folder where the user can actually upload files
sudo mkdir -p /var/sftp/kareem/incoming
sudo chown kareem:ftp /var/sftp/kareem/incoming
sudo chmod 755 /var/sftp/kareem/incoming
```

4. Configure the sshd config file & restart the sshd

```
sudo vi /etc/ssh/sshd_config

# Add this at the bottom of the file
Match User kareem
    PasswordAuthentication yes
    ChrootDirectory /var/sftp/kareem
    ForceCommand internal-sftp
    X11Forwarding no
    AllowTcpForwarding no

sudo sshd -t
sudo systemctl restart sshd
```

5. Verify the task

```
# This should fail because we didn't gave permission of ssh to user karem
ssh karem@stapp02

# This will work
sftp kareem@stapp02
```
