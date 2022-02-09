Urbino`s University - Applied computer science - Programming languages and software verification.

# Aim


# Summary   

### Actors Modified:
- The Client has been modified adding a boolean varaible named "Safety", this variable rappresent if the Client is positioned into a good or bad zone. If the Client is into the bad zone the Mules could decide to not accept the Client's message.
- The Mules has been modified adding a boolean variable named "BlackList" and a variable named "decision", the first variable modelling the secure concept of Mules, hence the Client can refused to accept the Mule that is into the black list. The Second varible rapresent if the Mule had acepted the Client's message or not. 

### WorkFlow implemented:
1. At the begining the Mules start to walk randomly between the Client and the Proxy. 
2. If the Client has a message to deliver, switches itself to request mode and waits the arriving of a Mule in way to deliver the message.
3. When a Mule arriving to the Client zone, it checks if the Client has to deliver a message, if the checkin is positive, the Mule starts to talk with the Client.
4. If the Mule is 'black listed' the client could choose to not hire him to send the message. 
5. If the Client is into the bad zone, the Mule could choose to accepted or not the Client's message.
6. If the Mule had accepted the message, the Client pays the Mule,then the Mule starts to walking randomly until to reach the Proxy  otherwise the Mule starts to walking randomly without a targhet. 
7. In this moment if the Mule hired from the Client losts the message (the probability to lost the message chaghe if the Mule had accepted a message from a not secure client), then the Mule come be 'black listed'. 
8. If a Mule with the Client's message reach the Proxy zone, the Mule delivers the message to Proxy, at the end the Mule returns to walk randomly.
9. If the Mule that delivered the message to Proxy was 'black listed', that Mule come be 'white listed'.
10. When the Proxy receives the messagge, delivers it to the Server and waits the answer of it.
11. When the Server receives the message from the Proxy, it generates the message answer to deliver at Proxy.
12. When the Proxy receives the answer from the server, switches it self in requesting mode and waits the arriving of a mule. 
13. When a Mule arriving to the proxy zone, it checks if the Proxy has to deliver a message, if the checkin is positive, the Proxy deliver the answer to the Mule.
14. The Mule starts to walking randomly, if during the attempt to reach the Clien, the Mule losts the Proxy's message, the mule come be 'black listed'.
15. If the Mule reach the Client's zone with the message, the mule delivers the answer to Client and come back to be 'white listed', after, the Client pays the Mule, at the end the Mule returns to walk randomly.

### Properties implemented:

## Autors 
- Francesco Rossi #298356
- Francesco Rombaldoni #306249
