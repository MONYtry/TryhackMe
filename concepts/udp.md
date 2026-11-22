# 🌐 User Datagram Protocol (UDP)

What is UDP, **User-Datagram-Protocol** it was invented in **1980** <br>
It is a data transmission protocol which is good for live-streaming because UDP dosen't care if data was received successfully. <br>
And if you live-stream you rather want a skiped frame then waiting for the one frame to load. (<- <a href="https://github.com/MONYtry/TryhackMe/blob/main/tcpHandshake.md">TCP </a>)

# 💥 DoS / DDoS & UDP-Flooding

UDP is just sending out data, without guaranteed receiving or sequence that is why many **DoS** / **DDoS Attacks** use UDP because it is much better but why you ask? <br>
UDP dont need to check anything it just sends data. Thats also called **UDP-Flooding**.<br>
UDP-Flooding is just sending so many packets until the target can't keep up with the traffic.

# 🛡️ How can this be prevented?
Modern Servers & Websites use DDoS-Protection, Firewalls, Rate-Limiting which is good because providers like cloudflare are doing very good jobs because cloudflare handled an attack with <br>
**31.4 Tbps in late 2025** this is so much you could download **GTA VI** about 124 times per second!
<br><br>
More infomations: <a href="https://github.com/MONYtry/TryhackMe/blob/main/udp.md?plain=1">My Documentation about DDoS & Protection! </a>
