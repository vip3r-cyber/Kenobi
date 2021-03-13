# Kenobi
My own Writeup of machine Kenobi (Tryhackme)

¡¡¡ IMPORTANT !!!
Connect to your tryhackme vpn.
¡¡¡ IMPORTANT !!!

1. Scan the machine, i use this command to scan open ports in the machine:

$ nmap -T5 -p- -n -v <ip>
  
![Screenshot_1](https://user-images.githubusercontent.com/80575736/111028536-849d6380-83f7-11eb-8356-e13b67d6fe01.png)

2. When we have open ports in the machine, we have to try internal nmap scripts to see a few vulnerabilities. We can try with this:

$ nmap --script=vuln <ip>
$ 
