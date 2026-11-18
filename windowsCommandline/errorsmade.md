# TryHackMe room: Windows-Commandline
Link: https://tryhackme.com/room/windowscommandline

It startes with basic SSH Connection but how do you actually Connect trough SSH?
I already explained it a bit in my Repo: https://github.com/MONYtry/Server/blob/main/tutorial.md

But here is an better explaination:
SSH stands for Secure-Shell, what it really means is it lets an administrator of an Network enter a Server without being physicly infront of it. (Like a Remote-Accses)

When you open up an Command-Interface and type in SSH admin@(ip) and press enter. 
It will ask you for an Fingerprint it tells the server who you are.
If you accept it the Server will never ask you again. 
Then you enter your password meanwhile the Server generated an Mathematicly correct and asyncron key that your PC already has as soon as the login is correct. It is mostly saved under Known Hosts.
Only if the public generated key is the same as the one on the server you will grant accses otherwise you will get a big error message saying that your key isnt correct or you are a MIT (Man-In-The-Middle Attacker)
Now we are inside of the SSH Connection, and with my knowladge it is not possible to read the Data-Flow between the User & Server. 

The Command `ver` stands for version of something.
If you type it in your CMD it will show you you're OS-Version.
Most programms use it, it is almost universal.

You want to find infomations about your system?
Try the Command `systeminfo` it will show things as
- User
- OS
- system32 path
- Physical RAM installed
- Timezone
- Network-Adapter and so much more!

Need the IP of a Windows-System, no problem!
`ipconfig` displays every inch of it
It displays things as:
- IPv4
- IPv6
- Subnet-Mask
- Standard Gateaway
But that isnt all because if you add an /all to ipconfig (`ipconfig/all`) it will show deeper infomations about your network
- MAC
- Your Network-Adapter
- DNS-Server
- DHCP-Server and if it is enabled

You want to know an IP / Hostname **EASY** use the Ping Command it will show you the Connection and the Hostname for example use
ping www.google.com
it will show something like this:
```
anwser from (ip): Bytes=32 Time=13ms TTL=119
anwser from (ip): Bytes=32 Time=12ms TTL=119
anwser from (ip): Bytes=32 Time=11ms TTL=119
anwser from (ip): Bytes=32 Time=12ms TTL=119

Ping-Statistic for (ip):
    Packets: Sent = 4, Recived = 4, Lost = 0
    (0% Lost),
Ca. Time in Millisec.:
    Minimum = 11ms, Maximum = 13ms, Middle-Value = 12ms`
```
Lets take a look at the message we've got.

time = how long it took to get a respone

TTL = Time to Live (in seconds) but why do we actually have this?
TTL is very smart because lets say you are searching for a pair of sockts but you cant find them, you dont wanna waste your day searching for them you just take a diffrent paire right?
Thats why TTL was invented because if a request wasnt recived it dies after about 120 seconds.

Sent = 4 means the one ping command sent four packets each packed with 32 Bytes
Recived = 4 means we got 4 as a reponse from the target.
Lost = 0 is very good it means that no packet was lost.
Time in Millisec just shows us the statistics wit an min-max and middle-value in our example it is very good!

You wanna know how many times your request / packet hops trough a network?
Use `tracert (target)`
Example: 
```
> tracert google.com
  1    <1 ms    <1 ms    <1 ms  192-168-178-1 [192.168.178.1]
  2    10 ms     8 ms     8 ms  192.0.0.1
  3    10 ms     8 ms     9 ms  (your ISP) [(ISP-IPv4)]
  4    13 ms    11 ms    11 ms  89.27.238.38
  5    13 ms    11 ms    12 ms  89.27.238.39
  6    13 ms    11 ms    11 ms  dia01s04-in-f14.1e100.net [142.251.141.14]
  ```
It shows you the current hop, min-max and middle-value and the current IP-Adress where your test packet is located at.

Nslookup stands for name-system-lookup and it basicly gives you tiny bits of infomation about.
You can enter the interactive mode with onlye using nslookup and work from there or you just type in your wanted infomation 
Example

| Usage | Explaination |
|-------|-------|
| -type=A | Shows you the IPv4 of the target |
| -type=AAAA | Shows you the IPv6 of the target |
| -type=AAAAA | Shows you both of the IPs from the target |
| -type=MX | Shows you the mail-server of the target |
| -type=NS | Shows you the Name-Server-Record of the target |

I have to sleep now!
netstat -abon

PID Mit Port dings notieren!

cd Wie bei linux
type (FileName) = cat (Filename)
tasklist 
tasklist /? = Help
tasklist /FI "imagename eq notepad.exe"
taskkill /PID (ProzessID)


https://tryhackme.com/room/windowscommandline?utm_campaign=social_share&utm_medium=social&utm_content=room&utm_source=copy&share_date=2026-11-18&sharerId=6a6db5f574ab7522182287ff
