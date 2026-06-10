The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 3 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.

As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

Solution :

1. SSH into app server 3.

```
ssh banner@stapp03
```

2. Append the new nameservers to the top using a temporary variable stream, and overwrite the file's contents directly using standard redirection

```
sudo sh -c 'echo "nameserver 8.8.8.8\nameserver 8.8.4.4\n$(cat /etc/resolv.conf)" > /etc/resolv.conf'
```

3. Verify the task.

```

cat /etc/resolv.conf
```
