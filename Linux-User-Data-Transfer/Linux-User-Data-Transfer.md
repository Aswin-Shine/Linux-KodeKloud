Due to an accidental data mix-up, user data was unintentionally mingled on Nautilus App Server 1 at the /home/usersdata location by the Nautilus production support team in Stratos DC. To rectify this, specific user data needs to be filtered and relocated. Here are the details:

Locate all files (excluding directories) owned by user kareem within the /home/usersdata directory on App Server 1. Copy these files while preserving the directory structure to the /blog directory.

Solution :

1. SSH into app server 1

```
ssh tony@stapp01
```

2. Get into the directory and copy the files

```
cd /home/usersdata
ls

sudo find . -type f -user kareem -exec cp --parents {} /blog/ \;
```

3. To verify everything is copied use this command.

```
sudo find /blog -type f
```
