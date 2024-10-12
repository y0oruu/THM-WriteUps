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

After dumping the "expose" database we find two links and the password for one page. The other one is asking for an username starting with "z". The first page is vulnerable to LFI, so let's try to get an output of the "/etc/passwd" file to get the user. After getting the content of the "passwd" file, we find out that the user we're looking for is "zeamkish".

![image](https://github.com/user-attachments/assets/f5d953ef-d3e6-4ffa-a626-a3bb6df05ffb)

On the upload page, if we type the user "zeamkish", we have access to an upload page where we can upload only image. If the file extension is not "png" || "jpg" then the upload button is not usable. So if we create a reverse shell with the extension ".php.png" and then capture our request and we put it on the "Repeater" and changing the ".php.png" by just "php", It would work !

![image](https://github.com/user-attachments/assets/10808d16-78a6-484d-86bc-8adb69fee5c3)

So, we create our revershell using "revhshells.com".

![image](https://github.com/user-attachments/assets/0576bce9-2936-4f3e-9e8e-4c47b762972d)

We capture our request : 

![image](https://github.com/user-attachments/assets/cd14ad2e-0e67-4e6b-817f-d07b65e12f1b)

And then we modify our file extension ! 

![image](https://github.com/user-attachments/assets/47c59c5e-cfce-455b-9255-dddcd38c7a69)

Next, we go to the target directory and click on our reverseshell .

![image](https://github.com/user-attachments/assets/00d0330e-4047-4cd4-9c70-a6e063145625)

And we have a shell ! 

![image](https://github.com/user-attachments/assets/846a615a-d928-40cd-849d-b9e200db823a)

After going on the "zeakmish" directory, we have an user.txt but no permission to see it, but there's an another file that we can see the content and it's the ssh creds of zeamkish ! 

![image](https://github.com/user-attachments/assets/c5ed7d02-b144-4f5f-9b42-a5b1cba94ab0)

And we're connected as zeamkish ! 

![image](https://github.com/user-attachments/assets/2246121e-5652-439e-99de-f6738d2c6f0e)

The next step is to look for a way to get root on this machine ! So I'm using linpeas to find a way to do it.

![image](https://github.com/user-attachments/assets/f146f2e2-8f16-4465-81f0-1bc392bc5479)

After check, we can escalate our privileges by using "nano" and "find" SUID. 

![image](https://github.com/user-attachments/assets/87e6ee54-f8c7-4a3c-b605-714f468b9d03)

So finally, by exploiting 'find', we are root !!

![image](https://github.com/user-attachments/assets/541b6276-090a-4428-9050-d9b9fb578eaf)

To conclude, this machine was good, there was a lot of enumeration to make to finally pwn it !

Sorry in advance if this WriteUp is not as good as you expected, it's my first one so i'll keep improving :) !

Thanks for reading and see you in the next WriteUP !








