---
layout: page
title: HACKTHISSITE 

---

# Project Work: Hack This Site Missions

#### Basic Missions walkthrough Level 1 - 11 

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

![level 3b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%203b.png)


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

![level 4](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204.PNG)

![level 4b](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204b.PNG)

![level 4c](https://github.com/elizabethude/portfolio/blob/main/projectimages/hts/Level%204c.png)

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

---
##  Level 6
**Description:**
The hint suggests a progressive Caesar cipher. Each character is shifted by an increasing number.

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |


---
---
---
---
---
---
---
---
---
---
---
---
