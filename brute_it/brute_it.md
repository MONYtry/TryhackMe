# Room: Brute It <img src="/images/bruteit.jpg" alt="TryHearthMeImage" width="50" height="50">


**Infos:** <br>
Difficulty: easy<br>
Est. Time: 45min<br>
Task: Brute access, hash cracking and  escalate privileges.<br>
👉 Link: https://tryhackme.com/room/bruteit <br>
<br> 
<br>
# 📖 Things that I learned:
## 🐍 Hydra
Hydra is a tool for bruting web-applications, it is very easy and should not be used against real projects!
Command:
```
hydra -l (loginUserName) -P /usr/share/wordlists/rockyou.txt (ip) http-post-form '/(sub-domain)/:(userInputField)=^USER^&(userInputField)=^PASS^:F=Username or password invalid' -t 4
```
| Input | explanation |
|-------|-------------|
| loginUserName | stands for the username that is already known for the login |
| InputField | is the html classe that Hydra searches for on the Website |
| F= | the text that will show up if the login fails |

But why do we even have to enter the **F= value**, it will be searched by hydra to check if it failed or not
<br>

## 🛡️SSH2JOHN
SSH2John is used for making a Hash out of a encrpyted SSH-Key (id_rsa oder id_ed25519). <br>
Save the file somewhere with the SSH-Key inside of it command:  `nano id_rsa (paste in the key)`<br>
Create an hash out of it: 
```
python3 ssh2john.py (fileName) > (fileName).hash 
```
***Quick reminder that .hash isn't needed, I did that to keep track of my files and understand what I'm doing**
<br>
<br>
## 💥 John the Ripper
A tool made for brute-forcing passwords with a wordlist
For example lets say you want to know the password to something you would just type
```
john (fileName) --wordlist=/usr/share/wordlists/rockyou.txt
```
| Input | explanation |
|-------|-------------|
| (fileName) | file that gets checked |
| --wordlist=(path) | is just the path the tools uses |

## Privilege Escalation
Privilege Escalation often means finding a way to get access to higher permissions. <br>
Often possable because of bad configuration within the server <br>
<br>
<br>
# 💡 How I solved the room
**⚠️ Nmap** <br>
In the begining I had to do reconnaissence of the target.<br>
I had to use Nmap and see how many ports are open, also what service is using it.<br>
Then I needed to get infomations about the hole Server as SSH-Version, Apache-Version and OS.<br>
<br>
**🔎 Gobuster**<br>
One of the tasks was finding the hidden directory within **port 80** which was running an basic http-service.<br>
I scanned with gobuster the port and it found the subdomains:
- /admin

Then after it found the hidden subdomain I used curl -i http://(ip):80/admin, and I had to laugh a bit because there was an HTML comment
```
<!--- Remember the login-username was admin ---!>.
```
Now the last thing to do was getting the password, I googled how to crack passwords on a website. <br>
I learned about Hyrda. And as soon as I understood how to use it, I was logged in as Admin in a minute.

**♻️ SSH2John** <br>
The admin-page showed me an SSH-Key that I couldn't use. Thats when the AI from THM said that I should use SSH2John.<br>
So what I did was copying the SSH-Key into a file then I used SSH2John and I've got an Hash that John-The-Ripper could use to crack the password.<br>
And BOOM I've successfully granted access to the SSH-Server.<br>
<br>
**💥 Privilege Escalation**<br>
The command sudo -l showed me that I could use **/bin/cat** with **root rights** but without being root or having to use an password. <br>
Because cat had root rights I easily could read files like **/etc/shadow** <- there where passwords stored which also contained the root-password, but they where als in encrypted Hashes thats why I used <br>
my beloved John-The-Ripper, then I've had to login as root and yes I've been granted access to the root-account<br>

**ℹ️ Info** In **/etc/shadow** are passwords stored, but they where als in encrypted Hashes <br>
thats why i used my beloved John-The-Ripper, then I've had to login as root and yes I've been granted access to the root-account<br> <br> <br>

# 🛡️ How could this be prevented?
First step is to having an anti-bruteforce system inside the admin-login.
Second step is not to leak any login-credentails especialy for SSH.
Last and the most important step is to secure your user-rights, make sure do not leave any way to ROOT-Access within the system!
<br>
<br>

## 👨‍💻About me
I think this was the hardest but also the most rewarding room in the last days, I'm constantly learning and this room teached me a lot. <br>
My skill-set is now capable of tools like:
- nmap
- gobuster
- hydra
- SSH2John
- JohnTheRipper

Thanks for reading all of this, I hope my gramatic isn't too bad haha see'ya
