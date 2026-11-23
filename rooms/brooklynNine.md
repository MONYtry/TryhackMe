# Room: Brooklyn 99<img src="https://cdn-images.tryhackme.com/room-icons/95b2fab20e29a6d22d6191a789dcbe1f.jpeg" alt="Brooklyn Nine Nine-Icon" width="100" height="50">

**Infos:** <br>
Difficulty: medium<br>
Est. Time: 30min<br>
Task: Find two flags<br>
👉 Link: https://tryhackme.com/room/brooklynninenine<br>
<br>
<br>

# 📖 Things that I learned:

## 🔍 Nmap
I learned how important it is to use Nmap at the beginning of a penetration test. With `nmap -sV -sC (ip)`, I was able to discover open ports and the services running on them.

## 📂 FTP
I learned how easy it is to connect to an FTP server directly through the terminal. I had never logged into an FTP server this way before.

Command: `ftp (ip)`

I also learned that some FTP servers allow anonymous login, which can be a serious security risk if configured incorrectly.

## 🐉 Hydra and SSH
I already knew Hydra, but I didn't know that it could be used to crack SSH logins as well.

Command: `hydra -l (name) -P /usr/share/wordlists/rockyou.txt ssh://(ip)`

This was something new that genuinely surprised me!

## 🛡️ Privilege Escalation with LESS
I learned that the LESS command can be used to escalate privileges if it can be executed as root.

By using `sudo -l`, I discovered that I was allowed to execute LESS as root. With the command `!/bin/sh`, I was able to spawn a shell with root privileges.

# 💡 How I solved the room

**⚠️ Way-in** <br>
I started with an Nmap scan using `nmap -sV -sC (ip)`. The scan showed three interesting services: SSH, HTTP and FTP. <br>

My next step was to check the website running on the HTTP port. While inspecting the HTML source code, I found a comment asking if I knew what "steganography" was. <br>

Since I couldn't find anything else interesting on the website, I decided to investigate the FTP server. I had never logged into an FTP server through the terminal before, so I had to Google how to do it. Surprisingly, it was pretty easy! <br>

I used `ftp (ip)` and was asked for a username. During my Nmap scan, I had already noticed that anonymous login was available. So I tried the username `anonymous`. <br>

Now I needed a password. Remembering the strange comment on the website, I decided to use the word "steganography" as the password. And it worked! <br>

After successfully logging in, I searched through the FTP files and found the first flag. I also discovered a binary file, which I immediately tried to decode. Unfortunately, I couldn't get it to work. <br>

**ℹ️ Getting SSH Access** <br>
After trying to figure out the binary file, I decided to ask an AI for help. Unfortunately, it couldn't help me either. So I went back to Google. <br>

During my research, I learned something new: Hydra isn't only useful for cracking online logins. It can also be used to brute-force SSH passwords! <br>

I used the following command:

`hydra -l (name) -P /usr/share/wordlists/rockyou.txt ssh://(ip)`

And after a while, I successfully obtained SSH access! <br>

However, I was only logged in as a normal user, so I still needed to find a way to become root.

**💥 Escalating Privileges** <br>
My next step was using my favourite command: `sudo -l`. <br>

The output showed me something interesting: I was allowed to execute the LESS command as root. Unfortunately, I didn't know what I could do with that information, so I had to Google again. <br>

Eventually, I discovered that LESS can actually be used to spawn a shell! By executing:

`sudo /usr/bin/less /etc/profile`

I could enter the following command inside LESS:

`!/bin/sh`

And just like that, I had root privileges! I have to admit that I still don't fully understand why this works, but it was pretty impressive to discover. <br>

The final step was surprisingly simple. I navigated to `/root`, and there it was: the last flag! <br>
<br>

# 🛡️How could this be prevented?

There are several security issues that could have been prevented:

- **FTP:** Anonymous access should be disabled unless it is absolutely necessary. Sensitive files should never be publicly accessible.
- **SSH:** Use strong passwords or SSH keys instead of weak passwords that can be brute-forced with tools like Hydra.
- **Sudo permissions:** Never allow normal users to execute potentially dangerous programs like LESS as root without a good reason.

The biggest problem was the incorrect configuration of the services and permissions. Especially allowing LESS to run as root made privilege escalation incredibly easy.
