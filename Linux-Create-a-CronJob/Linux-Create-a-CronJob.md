The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

a. Install cronie package on all Nautilus app servers and start crond service.

b. Add a cron _/5 _ \* \* \* echo hello > /tmp/cron_text for root user.

Solution :

1. SSH into every app server one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Install and start Cronie on app servers.

```
sudo yum install -y cronie
sudo systemctl start crond
sudo systemctl enable crond
```

3. Add crontab for root user

```
echo "*/5 * * * * echo hello > /tmp/cron_text" | sudo crontab -u root -
```

4. To verify the task.

```
sudo systemctl status crond

sudo crontab -u root -l
```
