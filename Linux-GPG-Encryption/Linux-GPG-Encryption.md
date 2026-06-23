We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.

On storage server in Stratos Datacenter we have private and public keys stored at /home/\*\_key.asc. Use these keys to perform the following actions.

- Encrypt /home/encrypt_me.txt to /home/encrypted_me.asc.

- Decrypt /home/decrypt_me.asc to /home/decrypted_me.txt. (Passphrase for decryption and encryption is kodekloud).

- The user ID you can use is kodekloud@kodekloud.com.

Solution :

1. Login into storage server.

```
ssh natasha@ststor01
```

2. Import the keys.

```
# Import the public key
gpg --import /home/*public_key.asc

# Import the private key
gpg --import /home/*private_key.asc
```

3. Encrypt the file now.

```
gpg --batch --yes --trust-model always --armor --recipient kodekloud@kodekloud.com --output /home/encrypted_me.asc --encrypt /home/encrypt_me.txt
```

4. Decrypt the file now.

```
echo "kodekloud" | gpg --batch --yes --passphrase-fd 0 --output /home/decrypted_me.txt --decrypt /home/decrypt_me.asc
```

5. Verify the task.

```
ls -l /home/encrypted_me.asc /home/decrypted_me.txt
cat /home/decrypted_me.txt
```
