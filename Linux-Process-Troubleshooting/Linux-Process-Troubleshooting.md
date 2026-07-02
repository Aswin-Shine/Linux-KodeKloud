The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.

Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not have hosted any code yet on these servers, so you don't need to worry if Apache isn't serving any pages. Just make sure the service is up and running. Also, make sure Apache is running on port 6300 on all app servers.

Solution :

1. Using curl command find which server is having issues.

```
curl -I http://stapp01:6300/
curl -I http://stapp02:6300/
curl -I http://stapp03:6300/
```

2. SSH into the affected server (in my case it was app server 1)

```
ssh tony@stapp01
sudo su
```

3. Restart and check the logs for apache service

```
sudo systemctl status httpd
sudo systemctl restart httpd

journalctl -xeu httpd.service
```

4. Check which service is using the port and stop it

```
sudo ss -tulpn | grep :6300
sudo kill -9 20521
```

5. Restart and enable the apache

```
sudo systemctl restart httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

6. Verify the task

```
curl -I http://stapp01:6300/
```
