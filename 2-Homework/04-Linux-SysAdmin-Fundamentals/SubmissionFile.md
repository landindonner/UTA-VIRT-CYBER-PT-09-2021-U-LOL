## Week 4 Homework Submission File: Linux Systems Administration

### Step 1: Ensure/Double Check Permissions on Sensitive Files

1. Permissions on `/etc/shadow` should allow only `root` read and write access.

    - Command to inspect permissions: ls -l shadow

    - Command to set permissions (if needed): not needed. permissions -rw-r-----

2. Permissions on `/etc/gshadow` should allow only `root` read and write access.

    - Command to inspect permissions: ls -l gshadow

    - Command to set permissions (if needed): not needed. permissions -rw-r-----

3. Permissions on `/etc/group` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: ls -l group

    - Command to set permissions (if needed): not needed. permissions -rw-r--r--

4. Permissions on `/etc/passwd` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: ls -l passwd

    - Command to set permissions (if needed): not needed. permissions -rw-r--r--

### Step 2: Create User Accounts

1. Add user accounts for `sam`, `joe`, `amy`, `sara`, and `admin`.

    - Command to add each user account (include all five users): 
        1. sudo adduser sam
        2. sudo adduser joe
        3. sudo adduser amy
        4. sudo adduser sara
        5. sudo adduser admin

2. Ensure that only the `admin` has general sudo access.

    - Command to add `admin` to the `sudo` group: sudo usermod -aG sudo admin

### Step 3: Create User Group and Collaborative Folder

1. Add an `engineers` group to the system.

    - Command to add group: sudo addgroup engineers

2. Add users `sam`, `joe`, `amy`, and `sara` to the managed group.

    - Command to add users to `engineers` group (include all four users):
        1. sudo usermod -aG engineers sam
        2. sudo usermod -aG engineers joe
        3. sudo usermod -aG engineers amy
        4. sudo usermod -aG engineers sara

3. Create a shared folder for this group at `/home/engineers`.

    - Command to create the shared folder: sudo mkdir engineers

4. Change ownership on the new engineers' shared folder to the `engineers` group.

    - Command to change ownership of engineer's shared folder to engineer group: 
        1. sudo chown :engineers engineers

### Step 4: Lynis Auditing

1. Command to install Lynis: sudo apt-get install lynis

2. Command to see documentation and instructions: lynis show help OR man lynis

3. Command to run an audit: lynis audit system

4. Provide a report from the Lynis output on what can be done to harden the system.

    - Screenshot of report output:

![LynisScreenshot](https://user-images.githubusercontent.com/88755175/136399813-1b73b822-86a0-4f9b-b2d2-9c158142011f.PNG)




### Bonus
1. Command to install chkrootkit: sudo apt-get install chkrootkit

2. Command to see documentation and instructions: man chkrootkit OR sudo chkrootkit -h

3. Command to run expert mode: sudo chkrootkit -x

4. Provide a report from the chrootkit output on what can be done to harden the system.
    - Screenshot of end of sample output:
    
![ChkrootkitScreenshot](https://user-images.githubusercontent.com/88755175/136399649-8c0e3376-f1a1-43ab-bf2d-2688a8e28ded.PNG)


---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
