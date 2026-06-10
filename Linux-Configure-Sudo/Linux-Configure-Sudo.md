We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.

a. Provide sudo access to user siva on all app servers.

b. Make sure you have set up password-less sudo for the user.

Solution :

1. SSH into all app server one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Make siva password-less sudo user.

```
echo "siva ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.s/siva
sudo chmod 0400 /etc/sudoers.d/siva
```

3. Verify the task.

```
sudo su - siva -c "sudo yum check-update"
```
