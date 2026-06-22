The Nautilus DevOps team is ready to launch a new application, which they will deploy on app servers in Stratos Datacenter. They are expecting significant traffic/usage of haproxy on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:

a. In all app servers install haproxy package.

b. Using logrotate configure haproxy logs rotation to monthly and keep only 3 rotated logs.

(If by default log rotation is set, then please update configuration as needed)

Solution :

1. SSH into all the app severs one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Install haproxy and logrotate on the app server.

```
sudo yum install -y haproxy logrotate
```

3. Edit the logrotate config file.

```
sudo vi /etc/logrotate.d/haproxy

# Add this
/var/log/haproxy.log {
    monthly
    rotate 3
    compress
    delaycompress
    missingok
    notifempty
    sharedscripts
    postrotate
        /bin/kill -HUP `cat /var/run/syslogd.pid 2> /dev/null` 2> /dev/null || true
    endscript
}

cat /etc/logrotate.d/haproxy
```

4. Verify the task.

```
sudo logrotate -v -f /etc/logrotate.d/haproxy
```
