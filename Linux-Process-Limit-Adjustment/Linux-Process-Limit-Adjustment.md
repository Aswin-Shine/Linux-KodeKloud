In the Stratos Datacenter, our application server 1 is encountering performance degradation due to excessive processes held by the nfsuser user. To mitigate this issue, we need to enforce limitations on its maximum processes. Please set the maximum process limits as specified below:

a. Set the soft limit to 1027

b. Set the hard limit to 2026

Solution :

1. SSH into app server 1

```
ssh tony@stapp01
```

2. Run this command to set soft and hard process limits.

```
echo "nfsuser soft nproc 1027" | sudo tee -a /etc/security/limits.conf
echo "nfsuser hard nproc 2026" | sudo tee -a /etc/security/limits.conf
```

3. Verify the task.

```
tail -n 5 /etc/security/limits.conf
```
