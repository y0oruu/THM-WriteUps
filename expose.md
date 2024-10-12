Name of machine : Expose

Difficulty : Easy

--------------------------------------------------------
Firstly, I have modified my "/etc/hosts" file to add the "expose.thm" hostname.

![image](https://github.com/user-attachments/assets/beb8e512-e95f-4367-b093-f1a3dba5f185)

My first step was to do a nmap scan of the machine to find open ports.

![image](https://github.com/user-attachments/assets/e7596004-9b59-423c-bea8-bbaf7e2b7736)

By this scan, we can see that the "1337" port is open and the service discovered is "waste" , after further research we find that is a peer-to-peer and end-to-end protocol and software application. If we open our browser and type "http://www.expose.thm:1337", we find a web page.

The next step is to start a gobuster scan to find directories, maybe we'll find something interesting. 
Once the scan is done, we can notice 2 interesting directories : "admin" and "admin_101".

![image](https://github.com/user-attachments/assets/5669c114-3abe-4dfd-a781-febb8862396e)

When we try submitting a login request in the "/admin" page we find out that the button is not working at all. So let's try in the "admin_101" directory. And after testing, we find out that the button is working on this page !
So let's try capturing the request in BurpSuite !

![image](https://github.com/user-attachments/assets/1f3ab0c2-efaa-458f-a9a6-87ed328ffe4b)

Next, we save the request in a ".txt" file and try to use it in sqlmap. And we can see that the login form is vulnerable to SQL injection !

![image](https://github.com/user-attachments/assets/c5e53bc2-36a7-4453-b239-2bd9ca73cd36)



