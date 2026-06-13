xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:

1. Install and configure postfix on Stork DC mail server.

2. Create an email account kirsty@stratos.xfusioncorp.com identified by 8FmzjvFU6S.

3. Set its mail directory to /home/kirsty/Maildir.

4. Install and configure dovecot on the same serve

Solution :

1. SSH into mail server

```
ssh groot@stmail01
```

2. Install postfix and dovecot.

```
sudo yum install -y postfix dovecot
```

3. Create user named kristy and mailDir

```
sudo useradd -m kirsty
echo "kirsty:8FmzjvFU6S" | sudo chpasswd

sudo mkdir -p /home/kirsty/Maildir/{cur,new,tmp}
sudo chown -R kirsty:kirsty /home/kirsty/Maildir
sudo chmod -R 700 /home/kirsty/Maildir
```

4. Configure Postfix (SMTP)

```
sudo vi /etc/postfix/main.cf


#Locate or append the following configuration parameters to define the domain identity, listening interfaces, and the Maildir storage format:

myhostname = mail.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
home_mailbox = Maildir/
```

5. Configure Dovecot (IMAP/POP3)

```
sudo vi /etc/dovecot/dovecot.conf

#Ensure the protocols line is uncommented and includes imap and pop3:

protocols = imap pop3 lmtp
```

6. Configure Mail Location

```
sudo vi /etc/dovecot/conf.d/10-mail.conf

#Locate the mail_location line, uncomment it, and alter it to target the explicit home directory mapping:

mail_location = maildir:~/Maildir
```

6. Disable Strict SSL Enforcements (For Testing Environments)

```
sudo vi /etc/dovecot/conf.d/10-auth.conf

#Change disable_plaintext_auth to no:

disable_plaintext_auth = no
```

6. Start and enable postifx and dovecot

```
sudo systemctl restart postfix
sudo systemctl enable postfix

sudo systemctl restart dovecot
sudo systemctl enable dovecot
```

7. Verify the task.

```
echo "Test mail body" | mail -s "Test Subject" kirsty@stratos.xfusioncorp.com
ls -l /home/kirsty/Maildir/new/
```
