In response to heightened security concerns, the xFusionCorp Industries security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications:

a. Create a user named yousuf on App server 3 within the Stratos Datacenter.

b. Assign a unique UID 1270 and designate the home directory as /var/www/yousuf.

Solution :

1. SSH into app server 3

```
ssh banner@stapp03
```

2. Create the new user

```
sudo useradd -u 1270 -d /var/www/yousuf -m yousuf
```

3. Verify the user has created or not.

```
id yousuf
ls -ld /var/www/yousuf
```
