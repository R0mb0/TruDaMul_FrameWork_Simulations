Urbino`s University - Applied computer science - Programming languages and software verification.

# Aim
The aim is to provide a very base working implementation of the framework from which implement the other specifc framework case to test.  

# Summary   

### Actors Implemented:

- A Client that could interact with the mules.
- Two Mules which know their identification and can interact with the Client and the Proxy. 
- A Proxy that can interact with the mules and the server.
- A Server that can interact with the proxy.

### WorkFlow Implemented:
1. At the begining the Mules start to walk randomly between the Client and the Proxy. 
2. If the Client has a message to deliver, switches itself to request mode and waits the arriving of a Mule in way to deliver the message.
3. When a Mule arriving to the Client zone, it checks if the Client has to deliver a message, if the checkin is positive, also the Client pays the Mule and delivers the message to it.
4. The Mule walks randomly unti to reach the Proxy.
5. The Mule delivers the Client's message to Proxy, at the end the Mule returns to walk randomly.
6. When the Proxy receives the messagge, delivers it to the Server and waits the answer of it.
7. When the Server receives the message from the Proxy, it generates the message answer to deliver at Proxy.
8. When the Proxy receives the answer from the server, switches it self in requesting mode and waits the arriving of a mule. 
9. When a Mule arriving to the proxy zone, it checks if the Proxy has to deliver a message, if the checkin is positive, the Proxy deliver the answer to the Mule.
10. The Mule walks randomly until to reach the Client.
11. The Mule delivers the answer to Client, after, the Client pays the Mule, at the end the Mule returns to walk randomly.

### Properties implemented:
- If the Client's request will be always accomplished. 
- If the Client's wallet can have a negative value.
- If during the esecution always a Mule will be selected to deliver the Client's messages.
- If the Client's request can remain unheard by the Mules.

## Autors 
- Francesco Rossi #298356
- Francesco Rombaldoni #306249
