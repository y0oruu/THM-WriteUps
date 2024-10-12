Name of machine : Expose

Difficulty : Easy

--------------------------------------------------------
Firstly, I have modified my "/etc/hosts" file to add the "expose.thm" hostname.

![image](https://github.com/user-attachments/assets/beb8e512-e95f-4367-b093-f1a3dba5f185)

My first step was to do a nmap scan of the machine to find open ports.

![image](https://github.com/user-attachments/assets/e7596004-9b59-423c-bea8-bbaf7e2b7736)

By this scan, we can see that the "1337" port is open and the service discovered is "waste" , after further research we find that is a peer-to-peer and end-to-end protocol and software application. If we open our browser and type "expose.thm:1337", we find a web page.


