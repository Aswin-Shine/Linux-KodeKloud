The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for archiving website content files. They have a static website running on App Server 3 in Stratos Datacenter, and they need to create a bash script named news_archive.sh which should accomplish the following tasks. (Also remember to place the script under the /scripts directory on App Server 3).

a. Create a zip archive named xfusioncorp_news.zip of /var/www/html/news directory.

b. Save the archive in the /archives/ directory on the App Server 3. This is a temporary storage, as archives from this location will be cleaned on a weekly basis. Therefore, the archive should also be copied to the Nautilus Storage Server so it can be retrieved later for validation purposes.

c. Copy the created archive to the Nautilus Storage Server server in the /archives/ location.

d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

e. Do not use sudo inside the script.

Solution :

1. SSH into app server 3.

```
ssh banner@stapp03
```

2. SSH key send to the storage server.

```
ssh-keygen
ssh-copy-id natasha@ststor01
```

3. Make the bash script in scripts directory.

```
cd /scripts
vi news_archive.sh

#!/bin/bash

SRC_DIR="/var/www/html/news"
ARCHIVE_NAME="xfusioncorp_news.zip"
LOCAL_DEST="/archives"
REMOTE_USER="natasha"
REMOTE_HOST="ststor01"
REMOTE_DEST="/archives/"

# Create the zip archive locally
zip -r "${LOCAL_DEST}/${ARCHIVE_NAME}" "${SRC_DIR}"

# Securely copy the archive to the storage server
scp "${LOCAL_DEST}/${ARCHIVE_NAME}" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DEST}"

```

4. Make script executable and run the script.

```
chmod +x news_archive.sh
./news_archive.sh
```

5. Verify the task.

```
ssh natasha@ststor01
ls -l /archives/
```
