## Nmap

The first thing I did was using the tool nmap to see which ports are open on the server, in this scenario I already know the IP of the WServer.

#### Initial scan
````
nmap -Pn -T4 -sV --min-rate 5000 -p- --open 192.168.122.242 -oX first_scan.xml
Starting Nmap 7.98 ( https://nmap.org ) at 2026-03-14 19:19 +0100
Nmap scan report for WIN-SERVER22 (192.168.122.242)
Host is up (0.00063s latency).
Not shown: 64755 closed tcp ports (reset), 754 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-03-14 18:19:56Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: lab.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: lab.local, Site: Default-First-Site-Name)
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: lab.local, Site: Default-First-Site-Name)
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: lab.local, Site: Default-First-Site-Name)
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
56429/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
56430/tcp open  msrpc         Microsoft Windows RPC
56433/tcp open  msrpc         Microsoft Windows RPC
56440/tcp open  msrpc         Microsoft Windows RPC
56450/tcp open  msrpc         Microsoft Windows RPC
56460/tcp open  msrpc         Microsoft Windows RPC
MAC Address: 52:54:00:5D:DD:27 (QEMU virtual NIC)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 61.80 seconds
````
With the first scan I can see a lot of ports and information but these are the most important to see:

- 88: This port is used with Kerberos, I can try to perform a user enumeration and kerberoasting. 
- 135, 139: Used for MSRPC and NetBIOS, I can obtain more information about the host.
- 445: This port if for the SMB service. I will scan for files that can give me more information and search for vulnerabilities.
- 389, 636: LDAP. In these port I can search for users that are in the domain
- 5985: WinRM. If I get a credential I can try to log in

With this scan I used the searchsploit tool to find useful exploits for this services but unfortunately I didn't find anything.

Now I will try to search for public shares that can give me more information 

I use crackmapexec and I get the name of the server and domain

![](<../../assets/Pasted image 20260403112859.png>)

With nmblookup I get the same information

![](<../../assets/Pasted image 20260403113503.png>)

I try to enumerate users with the anonymous login but it doesn't show me anything.

![](<../../assets/Pasted image 20260403114734.png>)