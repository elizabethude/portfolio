---
layout: post
title: 
---

## Task 2 Understanding SMB

**Answer the questions below**

**What does SMB stand for?**

> Server Message Block

**What type of protocol is SMB?**   

> response-request

**What do clients connect to servers using?**   

> TCP/IP

**What systems does Samba run on?**

> Unix


##  Task 3 Enumerating SMB

**Answer the questions below**

Conduct an nmap scan of your choosing, How many ports are open?

```
root@ip-10-10-113-212:~# nmap -sS 10.10.21.250
```

**What ports is SMB running on?**

> 139/445

**Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?**   

>  WORKGROUP

**What comes up as the name of the machine?**    

>  POLOSMB

**What operating system version is running?**    

>  6.1

**What share sticks out as something we might want to investigate?**    

>  profiles - IPC$ and print$ are default SMB shares. netlogon is a share that belongs to the Network Login service. By process of elimination, the share that sticks out is profiles


##  Task 4 Exploiting SMB

**Answer the questions below**

**What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?**

>  smbclient //10.10.10.2/secret -U suit -p 445

Great! Now you've got a hang of the syntax, let's have a go at trying to exploit this vulnerability. You have a list of users, the name of the share (smb) and a suspected vulnerability.

>  No answer needed

Lets see if our interesting share has been configured to allow anonymous access, I.E it doesn't require authentication to view the files. We can do this easily by:

- using the username "Anonymous"

- connecting to the share we found during the enumeration stage

- and not supplying a password.

**Does the share allow anonymous access? Y/N?**
```
smbclient //10.10.21.250/profiles -U Anonymous
```
> Y

**Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?**

>  John Cactus

**What service has been configured to allow him to work from home?**

>  ssh

**Okay! Now we know this, what directory on the share should we look in?**

SSH keys are kept in the **.ssh** directory. By default, the private key for the server is saved in a file named **id_rsa**, while the public key is in **id_rsa.pub**. To connect to the server, we’ll need the private key. Since we don’t know John Cactus’s SSH username, I downloaded the public key, as it often includes the SSH username.

When working with an SMB server, multiple files can be downloaded at once using the mget command.

>  .ssh

**This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?**

>  id_rsa

Download this file to your local machine, and change the permissions to "600" using "chmod 600 [file]".

Now, use the information you have already gathered to work out the username of the account. Then, use the service and key to log-in to the server.

What is the smb.txt flag?

THM{smb_is_fun_eh?}

