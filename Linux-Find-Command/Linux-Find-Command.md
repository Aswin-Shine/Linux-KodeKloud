During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:

a. On App Server 1 at location /var/www/html/ecommerce find out all files (not directories) having .php extension. 

b. Copy all those files along with their parent directory structure to location /ecommerce on same server. 

c. Please make sure not to copy the entire /var/www/html/ecommercedirectory content.

Solution :

1. SSH into app server 1.

```
ssh tony@stapp01
sudo su
```

2. Make the directory first.

```
mkdir -p /ecommerce
```

3. Get into the directory and copy all the files with .php using find command

```
cd /var/www/html/ecommerce

find . -type f -name "*.php" -exec cp --parents {} /ecommerce \;
```

4. Verify the task using find command.

```
find /ecommerce -type f ! -name "*.php"
```
