# Room: Pickle Rick <img src="/images/pickleRick.jpeg" alt="Rick and Morty" width="50" height="50">


**Infos:** <br>
Difficulty: easy<br>
Est. Time: 30min<br>
Task: Get access, find flags and escalate privileges.<br>
👉 Link: https://tryhackme.com/room/picklerick <br>
<br> 
<br>

# 💡 How I solved the room
**⚠️ Nmap** <br>
In the begining I had to do reconnaissence of the target.<br>
I had to use Nmap and see how many ports are open, also what service is using it.<br>
And it had an active website.
<br>

**🔎 Gobuster**<br>
One of the tasks was finding the hidden directory within **port 80** which was running an basic http-service.<br>
Then after it found the port I used **curl -i http://(ip):80**, and I had to laugh a bit because there was an HTML comment saying:

```
<!--- The login-username was R1ckIsRul1ng ---!>.
```

I scanned with gobuster and it found the subdomains:
- /login.php

**⛓️‍💥 Getting the login** <br>
Now the last thing to do was getting the password, I thought about brute-forceing but then I had an idea, I didn't check the **robots.txt** <br>
So I did check it and it had a wierd String, I copyed it inside of the login and voilà we are now logged in!<br>

**🚩 Searching the flag** <br>
The website had a small command inputline and I tried using **whoAmI** and yes it was a real commandline, <br>
soon after that I read the directory with **ls -la** thats when I found the first flag!
Then I checked with **pwd* where I'm currently at, I used **cd /** to get in the highest directory and then I checked again with **ls -la**
It found **/home/rick**, I instantly checked it and again it had the flag inside of it.

**💥 Privilege Escalation**<br>
The command **sudo -l** showed me that I could use **ANY-Command** with **root rights** but without being root or having to use an password. <br>
My next step was to go inside the root folder with sudo ls -la /root. <br>
And thats when I was stunned, it was actually right, I found the last flag! <br>

# 🛡️ How could this be prevented?
First step is not having an comment inside the website that leaks the username<br>
Second step is not to leak any login-credentails inside Robots.txt (It is ONLY for Webcrawlers and Bots)<br>
Last and the most important step is to secure your user-rights, make sure do not leave any way to ROOT-Access within the system!
<br>
<br>
<a href="https://tryhackme.com/room/picklerick?utm_campaign=social_share&utm_medium=social&utm_content=share-completed-room&utm_source=copy&share_date=2026-11-21&sharerId=6a6db5f574ab7522182287ff">👉 Link to the achivment </a>
