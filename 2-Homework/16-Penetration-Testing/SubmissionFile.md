## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is: **Karl Fitzgerald**

- How can this information be helpful to an attacker: **Attacker could use this info in a whale phishing attack**


#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located: **Sunnyvale, CA**

  2. What is the NetRange IP address: **65.61.137.64 - 65.61.137.127**

  3. What is the company they use to store their infrastructure:  **Rackspace**

  4. What is the IP address of the DNS server: **65.61.137.117**

#### Step 3: Shodan

- What open ports and running services did Shodan find: **80, 443 - Apache/Tomcat/Coyote web service**

#### Step 4: Recon-ng

- Install the Recon module `xssed`. 
- Set the source to `demo.testfire.net`. 
- Run the module. 

Is Altoro Mutual vulnerable to XSS: **Yes. On 08/02/2009 j0rd4n14n.r1z discovered an XSS vulnerability on demo.testfire.net**

### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine: 
 
- Bonus command to output results into a new text file named `zenmapscan.txt`:

![image](https://user-images.githubusercontent.com/88755175/149270387-5990f244-918a-4017-81fd-9fda8c739b29.png)


- Zenmap vulnerability script command: 
 ![image](https://user-images.githubusercontent.com/88755175/149270869-7e715b02-9ede-4ebf-a826-6d77b4aba815.png)


- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:  **CVE-2011-2523 vsFTPd 2.3.4 backdoor**

  2. Why is it dangerous: **This vulnerability can be exploited to return a shell with root privileges**

  3. What mitigation strategies can you recommendations for the client to protect their server:  **Disable FTP or update servers**



---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

