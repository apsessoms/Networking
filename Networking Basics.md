![image](https://github.com/apsessoms/Networking/assets/99392512/7c252b0d-8261-4e6a-9f9b-910a7a9dcf02)

What if you have another network containing similiar devices connected to a switch? Are they able to communicate with eachother?

**How does a computer in Network A talk to a computer in Network B?**
![image](https://github.com/apsessoms/Networking/assets/99392512/62c8276a-5f44-473c-b3af-0c6c1beccc49)

If you said Switch, you were close! It is actually a **Router**. Routers help connect two networks together. It's able to connect to the two separate networks by having two different IPs assigned (one on each network). 
How do the computers know where the router is on the network? The systems will have to be configured with a gateway (or route) which takes you to the internet or other networks. The systems need to know where that "door" is to go through that. 

To see the exhisting route configuration on a system, type **route** into the command prompt to display the Kernels routing table. 

![image](https://github.com/apsessoms/Networking/assets/99392512/29d518cb-963b-4f3c-8967-d8bdabcabb54)

There are no routing configurations as of now, which means that the computers on the networks shown above will not be able to talk to eachother.

![image](https://github.com/apsessoms/Networking/assets/99392512/4218828f-ab0f-4230-aa0c-9fb65fa18d5f)

 To configure a gateway on Network B to reach a computer on Network A, run the "ip route add 192.168.1.0/24 via
192.168.2.1 (aka the gateway). 

![image](https://github.com/apsessoms/Networking/assets/99392512/45f4c94b-79a2-4cc4-8e32-e33a714c1129)

This must be done for all systems.  To configure a gateway on Network A to reach a computer on Network B, run the "ip route add 192.168.2.1/24 via
192.168.1.0 (aka the gateway). 
