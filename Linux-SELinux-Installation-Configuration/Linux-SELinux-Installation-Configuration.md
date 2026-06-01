Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:

Install the required SELinux packages.

Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.

No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.

Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Install and configure the selinux in the app server.

```
sudo yum install -y selinux-policy selinux-policy-targeted libselinux-utils policycoreutils

sudo sed -i 's/^SELINUX=.*/SELINUX=disabled' /etc/selinux/config
```

3. Verify the task.

```
cat /etc/selinux/config
```
