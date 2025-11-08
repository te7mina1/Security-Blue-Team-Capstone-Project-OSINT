# Capstone Project write-up : Introduction to OSINT (Security Blue Team)

<img width="786" height="728" alt="image" src="https://github.com/user-attachments/assets/03f5521a-4e5a-47c3-8d2c-203e2a726e5f" />

Before completing the SBT OSINT course, I had little knowledge about how Open-Source Intelligence is all about. I faced a lot of challenges whiles taking the course due to unfamiliarity with some of the tools, but I was eager to know more with determination and research online I successfully achieve the aim.

## Introduction

The course introduced us to open source intelligence fundamentals and techniques with tools for information gathering collections such as, theHarvester, Google Dorks and Image search etc. I completed the capstone with the practical skills gained in the course.

## **Challenge Scenario**

You work for a law enforcement organisation, and you have been assigned to track a person-of-interest, that is believed to be associated with a hacking group that recently compromised a Managed Service Provider (MSP) and are trying to sell the stolen credentials on both the clear net and dark web. Another team is focusing on the dark web lead, so you have been tasked with using OSINT sources to build up a profile on the individual and attempt to locate any evidence that links them to the MSP breach and sale of account details. You have been provided with some information to start your investigation. You should use any of the sources or tools taught in this course, that you deem to be applicable and appropriate. **We know that the email address used to register the Twitter account is fake, so do not include this in your report.**

> **Note:** *This is a fictional scenario. Any affiliation between the scenario individual and any real person is strictly coincidental.*
> 

## Challenge Resources

**Your manager has provided you with the following starting information:**

- **Twitter handle used by actor:** *@sp1ritfyre*

SBT-OSINT-Challenge-Report.txt - information needed

```
 ___________   _____ _   ____   _______ ___   _      _
|  _  | ___ \ /  ___| | / /\ \ / /  ___/ _ \ | |    | |
| | | | |_/ / \ `--.| |/ /  \ V /| |_ / /_\ \| |    | |
| | | |  __/   `--. \    \   \ / |  _||  _  || |    | |
\ \_/ / |     /\__/ / |\  \  | | | |  | | | || |____| |____
 \___/\_|     \____/\_| \_/  \_/ \_|  \_| |_/\_____/\_____/

Investigation into MSP data breach. Clear web investigation team.

===============================++===============================

Known Info:
=================
Twitter Handle: @sp1ritfyre

Required Info:
=================
[1] First Name: **Sam**
[2] Last Name: **Woods**
[3] Age: 23
[4] Country: **United Kingdom**
[5] Interests (5 minimum): **Security, Programming, Technology, Gaming, Photography, Camping**
[6] Hacker's employer (company name): **PhilmanSecurityInc.**
[7] Hacker's position within company: **Junior Penetration Tester**

Online Presence:
=================================
[8] Self-Owned Website (Hacker owns the domain): **https://redhunt.net/**
[9] Other Websites (Person does not own the domain, such as blogs): **https://sp1ritfyrehackerstories.blogspot.com/
https://www.blogger.com/profile/08313689826885886832**

Evidence Collection:
=================================
[10] Any URLs of webpages that directly tie individual to MSP breach: **https://www.blogger.com/profile/16540060306570410038
https://sammiewoodsec.blogspot.com/**

Email Addresses Utilised:
=================================
[11] What email addresses have been used by the hacker? (2)
[**d1ved33p@gmail.com**](mailto:d1ved33p@gmail.com)
===============================++===============================

```

## OSINT Information Gathering

Checking for the X account to find any information using Google Dorking.

<img width="1186" height="670" alt="image" src="https://github.com/user-attachments/assets/5121d106-df16-45c3-9033-bfc238cb9782" />


Based on the results it appears to be the first output from the search, which looks very promising with the third output as well. Further investigation, let’s check the account.

<img width="718" height="651" alt="image" src="https://github.com/user-attachments/assets/96a8d6c7-f462-4c0c-ac2e-994f885c4060" />

From the page of our target, we were able to find an encoded text (**cmVkaHVudC5uZXQK.xyz**) in base64. Not sure what it was or where it leads to, I decided to decode it and find what is behind.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%203.png)

There are online tools for decoding an encoded text such as cyberchef, but I decided to use the terminal. Using the command in the terminal

```bash
echo -n "cmVkaHVudC5uZXQK.xyz" | base64 -d
```

I then got the output or decoded text pointing to another url.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%204.png)

Using Google Dorking technique to only find the output related to the target account, @sp1itfyre , I got the first link which leads to the target website.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%205.png)

Checking the website, I did not find anything much on the page. But scrolling down to the website, I realized the target was the owner of the site. 

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%206.png)

Not getting much information, I decided to search for the target user again to find anything related, which then brings me a blogger post website. This time I was sure to get much information about the target user.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%207.png)

From the blog post, we could find several information about the user like the

- **Gender** - which shows female
- **Email** - that’s a link to the target email address and finally
- **the Location** -  but in this case the location has been encoded into hexadecimal, which I need to decode first to find where it sends me to.

**68747470733a2f2f73616d6d6965776f6f647365632e626c6f6773706f742e636f6d**

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%208.png)

After decoding the encoded string from hexadecimal using cyberchef, I got the output pointing to a blogspot ([**https://sammiewoodsec.blogspot.com**](https://sammiewoodsec.blogspot.com/)) page. This time, I was hoping to get most of the information I am looking for about the target.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%209.png)

As hoped, I was able to find most information on this blog post like the target’s

- **Name - Sam Woods**
- **Email - [d1ved33p@gmail.com](mailto:d1ved33p@gmail.com)** and also the about page of the user, **Sam Woods**.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%2010.png)

More on the About page, some of the information required for the task can be found with other interesting information also. I got:

- **Occupation - Junior Penetration Tester**
- **Location - Reading, United Kingdom**
- **Interests - Security, Programming, Technology, Gaming, Photography, Camping**

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%2011.png)

Going very down to the page, I found the age of my target in a section of her post leading to a very detailed section about herself.

- **Age - 23**

> The age also can be found on the same page where she talks about how she entered in to cybersecurity as shown below.
> 

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%2012.png)

In the above, i found a lot of information about how she started, how she grew up and the schools she went to. Focusing more on the company and her role there is most crucial as part of my task.

- **Company - PhilmanSecurityInc.**
- **Role - junior pen tester**

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%2013.png)

Being curious to check for other information also, I decided to go for the “Hacker stories” page, just to see if anything spicy can be found there.

![image.png](Capstone%20Project%20write-up%20Introduction%20to%20OSINT%20(S/image%2014.png)

As shown on the page, “There is nothing here!” and indeed I couldn’t find anything good here. That brings me to the end of the task given to me on OSINT.

> The answers to the task here is provided in the “SBT-OSINT-Challenge-Report.txt” above the page.
> 

## Conclusion

This technique of cyber security dives how both Blue Team (Defensive) and Red Team (Offensive) utilize OSINT in their daily task to better protect the data and security of the organization. Understanding how OSINT or Information Gathering works helps to protect online data, identify potential threats and support incident response.

## Thank you.
