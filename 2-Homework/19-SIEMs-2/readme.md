## Unit 19 Homework: Protecting VSI from Future Attacks

### Scenario

In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks. 

You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.

### Logs

Use the same log files you used during the Master of SOC activity:

- [Windows Logs](resources/windows_server_logs.csv)
- [Windows Attack Logs](resources/windows_server_attack_logs.csv)
- [Apache Webserver Logs](resources/apache_logs.txt	)
- [Apache Webserver Attack Logs](resources/apache_attack_logs.txt	)

---

### Part 1: Windows Server Attack

Note: This is a public-facing windows server that VSI employees access.
 
#### Question 1
- Several users were impacted during the attack on March 25th.
- Based on the attack signatures, what mitigations would you recommend to protect each user account? Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.

**Answer: To protect users, one could create a whitelist of only allowing access to those accounts with certain IP addresses.**

**For individual users:**
**User K: An attempt was made to reset an accounts password:**
   **Mitigation: Create a rule in active directory locking out accounts after too many password reset attempts. Also could set up an alert threshold to indicate an unusual amount of resets for that user**
   
**User J: An account successfully logged on:** 
   **Mitigation: Because it appears user J was compromised, the user must be logged off and their password reset by sys admin.**

**User A: A user account was locked out:**
    **Mitigation: The user may be locked out due to too many incorrect passwords. The admin could set up two factor authentication or a progressive delay which locks out your account for only a certain period time.**
    
  
  
#### Question 2
- VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.
- What sort of mitigation could you use to protect against this?

**Mitigation: As with the mitigation strategy for User A, you can set up rules to only lock out an account for a period of time. This will prevent the brute force and allow legitimate access to the server. You could also implement to factor authentication or captcha as well.**
  

### Part 2: Apache Webserver Attack:

#### Question 1
- Based on the geographic map, recommend a firewall rule that the networking team should implement.
- Provide a "plain english" description of the rule.
  - For example: "Block all incoming HTTP traffic where the source IP comes from the city of Los Angeles."
- Provide a screen shot of the geographic map that justifies why you created this rule. 

**Mitigation: Since most of the traffic on the attack logs increased from Ukraine, simply block all IPs that have a source IP from Ukraine**

![image](https://user-images.githubusercontent.com/88755175/152089861-e7bc442f-388c-482e-8374-e1277db15755.png)

  
#### Question 2

- VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

- What other rules can you create to protect VSI from attacks against your webserver?
  - Conceive of two more rules in "plain english". 
  - Hint: Look for other fields that indicate the attacker.
  
  **Mitigation: Since user_agent Mozilla 4.0 was the top entry in the attack logs, the admin could block all traffic that matched the user_agent indicated in the logs. Secondly, the attackers used the URI VSI_Account_logon.php**


### Guidelines for your Submission:
  
In a word document, provide the following:
- Answers for all questions.
- Screenshots where indicated

Submit your findings in BootCampSpot!

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
