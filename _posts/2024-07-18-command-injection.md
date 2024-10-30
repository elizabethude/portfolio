---
layout: post
title: Command Injection - TryHackMe
---



In this room, we'll go through the concept of detection engineering and frameworks used towards crafting effective threat detection strategies.

Before starting, I’d recommend checking out the reading material provided with each task — it’ll give you a solid foundation. 



## **Task 2 Discovering Command Injection**


**What variable stores the user's input in the PHP code snippet in this task?**

![2a](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/2a.PNG?raw=true)


>  $title


**What HTTP method is used to retrieve data submitted by a user in the PHP code snippet?**

>  GET


**If I wanted to execute the id command in the Python code snippet, what route would I need to visit?**

![2c](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/2c.PNG?raw=true)

>  /id



##  **Task 3 Exploiting Command Injection**


**What payload would I use if I wanted to determine what user the application is running as?**

![3a](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/3a.PNG?raw=true)


>  whoami


**What popular network tool would I use to test for blind command injection on a Linux machine?**

![3bc](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/3bc.PNG?raw=true)


>  ping

**What payload would I use to test a Windows machine for blind command injection?**

>  timeout



##   **Task 4 Remediating Command Injection**


**What is the term for the process of "cleaning" user input that is provided to an application?**

![4a](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/4a.PNG?raw=true)



>  sanitisation



##  **Task 5 Practical: Command Injection (Deploy)**

**What user is this application running as?**

![5a](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/5a.PNG?raw=true)


>  www-data

**What are the contents of the flag located in /home/tryhackme/flag.txt?**

![5b](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/5c.PNG?raw=true)


![5c](https://github.com/elizabethude/portfolio/blob/main/projectimages/tryhackme/command%20injection/5d.PNG?raw=true)




>  THM{COMMAND_INJECTION_COMPLETE}

