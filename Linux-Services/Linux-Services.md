As per details shared by the development team, the new application release has some dependencies on the back end. There are some packages/services that need to be installed on all app servers under Stratos Datacenter. As per requirements please perform the following steps:

a. Install postfix package on all the application servers.

b. Once installed, make sure it is enabled to start during boot.

Solution :

1. SSH into all app server one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Install and enable postfix.

```
sudo systemctl yum install -y postfix
sudo systemctl start postfix
sudo systemctl enable postfix
```

3. Verify the task.

```
sudo systemctl status postfix
```
