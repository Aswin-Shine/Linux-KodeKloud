At xFusionCorp Industries, the Stratos Datacenter houses a jump host server that stores template XML files essential for the Nautilus application. Prior to their use, these files need to be populated with valid data. As part of regular maintenance, the system administration team utilizes various string and file manipulation commands to prepare these templates.

Your task is to substitute all occurrences of the string About with Architecture within the XML file located at /root/nautilus.xml on the jump host server.

Solution :

1. Command to subsitute About to Architecture.

```
sudo sed -i 's/About/Architecture/g' /root/nautilus.xml
```

2. To verify the task.

```
sudo grep "About" /root/nautilus.xml
sudo grap "Architecture" /root/nautilus.xml
```
