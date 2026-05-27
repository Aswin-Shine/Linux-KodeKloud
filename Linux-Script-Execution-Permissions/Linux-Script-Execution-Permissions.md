In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on app server 3 within the Stratos Datacenter.
Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on app server 3. Additionally, ensure that all users have the capability to execute it.

Solution :

1. SSH into app server 03

```
ssh banner@stapp03
```

2. Executable permission command

```
cd /tmp
sudo chmod 777 xfusioncorp.sh
```

3. To verify the task

```
ls -l
```
