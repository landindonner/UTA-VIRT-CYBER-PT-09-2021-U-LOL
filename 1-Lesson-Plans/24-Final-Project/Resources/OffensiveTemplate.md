# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
_TODO: Fill out the information below._

Nmap scan results for each machine reveal the below services and OS details:

![image](https://user-images.githubusercontent.com/88755175/156093325-c4efe907-06b4-419a-a9e7-4ab0115180a5.png)



The following vulnerabilities were identified on each target:
- Target 1
  - Port 22 running OpenSSH 6.7p1 
      - https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=openssh+6.7p1
  - Port 80 running Apache httpd 2.4.10
      - https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=apache+httpd+2.4.10
  - Port 111 running rpcbind 2-4
      - https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=rpcbind+2-4
  - Port 139 and 445 running netbios-ssn Samba smbd 3.X - 4.X
      - https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=samba+smbd+3.X
  - Reconnaissance revealed the website was a wordpress website (http://raven.local/wordpress)

Using wpscan to reveal anything useful:
  
  ![image](https://user-images.githubusercontent.com/88755175/156097890-9e938b35-3514-4a51-99e3-ebc7523bf051.png)
  
Using wpscan to enumerate users:
  
  ![image](https://user-images.githubusercontent.com/88755175/156098075-26ed5e23-6e90-49bc-a2cc-96d37926998c.png)

Users michael and steven were enumerated:

![image](https://user-images.githubusercontent.com/88755175/156098176-e1f67b37-6dd3-4062-85f7-25c6d0fdb005.png)  

SSH into 192.168.1.110 using michael user name. In lieu of using hydra to crack michael password, common passwords were guessed: (password, 123456, test, admin, michael)

![image](https://user-images.githubusercontent.com/88755175/156098868-9d470b01-5cf9-4579-9e36-c8f18c8bd566.png)


### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
Target 1
 `flag1.txt`: flag1{b9bbcb33e11b80be759c4e844862482d}
 
 Searching strings reflexively in the root directory for 'flag1' 
   ![image](https://user-images.githubusercontent.com/88755175/156099446-b82d1786-b3c2-4f9d-a826-92ba2042022f.png)

flag1 was found in service.html    
  ![image](https://user-images.githubusercontent.com/88755175/156099329-e335c9a8-9bd2-49c2-8cec-179d16fac009.png)
  
flag hidden in the footer of the HTML. Searching the source code at http://ravel.local/service.html

![image](https://user-images.githubusercontent.com/88755175/156099922-ce1d92dd-f4ed-4c2a-b519-9345d918f42e.png)

`flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
 
 After gaining access to the server via SSH using michael user name. Simple directory enumeration revealed flag 2:
 ![image](https://user-images.githubusercontent.com/88755175/156100834-46b5f359-005a-423e-b3eb-1495faa95a04.png)
 
 Further searching in accessible directories revealed a wp-config.php with plain text user name and password:
 
 ![image](https://user-images.githubusercontent.com/88755175/156101345-595dad51-8298-4e2a-8428-b32456036381.png)

 Using the discovered user name and password, access to MySQL database was granted:
 
 ![image](https://user-images.githubusercontent.com/88755175/156101668-1884d215-bcc9-4962-badf-7e78d63ac22b.png)
 
 Enumerate databases:
 
 ![image](https://user-images.githubusercontent.com/88755175/156101773-3fd78eb1-7f78-4367-b230-32bbb300d870.png)
 
 Setting the database and enumerating the tables:
 
 ![image](https://user-images.githubusercontent.com/88755175/156102144-b0a8da25-d9f1-4ec9-8ac5-939b51066f10.png)

Selecting all rows from wp_users table:

![image](https://user-images.githubusercontent.com/88755175/156102288-6a833790-438b-48d8-90c6-2a35c0c48791.png)

Username and hashes file was created based on data found in the wp_users table:

![image](https://user-images.githubusercontent.com/88755175/156102422-52cbc226-6568-46ab-abe1-700703c4d399.png)

Used John the Ripper to crack the passwords:

![image](https://user-images.githubusercontent.com/88755175/156102491-cb214d17-7d41-42b5-9a09-df93d94150b7.png)

John revealed steven's password

![image](https://user-images.githubusercontent.com/88755175/156102530-a2c66052-300d-4318-b96f-0d9b7eb14be5.png)

Logging in as wordpress admin using steven's cracked password:

![image](https://user-images.githubusercontent.com/88755175/156103300-fbdb2d4d-37f2-44e8-8b09-9cd964cfb9d9.png)

Items on the dashboard:

![image](https://user-images.githubusercontent.com/88755175/156103373-049e845b-5d66-4c26-97fe-f7b56ecd7db1.png)

Clicking posts flag3 is revealed: 

![image](https://user-images.githubusercontent.com/88755175/156103411-c3614cf8-2ab2-4d40-af96-d5a731347253.png)

flag3: flag3{afc01ab56b50591e7dccf93122770cd2}

![image](https://user-images.githubusercontent.com/88755175/156103479-5a7d1c03-a298-4839-b7b5-c8805d4df9bc.png)

SSH into raven with steven and enumerating his sudo privileges:

![image](https://user-images.githubusercontent.com/88755175/156103784-536800d9-236a-4bad-8738-d3ccba5bea6d.png)

Using python to spawn a root shell:

![image](https://user-images.githubusercontent.com/88755175/156103969-3ff58316-de72-4ce0-8ec1-7c01c72328dc.png)

Enumerating directories. List contents of root directory:

![image](https://user-images.githubusercontent.com/88755175/156104132-03399130-f173-4050-a2e0-749c5dff543a.png)

flag4: flag4{715dea6c055b9fe3337544932f2941ce}

![image](https://user-images.githubusercontent.com/88755175/156104230-1178c3f2-193a-4f65-92b9-0196f7ddac70.png)






 

