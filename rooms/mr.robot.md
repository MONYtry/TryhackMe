# Room: Mr. Robot <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRiTt9Ye6G2mBfEcRCUn8UP8E20-ePUQqWNg04wx_eVBQ&s=10" alt="MR. Robot" width="100" height="50">

**Infos:** <br>
Difficulty: medium<br>
Est. Time: 45min<br>
Task: Find all three flags<br>
👉 Link: https://tryhackme.com/room/mrrobot <br>
<br>
<br>

# 📖 Things that I learned:
## 📂 Removing duplicates with Linux
I learned how to remove duplicates from a file. <br>
It is easy with the command: `sort -u (oldFile) -o (newSortedFile)`<br>

## ♻️ Making a reverse shell within websites
I had to find a way inside the server that allowed me to create a reverse shell inside the website. <br>
It was easy because there was already one on GitHub. I just needed to listen to a port and visit the website. <br>
And that is how I got the reverse shell to work. <br>
Command: **ncat -lpvn (port)** <br>


## 🛡️ SUID
A Set-User-ID means setting the rights for the program.
Okay, let me explain it differently!
1. Root creates a file and adds SUID.
2. Non-root user runs this file WITH root rights.

And this is how to escalate privileges when something is misconfigured! <br> <br>

# 💡 How I solved the room

**⚠️ Way-in** <br>
The website that was running on the server was very cool-looking, but there wasn't any way in. <br>
Then I checked the robots.txt, and it showed:
```
key-1-of-3.txt
fsocity.dic
```
So my next step was looking at `http://(ip)/key-1-of-3.txt`, and there was the first flag. <br>
After finding the first flag, I had to take a look at `http://(ip)/fsocity.dic`, which was just a website full of words.

**ℹ️ Login** <br>
I had to search a bit to find out it was running WordPress, and then I had to try out the login. <br>
But because I already knew how to use Hydra, it was pretty simple. <br>
There was just one thing: what wordlist should I use to guess the password? <br>
And after a few minutes, I thought about using the fsocity.dic, so I copied the file onto the VM. It was very laggy, and it took a while. <br>
Hydra also didn't like the file. It said that it would take about 5 hours. That's when I had to ask the THM-AI if that could be true. <br>
The AI's response was saying that I had many duplicates inside that file. I should use `sort -u fsocity.dic -o fsocity_uniq.txt`. <br>
What the command does is remove duplicates and then save the file into a new one. I should also use .txt instead of .dic. <br>
After a while, it had the password and the username. I logged in, and there it was: a WordPress admin site. <br>

**🏗️ Creating the Reverse Shell** <br>
Now that I got admin access, I just needed a way inside the server. I had to do some research. <br>
What I found had me laughing: I could edit a page and put in a **reverse shell script**. <br>
Then the website just had to save the file. Now I needed to listen to the port that I used in the reverse shell. <br>
Command: **ncat -lpvn (port)** <br>

**🚩 Second Flag** <br>
The reverse shell worked very well, and within seconds, I had the second flag sitting inside `/home/robot/key-2-of-3.txt`.<br>
At least, that's what I thought would happen. But NO, it was only accessible to root. <br>
So I spawned a new CMD. Command: `python3 -c 'import pty; pty.spawn("/bin/bash")'` because otherwise, it didn't let me log in as the robot user.
After spawning the new CMD, I tried to log in as robot with the decrypted MD5 hash I found. It was easy to find because it was lying in the same directory as key-2-of-3.txt.

**💥 Escalating Privileges** <br>
But now I had to escalate my privileges to root. After using `find / -perm -6000 -type f 2>/dev/null | grep 'bin/'`, I saw nmap in the list. <br>
Using https://gtfobins.org/gtfobins/nmap/, I saw how to escalate with nmap, and yep, it worked very easily. <br>
The last command was `ls /root`, and there it was, the last key. <br>
<br>

# 🛡️How could this be prevented?
It is pretty simple, do not leave any sensitive infomation inside the robots.txt but that isn't the main problem<br>
The main problem is that both of those files where publicy reachable! <br>
And also make sure to only use SUID when it is actually needed!
