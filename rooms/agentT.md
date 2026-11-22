# Room: AgentT <img src="/images/pickleRick.jpeg" alt="Rick and Morty" width="50" height="50">


**Infos:** <br>
Difficulty: easy<br>
Est. Time: 10min<br>
Task: Find the exploit and flags.<br>
👉 Link: https://tryhackme.com/room/picklerick <br>
<br> 
<br>

# 💡 How I solved the room
**⚠️ Nmap** <br>
In the begining I had to do reconnaissence of the target.<br>
I had to use Nmap and see what ports are open, also what service is using it.<br>
And it had an active website. running on PHP 8.1.0-dev
<br>

**⛓️‍💥 Finding the exploit** <br>
In the task it said, the response from the server is wierd. So I took a look at it and it didn't seem off but then I've seen the **X-Powered-by PHP 8.1.0-dev** <br>
I googling the exact version I saw many websites saying that it has a critical secureity leak. I went on github and searched for the exploit.
After looking around I found one that was pretty well made, and thats how I successfully exploited an exploit. 

**🚩 Searching the flag** <br>
Because I'm already root, I just had to search for the flag this time i used **find / -type f -name "flag.txt"**
It instantly showed me the flag and with cat I could see the actuall flag


# 🛡️ How could this be prevented?
Currently not finished because I'm doing a room now :)
