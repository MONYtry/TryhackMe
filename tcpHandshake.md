# 3-Way TCP Handshake

First up what really is the Handshake and why do we even use it?
TCP Handshake was invented by a very smart person named **Robert Kahn in 1973**
TCP Handshake makes sure to only send Data when both Server and client are ready and reachable

# How does the Handshake work?
When you leave you're house you always check if you have the keys and when you dont have them you search them before going out.
same way with the Handshake
When you visit a wesbsite you browser sends a SYN Packet to the target Server
Then the server responds with a SYN ACK Packet
After that you browser say ACK and only after that the data can be sent / 

CLIENT - SYN 
`Server - SYN ACK`
CLIENT - ACK =