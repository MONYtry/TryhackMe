# Hidden deep into my hearth
**Infos:** <br>
Difficulty: easy<br>
Est. Time: 60min<br>
👉Link: https://tryhackme.com/room/lafb2026e9 <br>
I was confused at the beginning because of the wierd message but then I dived into the room.
<br> <br> <br>
# 📖 Things that I learned:
<br>


## 🔎 Gobuster
Gobuster is a powerfull tool that helps you find subdomains / paths via. Wordlists <br>
Command: `gobuster dir -u (HyperText Transfer Protocol) -w (Path to a Wordlist.txt)` <br>
<br>
Explanation: <br>
**-u** stands for url <br>
**-w** stands for wordlist <br>
  
Then you might get some results about your target<br>
<br>

## 🌐 cURL
cURL is a CMD based command and i dont really find good Explanations about it but from my point of understanding <br>
the Command: `curl (url)`  <br>
just displays the HTML Code but it also can show headers with the argument -i  <br>
For more infomations just use `curl --help` it will show you much more! <br>
<br>
<br>
# 👨‍💻 How I've solved the Room
At the beginning I was checking open ports with Nmap.<br>
I found open ports as SSH and an website running on port 5000. <br> 
The website basiclly said nothing I looked at the robots.txt file and it showed me this <br>
```
User-agent: *
Disallow: /cupids_secret_vault/*
# cupid_arrow_2026!!!
```

After that I instantly checked the subdomains from the target
`gobuster dir -u (url) -w /usr/share/wordlist/dirb/common.txt`
<br>
No results were given but I remember the **robots.txt Disallow path**.<br>
Then I checked it again with **gobuster** and it found a path leading to **/administrator** <br>
<br>
Now I used the Command `curl -i (url):5000/cupids_secret_vault/administrator` <br>
A rush went through me that I've never felt before but it felt very good because the result was very unexpected. <br> 
It looked like a login page from the terminal so I jumped in the Browser. <br>
And my guess was correct it was a login page.<br>
After looking around for clues I didn't tried to login.<br>
<br>
Why didn't I instantly tried to login in?<br>
<br>
Because everything you do on the internet is getting logged and watched somewhere. It wouldn't be suspicious to login but in my head it makes sens to first look around and then try to login. (You never know who is watching)
After not finding anything important I tried to login with <br>
```
Username: admin 
Password: I used the comment from robots.txt
```
and BOOM i was successfully logged in as an admin. And that is how I completed the Room
