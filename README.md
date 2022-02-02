Urbino`s University - Applied computer science - Programming languages and software verification.  

# TruDaMul Framework Basic Implementation.

# TruDaMul Simple Definiction.  

The rise of Internet-of-Things enables the development of smart applications devoted to improving the quality of life in urban and rural areas, thus fostering the creation of smart territories.  
Some dislocated areas, however, are underprivileged in the provision of such smart services due to the lack, inefficiency, or excessive cost of Internet access.
The TruDaMul Framework permit to carry data from an offline source to an online destination, relying an untrusted Data Mule to carry the message through the two areas.  
In particular the Framework enables communication between different actors and a reward mechanism for their work, based on the use of Distributed Ledger Technologies, Smart Contracts and Decentralized File Storages.  


## TruDaMul Requirements.  

### Data Mules.  

Data Mules (that is an acronym for Mobile Ubiquitous LAN Extensions) are mobile devices that consist of a storage device and a short-range wireless communication medium (e.g. Wi-Fi or Bluetooth) and can exchange data to/from a nearby static sensor or access point that they encounter. As a result of their movement between remote areas, they effectively create a data communication link.  
Data Mules allow for communication and data transfer even in the absence of Internet, and they can be important tools for the functioning of applications concerning the Internet-of-Things (IoT).

### Distributed Ledger Technologies.  

DLTs consist of a network of nodes that maintain a distributed ledger following the same protocol and, in the case of the blockchain, the ledger is organized into chronologically ordered blocks where each block is sequentially linked to the previous one.

#### Block: Smart Contracts.  
Smart Contracts are instructions stored in the blockchain and automatically triggered once the default condition is met.  
The use of Smart Contracts allows anyone to employ DLTs to operate well beyond just currency transactions.  
For instance, the creation of smart services, based on Smart Contracts, may enable users to interact with devices/vehicles present in smart
transportation systems or to favor the interoperability among the devices and resources of Smart Cities.  

#### Block: State Channels for Services Payments.  
State channels
have been introduced to provide rapid DLT payments without
the need to store all transactions on-chain, i.e. directly on the
ledger, but mostly off-chain, i.e. outside of the ledger. The
state channels protocol can be summarized in a few steps:  

- Opening Channel - A user U opens a new state channel in a Smart Contract, by depositing an amount of the same token and indicating the other channel party, V .  

- Updating Balance - Both U and V , now, can communicate off-chain by exchanging digitally signed balance messages. These messages are used to update a balance value between U and V , i.e. if U has to pay V then the balance increases, otherwise the balance decreases.  

- Closing Channel - Both U or V can close the state channel at any time. The corresponding Smart Contract method needs the copy of the last balance message exchanged and the signature of both parties. Finally, the balance value is deduced from U’s deposit in favor of V , while the remaining part is sent to U.  

![Example:](https://github.com/R0mb0/TruDaMul_FrameWork_Simulations/blob/main/ReadMe_Images/BackGround_and_Related_Work.png)

#### Block: Decentralized File Storages and Content Addressing.  
Decentralized File Storages (DFS) enable a content-based addressing approach, where the users, rather than establishing a connection with a Server, query the network asking for specific items.  

## TruDaMul Actors.  
The simplest TruDaMul case is composed of:

- A Client (C) that find itself in a offline condiction.  

- A Server (S) that is in a online condiction.  

- A Proxy (P) that can comuncate with the server.  

- Two Data Mules (M) that can bring the Client message to Proxy.  

#### Interaction Example.  

A Client (C) that finds itself in an offline condition (e.g. it is in a no broadband connection area), to send a message to a Server (S) that is online, uses one of two Data Mules (M), which takes care of retrieving (offline) the payload of C and bringing it to a Proxy (P),
which in turn forwards (online) the message to the Server (S). P, then, sends back a possible response through another (or,
possibly, the same) Mule.  

## TruDaMul Framework Workflow Client-Server Forward Direction.  

1. When a Mule, M1, passes nearby C, it receives a request containing the payload dimension (in byte) and the money offered for the job. An automated negotiation thread may happen here, for the price C is willing to pay to M1 for the job to be done.  

2. Then C transmits to M1 the following objects:  
	- The payload pC.  
	- A tender object, signed by C.  
	- A balance object, signed by C, that updates the balance between C and M1 in their state channel.  
	- A address signed by C.  

3. Once M1 becomes online, it can directly announce the tender using the tender signed by C, in order to reach an audience of Proxie. This process happens in a dedicated announcement service.  

4. Before (or while) announcing the tender, M1 also uploads the payload pC to the DFS.

5. The Proxy P, after checkeds the integrity of the tender signed by C, decideds to take charge it,
simply invokes a method in the TruDaMul Smart Contract owned by C. The submitTender method:  

	* Requires as parameters:  
		- The tender object.  
		- The signature of tender.  
		- Address.  
		- And the signature of address.  

	* Automatically checks the validity of the signatures and locks the amount of tokens indicated by C in tender in favor of P.  

	* Allows M1 to close the state channel with C in the future, using the current balanceM1 object.  

6. P sends a signed request to the decentralized authorization service for accessing.

7. P can finally decrypt the payload pC (previously obtained from the DFS) and send the message.  

## TruDaMul Framework Workflow Server-Client Response Direction.  

1. P creates the new payload pS containing S’s response message.  

2. P creates a tender object with the information to respond to Client.   

3. Then tender  is published in the announcement service. This announcement also requires the information about the location of C, extracted from the Client messagge, in order to allow a possible candidate Mule to know where to deliver.  

4. a Mule, M2, wants to take charge of tenderP.  

5. M2 then sends a signed request to the decentralized authorization service.  

6. Once M2 reaches the vicinity of C, the former transmits to the latter tender together with a price request.  

7. Once C checks the validity of tenderP , it may start an automated negotiation thread with M2 for reaching an agreement on the price’s request.  

8. Since the presence of C signature is required for closing the channel using the balanceM2 object (and thus getting paid), then M2, once online.  
	
## The Scope of this Work.  

The scope of this work is create a basic Implementation of "TruDaMul" framework, implementing the simplest TruDaMul case but simplifying the actors interations.  
Later the implementation, create a specific test, in way to chek the system propeties, likes the protocol errors. 


## Project Credits.  
Mirko Zichichi y, Luca Serenay, Stefano Ferrettiz, Gabriele D’Angeloy  
Ontology Engineering Group, Universidad Polit ecnica de Madrid, Spain  
yDepartment of Computer Science and Engineering, University of Bologna, Italy  
zDepartment of Pure and Applied Sciences, University of Urbino “Carlo Bo”, Italy  
mirko.zichichi@upm.es, luca.serena2@unibo.it, stefano.ferretti@uniurb.it, g.dangelo@unibo.it  
