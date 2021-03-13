# Kenobi
My own Writeup of machine Kenobi (Tryhackme)

¡¡¡ IMPORTANT !!!
## First of all, connect to your tryhackme vpn.
¡¡¡ IMPORTANT !!!

1. Scan the machine, i use this command to scan open ports in the machine:

````nmap -T5 -p- -n -v <ip>````
  
![Screenshot_1](https://user-images.githubusercontent.com/80575736/111028536-849d6380-83f7-11eb-8356-e13b67d6fe01.png)

With this information we can show a few open ports, for example port 21 (ftp), port 22 (ssh), port 445 (smb), port 139 (NetBios) and port 445 (Shared_folders SMB)

In this machine we have to explotate SMB shared folders port (445), and ftp (21)

2. When we have open ports in the machine, we have to try internal nmap scripts to see a few vulnerabilities. We can try with this:

$ nmap --script=vuln <ip> 
$ 
