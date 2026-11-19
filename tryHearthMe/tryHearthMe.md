# Room: TryHearthMe <img src="/images/tryHearthMe.png" alt="TryHearthMeImage" width="50" height="50">


**Infos:** <br>
Difficulty: easy<br>
Est. Time: 60min<br>
Task: Get admin acsses inside a Web-Shop.<br>
👉 Link: https://tryhackme.com/room/lafb2026e5 <br>
<br> <br>
# 📖 Things that I learned:
<br>

## Local-Storage
Local-Stroage is mostly used to save small data within the current website. As soon as you visit the website again the local-storage get loaded. <br>
For example if you are on a shopping-website and you add an item into your cart, it is the best way to save an JSON formated String inside your local Storage. <br>
It also helps to load websites faster (cache) <br> <br>
I learned to decode / encode **jwt Strings** because in the room the Login-Values where stored inside one. <br>
The source that I used: **https://www.jwt.io/** and it is insane I instantly understand it<br>
<br>
<br>

# 💡How I solved it
My first instinct was using gobuster and try to find hidden pages. <br>
Found subdomains:
- login
- admin
- logout
- register

As soon as admin popped up, my hearth was beating very fast because I felt that I'm able to solve it. <br> 
After looking at the JS Code, I was very confused but then it hit me, It had no reference to any database (For the login / register) <br>
It had to be localStorage because in the Login-Page I typed in a random email and it accepted it without even checking the provider or anything. <br>
The Local Storage had one entry but I didn't really know what to do so I replaced the current value with `admin=true`, and it broke. <br>
I had to ask AI what type of String it was because it wasn't readable for me and it told me that I should take a look at **jwt Tokens**, after that I searched for a Website and after I've found one the hole problem was solved and within 3 minutes I had admin privileges<br>
<br>
After I've got the admin rights I looked around and found a suspicous Item in the Webshop it was called ItemFlag. The description was the Flag.
This is how I hacked the Webshop at TryHearthMe on TryHackMe


# 🛡️How could this be prevented?
Instead of saving any login-credentials inside the local-storage the page-owner should have made a database with encrypted account credentials. <br>
**Keep in mind, dont use Local-Storage for Login-Credentials or any important data!** <br>
Stay safe
<p align="center">Thanks for reading all of this, I'm trying to make better doucmentations 🚀</p>
