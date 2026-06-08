The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on Nautilus Backup Server. This is one of the pending items from last month, so please configure a local yum repository on Nautilus Backup Server as per details given below.

a. We have some packages already present at location /packages/downloaded_rpms/ on Nautilus Backup Server.

b. Create a yum repo named epel_local and make sure to set Repository ID to epel_local. Configure it to use package's location /packages/downloaded_rpms/.

c. Install package samba from this newly created repo.

Solution :

1. SSH into nautilus backup server.

```
ssh clint@stbkp01
```

2. Create a yum repo named epel_local in /packages/downloaded_rpms/

```
sudo createrepo /packages/downloaded_rpms/
sudo mkdir -p /etc/yum.repos.d

sudo tee /etc/yum.repos.d/epel_local.repo << 'EOF'
[epel_local]
name=epel_local
baseurl=file:///packages/downloaded_rpms/
enabled=1
gpgcheck=0
EOF
```

3. Clean the cache and check you new repo registration.

```
sudo yum clean all
sudo yum repolist
```

4. Download samba in this repo.

```
sudo yum install --disablerepo=* --enablerepo=epel_local -y samba
```

5. Verify the task.

```
rpm -qi samba
```
