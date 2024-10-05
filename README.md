[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/R0mb0/TruDaMul_FrameWork_Simulations)
[![Open Source Love svg3](https://badges.frapsoft.com/os/v3/open-source.svg?v=103)](https://github.com/R0mb0/TruDaMul_FrameWork_Simulations)
[![Donate](https://img.shields.io/badge/PayPal-Donate%20to%20Author-blue.svg)](http://paypal.me/R0mb0)

Urbino`s University - Applied computer science - Programming languages and software verification.  

# Basic Implementation of TruDaMul Framework.

# Simple Definition of TruDaMul Framework.  

## TruDaMul Framework Targhet.

The rise of Internet-of-Things enables the development of smart applications devoted to improving the quality of life in urban and rural areas, thus fostering the creation of smart territories.  
Some dislocated areas, however, are underprivileged in the provision of such smart services due to the lack, inefficiency, or excessive cost of Internet access.
The TruDaMul Framework is able to carry data from an offline source to an online destination, relying on an untrusted Data Mule to carry the message through the two areas.  
In particular the Framework enables communication between different actors and a reward mechanism for their work, based on the use of Distributed Ledger Technologies, Smart Contracts and Decentralized File Storages.  


## TruDaMul Requirements.  

### Data Mules.  

Data Mules (that is an acronym for Mobile Ubiquitous LAN Extensions) are mobile devices that consist of a storage device and a short-range wireless communication medium (e.g. Wi-Fi or Bluetooth) and can exchange data to/from a nearby static sensor or access point that they encounter. As a result of their movement between remote areas, they effectively create a data communication link.  
Data Mules allow for communication and data transfer even in the absence of Internet, and they can be important tools for the functioning of applications concerning the Internet-of-Things (IoT).  

### Distributed Ledger Technologies.  

DLTs consist of a network of nodes that maintain a distributed ledger following the same protocol and, in the case of the blockchain, the ledger is organized into chronologically ordered blocks where each block is sequentially linked to the previous one.
The DLTs are composed of this protocols:  

#### 1.Smart Contracts.  
Smart Contracts are instructions stored in the blockchain and automatically triggered once the default condition is met.  
The use of Smart Contracts allows anyone to employ DLTs to operate beyond just currency transactions.  
For instance, the creation of smart services based on Smart Contracts may enable users to interact with devices/vehicles present in smart transportation systems and may also improve the interoperability among the devices and resources of Smart Cities.  

#### 2.State Channels for Services Payments.  
State channels have been introduced to provide rapid DLT payments without the need to store all transactions on-chain, i.e. directly on the ledger, but mostly off-chain, i.e. outside of the ledger. The state channels protocol can be summarized in a few steps:  

- Opening Channel - A user U opens a new state channel in a Smart Contract, by depositing an amount of the same money and indicating the other channel party, V.  

- Updating Balance - Both U and V , now, can communicate off-chain by exchanging digitally signed balance messages. These messages are used to update a balance value between U and V , i.e. if U has to pay V then the balance increases, otherwise the balance decreases.  

- Closing Channel - Both U or V can close the state channel at any time. The corresponding Smart Contract method needs the copy of the last balance message exchanged and the signature of both parties. Finally, the balance value is deducted from U`s deposit in favor of V, while the remaining part is sent to U.  

![Example:](https://github.com/R0mb0/TruDaMul_FrameWork_Simulations/blob/main/ReadMe_Images/Scheme.png)

#### 3.Decentralized File Storages and Content Addressing.  
Decentralized File Storages (DFS) enable a content-based addressing approach, where the users, rather than establishing a connection with a Server, query the network asking for specific items.  

## TruDaMul Actors.  
The simplest TruDaMul case is composed of:

- A Client (C) that find itself in a offline condiction.  

- A Server (S) that is in a online condiction.  

- A Proxy (P) that can comuncate with the server.  

- Two Data Mules (M) that can bring the Client message to Proxy.  

#### Interaction Example.  

A Client (C) that finds itself in an offline condition (e.g. it is in a no broadband connection area), to send a message to a Server (S) that is online, uses one of two Data Mules (M), which takes care of retrieving (offline) the payload of C and forwarding it to a Proxy (P), which in turn forwards (online) the message to the Server (S). P then sends back a possible response through another (or
possibly the same) Mule.  

## TruDaMul Framework Workflow Client-Server Forward Direction.  

1. When a Mule, M1, passes nearby C, it receives a request containing the payload dimension (in byte) and the money offered for the job. An automated negotiation thread may happen here, for the price C is willing to pay to M1 for the job to be done.  

2. Then C transmits to M1 the following objects:  
	- The payload pC.  
	- A tender object, signed by C.  
	- A balance object, signed by C, that updates the balance between C and M1 in their state channel.  
	- A address signed by C.  

3. Once M1 becomes online, it can directly announce the tender using the tender signed by C, in order to reach an audience of Proxie. This process happens in a dedicated announcement service.  

4. Before (or while) announcing the tender, M1 also uploads the payload pC to the DFS.

5. The Proxy P, after checking the integrity of the tender signed by C, decides to take charge of it, simply uses a method from the TruDaMul Smart Contract owned by C. The submitTender method:  

	* Requires as parameters:  
		- The tender object.  
		- The signature of tender.  
		- Address.  
		- And the signature of address.  

	* Automatically checks the validity of the signatures and locks the amount of money indicated by C in tender in favor of P.  

	* Allows M1 to close the state channel with C in the future, using the current balanceM1 object.  

6. P sends a signed request to the decentralized authorization service for accessing.

7. P can finally decrypt the payload pC (previously obtained from the DFS) and send the message.  

## TruDaMul Framework Workflow Server-Client Response Direction.  

1. P creates the new payload pS containing S’s response message.  

2. P creates a tender object with the information to respond to Client.   

3. Then tender is published in the announcement service. This announcement also requires the information about the location of C, extracted from the Client message, in order to allow a possible candidate Mule to know where to deliver.  

4. Mule M2 volunteers to take charge of tender P.  

5. M2 then sends a signed request to the decentralized authorization service.  

6. Once M2 reaches the vicinity of C, the former transmits to the latter tender together with a price request.  

7. Once C checks the validity of tenderP, it may start an automated negotiation thread with M2 for reaching an agreement on the price`s request.  

8. Since the presence of C signature is required for closing the channel using the balance M2 object (and thus getting paid), M2, once online, invokes the method submitPayment of the TruDaMul contract. This one requires address M2 signed by C to unlock the payment.  
	
## The Scope of this Work.  

The scope of this work is create a basic Implementation of "TruDaMul" framework, implementing the simplest TruDaMul case but simplifying the actors interactions.  
Later the implementation creates a specific test to check the system proprieties, for example protocol errors.  


## Project Credits.  
Mirko Zichichi<sup> * +</sup>, Luca Serena <sup> +</sup>, Stefano Ferretti<sup> #</sup>, Gabriele D’Angelo<sup> +</sup>  
<sup>*</sup> Ontology Engineering Group, Universidad Polit ecnica de Madrid, Spain  
<sup>+</sup> Department of Computer Science and Engineering, University of Bologna, Italy  
<sup>#</sup> Department of Pure and Applied Sciences, University of Urbino “Carlo Bo”, Italy  
mirko.zichichi@upm.es, luca.serena2@unibo.it, stefano.ferretti@uniurb.it, g.dangelo@unibo.it  

# Project Aim
The aim is to provide a very base working implementation of the framework from which implement the other specifc framework case to test.  

### Actors Implemented:

- A Client that could interact with the Mules. The Client is composed by: a varibles named "State" that rapresent the internal state of the Client, a variable named "wallet" that represent the Client's money that could be spent to hire the Mules, a variable named "Id" that is used to remeber the ids of the hired Mules and a boolean varaible named "Safety" that rappresent if the Client is positioned into a good or bad zone. In case of a Client positionated into a bad zone, the Mules could decide to not accept the Client's message.   
- Two Mules which know their identification and can interact with the Client and the Proxy. The Mules are composed by: a variable named "State" that rapresent the internal state of the Mules, a variable named "Wallet" that represent the earned Mules money, a boolean variable named "BlackList" and a variable named "decision", the first variable modelling the secure concept of Mules, hence the Client can refused to accept the Mule that is into the black list. The Second varible rapresent if the Mule had acepted the Client's message or not. 
- A Proxy that can interact with the mules and the server. The Proxy is composed by: a varibles named "State" that rapresent the internal state of the Proxy and a variable named "Id" that is used to remeber the ids of the hired Mules from Proxy.
- A Server that can interact with the proxy. The server is composed by a variable named "State" that rapresent the internal state of the Server.

### WorkFlow implemented:
1. At the begining the Mules start to walk randomly between the Client and the Proxy. 
2. If the Client has a message to deliver, switches itself to request mode and waits that arriving a Mule in way to deliver the message.
3. When a Mule arriving to the Client zone, it checks if the Client has to deliver a message, if the checkin is positive, the Mule starts to talk with the Client.
4. If the Mule is 'black listed' the client could choose to not hire him to send the message. 
5. If the Client is into the bad zone, the Mule could choose to accepted or not the Client's message.
6. If the Cient ha accepted the Mule and if the Mule had accepted the message, the Client pays the Mule,then the Mule starts to walking until to reach the Proxy  otherwise the Mule starts to walking randomly without a target. 
7. In this moment if the Mule hired from the Client losts the message (the probability to lost the message change if the Mule had accepted a message from a not secure Client), then the Mule come be 'black listed'. 
8. If a Mule with the Client's message reach the Proxy zone, the Mule delivers the message to Proxy, at the end the Mule returns to walk randomly.
9. If the Mule that delivered the message to Proxy was 'black listed', that Mule come be 'white listed'.
10. When the Proxy receives the messagge, delivers it to the Server and waits the answer of it.
11. When the Server receives the message from the Proxy, it generates the message answer, then deliver the answer to Proxy.
12. When the Proxy receives the answer from the server, switches itself in requesting mode and waits the arriving of a Mule. 
13. When a Mule arriving to the proxy zone, it checks if the Proxy has to deliver a message, if the checkin is positive, the Mule accept the answer message from Proxy.
14. The Mule starts to walking, if during the attempt to reach the Client, the Mule losts the Proxy's message, the mule come be 'black listed' (the probability to lost the message change if the Client to deliver the message is into the bad zone).
15. If the Mule reach the Client's zone with the message, the mule delivers the answer to Client and come back to be 'white listed', after, the Client pays the Mule, at the end the Mule returns to walk randomly.

### Properties implemented:
- If Both the Mules have the message in the same moment.
- If the Client's wallet can have negative value.
- If the Mule's wallet can exceed the value of 50.
- If a Mule's wallet can reach a value of 50 and the other Mule's wallet remain at 0.
- If both Mule's are going to Client in way to deliver the message.
- If both Mule's are going to Proxy in way to deliver the message.
- If the Client will always have a message to send.  
- If when the Mule has delivered the message, then will come back to walk randomly.
- If the Client is in the request mode, then its request will be examined by a Mule. 
- If the Client is in the request mode, the Client is into the safe zone and both the Mules aren't listed into the "black list",then the Client's request will be examined by a Mule.
-  If the Proxy is waiting a Mule, then its request will be examined by a Mule. 
-  If the Client is in the waiting mode, then it will receive the response.
-  If the Proxy forwards the message to the Server, then it will receive the response from the server. 
-  If the Mule is delivering the message, hence it has the message.
