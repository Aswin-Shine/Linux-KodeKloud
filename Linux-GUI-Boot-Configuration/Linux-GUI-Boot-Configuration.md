With the installation of new tools on the app servers within the Stratos Datacenter, certain functionalities now necessitate graphical user interface (GUI) access.

Adjust the default runlevel on all App servers in Stratos Datacenter to enable GUI booting by default. It's imperative not to initiate a server reboot after completing this task.

Solution :

1. SSH into all the servers one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Command to switch from run level 3 (multi-user) to run level 5 (graphical user) on all app servers.

```
sudo systemctl set-default graphical.target
```

3. Verify the task.

```
sudo systemctl get-default
```
