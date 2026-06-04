There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 2, alter the /home/BSD.txt file as per details given below:

a. Delete all lines containing word following and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)

b. Replace all occurrence of word from to them and save results in /home/BSD_REPLACE.txt file.

Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing the string itself; for example upto, contributor etc.

Solution :

1. SSH into app server 2.

```
ssh steve@stapp02
sudo su
```

2. Delete the word following using sed.

```
sed '/following/d' /home/BSD.txt > /home/BSD_DELETE.txt
```

3. Replace from to them using sed.

```
sed 's/\bfrom\b/them/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```

4. Verify the task.

```
grep "following" /home/BSD_DELETE.txt
grep -w "from" /home/BSD_REPLACE.txt
grep -w "them" /home/BSD_REPLACE.txt
```
