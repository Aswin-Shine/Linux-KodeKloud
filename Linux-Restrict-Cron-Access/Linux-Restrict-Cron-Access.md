In alignment with security compliance standards, the Nautilus project team has opted to impose restrictions on crontab access. Specifically, only designated users will be permitted to create or update cron jobs.

Configure crontab access on App Server 1 as follows: Allow crontab access to siva user while denying access to the eric user.

Solution :

1. SSH into app server 1.

```
ssh tony@stapp01
```

2. Command to restict and allow cron access.

```
echo "siva" | sudo tee /etc/cron.allow

echo "eric" | sudo tee /etc/cron.deny
```

3. Verify the task by this command.

```
cat /etc/cron.allow
cat /etc/cron.deny
```
