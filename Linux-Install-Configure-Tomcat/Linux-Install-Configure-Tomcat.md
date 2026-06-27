The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:

a. Install tomcat server on App Server 2.

b. Configure it to run on port 8086.

c. There is a ROOT.war file on Jump host at location /tmp.

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e curl http://stapp02:8086

Solution :

1. SSH into app server 2

```
ssh steve@stapp02
```

2. Install tomcat on the server

```
sudo yum install -y tomcat tomcat-webapps tomcat-admin-webapps
```

3. Configure the tomcat config file.

```
sudo vi /etc/tomcat/server.xml

# Look for this (usally at line number 67)
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />

# Change port to 8086

sudo rm -rf /var/lib/tomcat/webapps/ROOT
```

4. Back into jump host server to send ROOT.war file

```
scp /tmp/ROOT.war steve@stapp02:/tmp/
```

5. Move ROOT.war file to exact location (in app server 2)

```
sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/
sudo chown tomcat:tomcat /var/lib/tomcat/webapps/ROOT.war
```

6. Start and enable the tomcat server.

```
sudo systemctl enable tomcat
sudo systemctl start tomcat
```

7. Verfiy the task.

```
curl http://stapp02:8086
```
