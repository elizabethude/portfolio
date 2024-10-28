---
layout: post
---

3

What is SMB?

SMB - Server Message Block Protocol - is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. [source]

Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers.

The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.

How does SMB work?
 **1

 Once they have established a connection, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system. However, in the case of SMB, these things are done over the network.

What runs SMB?

Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support. Samba, an open source server that supports the SMB protocol, was released for Unix systems.

Answer the questions below

What does SMB stand for?    

Server Message Block

What type of protocol is SMB?   

response-request

What do clients connect to servers using?   

TCP/IP

What systems does Samba run on?

Unix

Enumeration

Enumeration is the process of gathering information on a target in order to find potential attack vectors and aid in exploitation.

This process is essential for an attack to be successful, as wasting time with exploits that either don't work or can crash the system can be a waste of energy. Enumeration can be used to gather usernames, passwords, network information, hostnames, application data, services, or any other information that may be valuable to an attacker.

SMB

Typically, there are SMB share drives on a server that can be connected to and used to view or transfer files. SMB can often be a great starting point for an attacker looking to discover sensitive information — you'd be surprised what is sometimes included on these shares.



Port Scanning

The first step of enumeration is to conduct a port scan, to find out as much information as you can about the services, applications, structure and operating system of the target machine.

If you haven't already looked at port scanning, I recommend checking out the Nmap room here.

Enum4Linux

Enum4linux is a tool used to enumerate SMB shares on both Windows and Linux systems. It is basically a wrapper around the tools in the Samba package and makes it easy to quickly extract information from the target pertaining to SMB. It's already installed on the AttackBox, however if you need to install it on your own attacking machine, you can do so from the official github.

The syntax of Enum4Linux is nice and simple: "enum4linux [options] ip"

TAG            FUNCTION

-U             get userlist
-M             get machine list
-N             get namelist dump (different from -U and-M)
-S             get sharelist
-P             get password policy information
-G             get group and member list

-a             all of the above (full basic enumeration)

Now we understand our enumeration tools, let's get started!

Answer the questions below

Conduct an nmap scan of your choosing, How many ports are open?

```
root@ip-10-10-113-212:~# nmap -sS 10.10.21.250
```

3

What ports is SMB running on?

139/445

Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?   

WORKGROUP

What comes up as the name of the machine?    

POLOSMB

What operating system version is running?    

6.1

What share sticks out as something we might want to investigate?    

profiles


4
Types of SMB Exploit

While there are vulnerabilities such as CVE-2017-7494 that can allow remote code execution by exploiting SMB, you're more likely to encounter a situation where the best way into a system is due to misconfigurations in the system. In this case, we're going to be exploiting anonymous SMB share access- a common misconfiguration that can allow us to gain information that will lead to a shell.

Method Breakdown

So, from our enumeration stage, we know:

    - The SMB share location

    - The name of an interesting SMB share

SMBClient

Because we're trying to access an SMB share, we need a client to access resources on servers. We will be using SMBClient because it's part of the default samba suite. While it’s already installed on the AttackBox, if you do need to install it on your own attacking machine, you can find the documentation here.

We can remotely access the SMB share using the syntax:

smbclient //[IP]/[SHARE]

Followed by the tags:

-U [name] : to specify the user

-p [port] : to specify the port


Got it? Okay, let's do this!

Answer the questions below

What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

smbclient //10.10.10.2/secret -U suit -p 445

Great! Now you've got a hang of the syntax, let's have a go at trying to exploit this vulnerability. You have a list of users, the name of the share (smb) and a suspected vulnerability.

Lets see if our interesting share has been configured to allow anonymous access, I.E it doesn't require authentication to view the files. We can do this easily by:

- using the username "Anonymous"

- connecting to the share we found during the enumeration stage

- and not supplying a password.

Does the share allow anonymous access? Y/N?

Y

Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?

John Cactus
