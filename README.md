In the case you no longer have SSH access to the existing server (i.e. you lost your private key).

1. Stop the running EC2 instance
2. Detach volume (let's call it volume A)
3. Start new t2.micro EC2 instance, using my new key pair. Make sure you create it in the same subnet, otherwise you will have to terminate the instance and create it again.
4. Attach volume A to the new micro instance, as /dev/xvdf (or /dev/sdf)
5. SSH to the new micro instance and mount volume A to /mnt/tmp
6. $ sudo mkdir /mnt/tmp; sudo mount -o nouuid /dev/xvdf1 /mnt/tmp
7. Copy ~/.ssh/authorized_keys to /mnt/tmp/home/ec2-user/.ssh/authorized_keys
8. Logout
9. Terminate micro instance
10. Detach volume A from it
11. Attach volume A back to the main instance as /dev/xvda
12. Start the main instance
13. Login as before, using your new .pem file
