---
layout: page
title: HACKTHISSITE 

---

# Project Work: Hack This Site Missions


[HackThisSite](https://www.hackthissite.org/) is an online platform to help individuals learn and practice ethical hacking and cybersecurity skills. 

It provides a range of challenges and missions that simulate real-world security vulnerabilities, allowing users to develop and test their penetration testing and problem-solving abilities in a controlled environment.

Here, I demonstrate how I completed the Basic missions, which included identifying potential security vulnerabilities within the application, exploring how attackers might exploit them, and providing recommendations for mitigating the risks identified.

Below is a detailed walkthrough of the challenges faced in the Hack This Site missions. 

## Table of Contents
1. [Level 1](#level-1)
2. [Level 2](#level-2)
3. [Level 3](#level-3)
4. [Level 4](#level-4)
5. [Level 5](#level-5)
6. [Level 6](#level-6)
7. [Level 7](#level-7)
8. [Level 8](#level-8)
9. [Level 9](#level-9)
10. [Level 10](#level-10)
11. [Level 11](#level-11)

---

## Level 1
**Description:**  
View page source to find the password; the password can be found commented out.

![level 1 ](https://raw.githubusercontent.com/elizabethude/portfolio/refs/heads/main/projectimages/hts/Level%201.PNG)

---

## Level 2
**Description:**  
Since there is no text file to compare the user input, pressing enter without typing will sign in the user with an empty password.

---

## Level 3
**Description:**  
To find the password file, view the page source and locate the file name (`password.php`). Append it to the URL:

![level 3](https://raw.githubusercontent.com/elizabethude/portfolio/refs/heads/main/projectimages/hts/Level%203.PNG)

```
https://www.hackthissite.org/missions/basic/3/password.php
```

![level 3b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%203b.png?raw=true)


---

## Level 4
**Description:**  
Find the HTML form that sends the email in the source code.
```
html
<form action="/missions/basic/4/level4.php" method="post">
    <input type="hidden" name="to" value="sam@hackthissite.org" />
    <input type="submit" value="Send password to Sam" />
</form>
```
Solution:
Change the email address to one you have access to. Send the email and check for the password.

![level 4](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204.PNG?raw=true)

![level 4b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204b.PNG?raw=true)

![level 4c](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204c.png?raw=true)

---
##  Level 5
**Description:**
Similar to Level 4, find the HTML form and change the hidden email field.
```
<form action="/missions/basic/4/level4.php" method="post">
    <input type="hidden" name="to" value="sam@hackthissite.org" />
    <input type="submit" value="Send password to Sam" />
</form>
```
Solution:
Change the email address and send the email to retrieve the password.

![level 5](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%205%20(pw).png?raw=true)

---
##  Level 6
**Description:**
The hint suggests a progressive Caesar cipher. An increasing number shifts each character.

|Character     | Shift Applised    | Reverse the shift | Decryted Character|
|:-------------|:------------------|:------------------|:------------------|
| 8            | 0                 |No shift           |a                  |
| c            | 1                 |c → b              |b                  |
| d            | 2                 |d → b              |c                  |    
| 3            | 3                 |3 → 0              |0                  |
| 7            | 4                 |7 → 3              |3                  |
| 7            | 5                 |7 → 2              |2                  |
| =            | 6                 |= → 7              |7                  |    
| l            | 7                 |l → e              |e                  |

Final Decrypted Text:
The decrypted string is 8bb0327e.

---
##  Level 7
**Description:**
Never trust user inputs!

Steps:

Type ;ls into the input box to view the directory.
Append the password file name to the URL:
```
https://www.hackthissite.org/missions/basic/7/k1kh31b1n55h.php
```
![level 7](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%207.png?raw=true)

![level 7b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%207b.png?raw=true)

![level 7c](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%207c.png?raw=true)

---
##  Level 8
**Description:**
Use Server-Side Includes (SSI) to find the hidden password.

Payload:
```
<!--#exec cmd="ls ../"-->
```

Solution:
The command executes and lists the directory content. Copy the password file and append it to the URL to complete the mission.

![Level 8](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%208.png?raw=true)

![Level 8b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%208b.png?raw=true)

![Level 8c](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%208c.png?raw=true)

---

##  Level 9

**Description:**
Like Level 8, inject payload code into the form and traverse to the Level 9 directory.

Payload:
```
<!--#exec cmd="ls ../../9"-->
```
Solution:
Append the password file to the level 9 URL:
```
https://www.hackthissite.org/missions/basic/9/p91e283zc3.php
```
![Level 9](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%209.png?raw=true)

![Level 9b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%209b.png?raw=true)

![Level 9](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%209c.png?raw=true)

---

##  Level 10

**Description:**
This challenge uses cookies for authentication.

Steps:

Open Burp Suite and intercept the request.
Submit any input in the form on level 10.
Change the cookie authentication from "no" to "yes" and forward the request.

![Level 10.png](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%2010.png?raw=true)

![Level 10b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%2010b.png?raw=true)

---

##  Level 11

**Description:**
This challenge emphasizes the importance of not activating directory listing.

Steps:

Append letters to the URL to navigate through directories.
Discovered hidden files like .htaccess and view the relevant code.
Append 'DaAnswer' to the URL to get the following:

```
https://www.hackthissite.org/missions/basic/11/e/l/t/o/n/DaAnswer
```

Append index.php to the URL to access the password entry box. The password is here:
```
https://www.hackthissite.org/missions/basic/11/index.php
```

---

#### Conclusion

This project illustrates various methods for solving web security challenges, emphasizing the importance of understanding web vulnerabilities and user input validation.


