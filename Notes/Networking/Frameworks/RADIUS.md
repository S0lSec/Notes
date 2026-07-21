Remote Authentication Dial-in User Service is a network security protocol based on the client-server model.
- Clients can place requests to access services from any location
- Uses UDP to communicating between a NAS and RADIUS functions


RADIUS Client Server and Dial-In user interaction
1. A user places a PPP authentication request to the RADIUS Client, i.e., NAS.
2. The NAS asks for credentials like the username and password in case of a Password Authentication Protocol (PAP) or challenge in case of a Challenge Handshake Authentication Protocol (CHAP). 
3. The user supplies the credentials that are asked for.
4. The RADIUS client sends the encrypted credentials to the RADIUS server.
5. The RADIUS server throws a response in the form of Accept, Reject, or Challenge.
6. The RADIUS client provides access to services and user resources based on Accept or Reject parameters.