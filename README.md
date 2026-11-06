# brokenpipe-writeup

Here is the original link to KillaBoi's BrokenPipe exploit:
https://github.com/KillaBoi/BrokenPipe

This exploit requires the computer to have steam installed and running in the background.


This is a writeup for utilising BrokenPipe on a windows 11 machine:

First, I set up my windows 11 virtual machine to have steam installed and have my admin account be named “admin”, with an undisclosed password.
My guest account is called “visitor” and the password is “abc123”, let’s simulate privilege escalation for someone with low level access to a windows 11 machine
Admin has administrators as their local group, visitor has users as their local group, this shows visitor is low-level.

<img width="940" height="707" alt="image" src="https://github.com/user-attachments/assets/f6d9cda9-af71-4e79-adc1-6df4419d61a7" />
 
<img width="940" height="715" alt="image" src="https://github.com/user-attachments/assets/9b00fff8-ffbc-4c52-bfba-3b86fa55b6db" />

<img width="940" height="687" alt="image" src="https://github.com/user-attachments/assets/57777f24-9a80-44e5-93e9-df10e854ce78" />

 
 
I have logged into the visitor account. Let’s say that I’m an attacker that wants to disable the firewall settings on the target computer, but when I try to do it on my visitor account I’m prompted for admin login credentials. I want to bypass this, so I’ll utilise BrokenPipe.

<img width="940" height="663" alt="image" src="https://github.com/user-attachments/assets/1088bdd3-5d25-4f19-8e51-8de52b211b7f" />

 

So I navigate to the GitHub repository for BrokenPipe and find the powershell code. Here is the github for BrokenPipe:  https://github.com/KillaBoi/BrokenPipe#what-is-brokenpipe 

<img width="940" height="703" alt="image" src="https://github.com/user-attachments/assets/b5f80c0f-f61e-4be3-a810-86fd6a42b6fa" />

I don’t need to download anything, I can copy and paste the script into PowerShell and it will execute automatically. 
I have to run steam so that steamservice.exe runs in the background (which is what this vulnerability exploits).

<img width="940" height="706" alt="image" src="https://github.com/user-attachments/assets/f5437871-86e9-41db-b7e2-8a9f549ec966" />

No steam login required, I just have the login screen running in the background.
Now I open PowerShell and paste the script. Remember that I have low-level access.
Remember to paste this into PowerShell, not command prompt, they are different.
After a couple seconds, BrokenPipe opens a new command prompt which has NT AUTHORITY access. From here, I can do anything that NT authority users can. Let’s create a new admin account for example.

<img width="940" height="709" alt="image" src="https://github.com/user-attachments/assets/c3cece31-0af2-45be-b7d1-9fa3b3f3c982" />

 
Here I’ve created “hackedadmin” with the same password as visitor “abc123” and added it to the local administrators group. Let’s login to it. We already know that we have administrator permissions on this account, let’s do something with them, like turning off the firewall on our device.

<img width="940" height="712" alt="image" src="https://github.com/user-attachments/assets/317f1669-1058-4e71-aca5-2e45ebb0e68f" />

I then log into my hackedadmin account, see the image below. It’s still part of the administrators group.

<img width="940" height="708" alt="image" src="https://github.com/user-attachments/assets/7fc74678-9dbf-47fb-867d-d5b7fac20195" />

Here I’ve disabled the firewall, but you can also do anything else that you could with an administrator account, say allowing a reverse shell connection to a different computer, allowing you to no longer need require physical access to the computer. 
<img width="940" height="700" alt="image" src="https://github.com/user-attachments/assets/5c9a4e04-b47c-4f25-a293-53f13b3972a4" />

So what did we do? We:
1.	Logged into a low level account named “visitor” with no admin permissions
2.	Exploited BrokenPipe to gain NET AUTHORITY access in a PowerShell window
3.	Used NET AUTHORITY access to create a new administrator account named “hackedadmin”
4.	Utilised administrator access to disable the firewall on the computer, potentially allowing malicious traffic to flow to the computer.
