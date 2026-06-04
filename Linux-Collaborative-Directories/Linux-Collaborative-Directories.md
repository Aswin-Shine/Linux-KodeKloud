The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the sysops group of the team.

Setup a collaborative directory /sysops/data on app server 2 in Stratos Datacenter.

The directory should be group owned by the group sysops and the group should own the files inside the directory. The directory should be read/write/execute to the user and group owners, and others should not have any access.

Solution :

1. SSH into app server 2.

```
ssh steve@stapp02
```

2. Commands to do this task.

```
sudo mkdir -p /sysops/data
sudo chown :sysops /sysops/data
sudo chmod 2770 /sysops/data
```

3. Verify the task.

```
ls -ld /sysops/data
```
