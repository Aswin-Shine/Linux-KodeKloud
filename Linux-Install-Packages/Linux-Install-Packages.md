As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for strace.

Therefore, install the strace package on all app-servers.

Solution :

1. SSH into all app servers one by one.

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

2. Install the strace package.

```
sudo yum install -y strace
```

3. Verify the task.

```
strace -V
```
