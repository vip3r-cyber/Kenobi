# Kenobi
My own Writeup of machine Kenobi (Tryhackme)

¡¡¡ IMPORTANT !!!
## First of all, connect to your tryhackme vpn.
¡¡¡ IMPORTANT !!!

1. Scan the machine, i use this command to scan open ports in the machine:

````nmap -T5 -p- -n -v <ip>````
  
![Screenshot_1](https://user-images.githubusercontent.com/80575736/111028536-849d6380-83f7-11eb-8356-e13b67d6fe01.png)

With this information we can show a few open ports, for example port 21 (ftp), port 22 (ssh), port 111 (rpcbind) port 445 (smb), port 139 (NetBios) and port 445 (Shared_folders SMB)

In this machine we have to explotate SMB shared folders port (445), and ftp (21)

2. When we have open ports in the machine, we have to try internal nmap scripts to see a few vulnerabilities. We can try with this:

```nmap --script=vuln <ip> ```

For my i try this command and works better for me:

``` nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse <ip>```

![Screenshot_2](https://user-images.githubusercontent.com/80575736/111028824-87995380-83f9-11eb-881f-44023f30b244.png)

This command show the shared folders of the vulnerable machine, and we can watch a share with name "anonymous".

3. Connect with smbclient to see what there is in.

``` smbclient //<ip>/shared_folder```

![Screenshot_3](https://user-images.githubusercontent.com/80575736/111029377-b533cc00-83fc-11eb-8e64-8c7367b52469.png)

To show subfolders and files, we can use command ```ls``` like in linux terminal.

