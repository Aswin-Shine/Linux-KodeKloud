After conducting a security audit within the Stratos DC, the Nautilus security team discovered misconfigured permissions on critical files. To address this, corrective actions are being taken by the production support team. Specifically, the file named /etc/hostname on Nautilus App 2 server requires adjustments to its Access Control Lists (ACLs) as follows:

1. The file's user owner and group owner should be set to root.
2. Others should possess read only permissions on the file.
3. User kirsty must not have any permissions on the file.
4. User garrett should be granted read only permission on the file.

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Change the owernship of the file to root

```
sudo chown root:root /etc/hostname
```

3. Set read only permissions to the file other than root user.

```
sudo chmod 644 /etc/hostname
```

4. ACL for the user kirsty and garrett

```
sudo setfacl -m u:kirtsty:---,u:garrett:r--- /etc/hostname
```

5. Verify the task

```
ls -la /etc/hostname
getfacl /etc/hostname
```
