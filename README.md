# Incident-Investigation

## Steps

Independent Examination – Initial Vector of Compromise
1.	Name of attacker’s computer – kali
2.	IP address of attacker – 192.168.56.101
  ![image](https://github.com/user-attachments/assets/5c9954dd-8d42-45c5-94e3-ba29a8425638)


5. Approximate time at which attack started – 11:48 AM (9/7/2021)
 ![image](https://github.com/user-attachments/assets/a1053c16-a841-4624-9dac-9bb93119c943)


 4. Name of the account that was breached – JSmith
 ![image](https://github.com/user-attachments/assets/593c6ece-17d3-4c91-900b-a205767f605e)

On log 7874, we see a successful sign on.
 ![image](https://github.com/user-attachments/assets/5858a350-b944-43f2-92d7-4b6a0149c80a)

We see that the account belongs to JSmith
 ![image](https://github.com/user-attachments/assets/b4886709-cc2c-4d3f-9903-5e751cf98a32)

And it’s by our attacker.
Executive Summary
Our company suffered a breach on September 7th, around 11:56 AM. The attack was a Remote Desktop brute force attack, which started around 11:48 AM and lasted until 11:59 AM, during which, the attacker tried to gain access to multiple of our employee’s accounts. From what we could find, the attacker was successful in gaining access to one of our employee’s account whose username is “JSmith”. The best way to prevent this attack would have been through the use of some sort of time out mechanic, where, once someone guesses a password incorrectly, they are locked out of guessing the password again for a period of time. During this attack, we observed that the attacker made hundreds of attempts at gaining access to the accounts he targeted, all within a couple of minutes, so if we had a system in place that locked him out after guessing wrong a couple of times, we may have been able to prevent this breach. 


Guided Exercise – Post Breach Behavior
1.	3 different commands the attacker ran:
a.	ftp (along with ftp> quit)
 ![image](https://github.com/user-attachments/assets/e6931a96-82e9-490a-9a29-6956ab4f6ccf)

b.	get-process
 ![image](https://github.com/user-attachments/assets/0aebdf46-aa15-4157-bb9a-6e8fce496ef1)

c.	get -wmiobject -class Win32_Product
 ![image](https://github.com/user-attachments/assets/c719b88d-c632-4fd3-96a8-5981cb8c5455)

2.	Purpose of one of the commands:
a.	The ftp command stands for File Transfer Protocol, and it is used to transfer files between hosts, local or remote. 

3.	Specific process of interest: Mozilla Firefox (firefox.exe)
The attacker writes multiple commands related to firefox.exe, which isn’t a behavior that they exhibit for any of the other processes.  
 ![image](https://github.com/user-attachments/assets/37aa78ba-d90c-4f84-be51-b4d835aabcee)
![image](https://github.com/user-attachments/assets/42cf2407-1d93-4f0a-b1e4-cbf14436a8de)
![image](https://github.com/user-attachments/assets/12b5c258-30a5-4564-a280-e08e7ff3adcc)
![image](https://github.com/user-attachments/assets/9940b027-85da-409c-a272-e240f0980b0c)

 
 
 


Independent Examination – Privilege Escalation
1.	I believe that the attacker made use of the Mozilla Firefox web browser application to set the trap. We are told about parent and child applications, and how these can be used to elevate privileges, and the attacker runs multiple commands related to this:
 ![image](https://github.com/user-attachments/assets/fd5f87a7-5fe5-4810-9e7c-52afc06e7619)
![image](https://github.com/user-attachments/assets/547c63be-0ee9-4d05-8760-18c2a011cef7)
![image](https://github.com/user-attachments/assets/991c36e8-38f6-4b87-9912-ce42b72f81ce)

 
 
*Although I do think that Firefox was most likely used as the “trap”, I did also discover the perl.exe file, which is the actual malicious file (I put it into virustotal.com which I’ll show for another question), the part that I haven’t been able to get to the bottom of is how these two things are connected together. 

3.	The attacker replaced his version of perl.exe, which contains malware, with the legitimate file. 
 ![image](https://github.com/user-attachments/assets/3784346c-b7f9-437b-9722-18a693a624c0)

Locations of the two perl.exe files, the top one is the one that contains malware. 
4.	Hash Value for malicious “perl.exe”: 252664a449f41ef095a38b8f6061e943e43f7e73cca842ef3bb4b19738fbac21
Hash Value for normal “perl.exe”: 4d61ebe19311dbf7b9710ac2c6c402e3cba3e23b63e8b82be88e471343bed52d
 ![image](https://github.com/user-attachments/assets/f6c0c1d1-9b38-4e14-9380-98e86e67194c)
![image](https://github.com/user-attachments/assets/e0198611-181f-4d4f-a249-64faa9d42fb8)

 









