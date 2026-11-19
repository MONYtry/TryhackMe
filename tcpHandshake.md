# 👋 3-Way TCP Handshake

First up what really is the Handshake and why do we even use it?<br>
TCP was invented by a few very smart people in the **1970's**<br>
TCP Handshake makes sure to only send Data when both Server and client are ready and reachable <br>
Because when it wouldn't we would be using UDP (User Datagram Protocol)
More about UDP, **Link: Coming soon!**

## 💡 How does the Handshake work?
When you leave you're house you always check if you have the keys.<br>
same way with the Handshake<br>
<br>
## 👷 Building the Connection between Server - Client
When you visit a wesbsite you browser sends a **SYN Packet** to the target Server
Then the server responds with a **SYN ACK Packet**
After that you browser responds with a **ACK Packet** and only after that the data can be sent 

visualization:
```
CLIENT -> SYN -> SERVER 
Server -> SYN ACK -> CLIENT
CLIENT -> ACK -> SERVER 
```


## 💥 Breaking the connection between Server - Client
If you want to stop a TCP-Connection you will be doing the opposit of the first handshake!<br>
visualization:
```
CLIENT -> FIN -> SERVER 
Server -> ACK FIN -> CLIENT
CLIENT -> ACK -> SERVER 
```
