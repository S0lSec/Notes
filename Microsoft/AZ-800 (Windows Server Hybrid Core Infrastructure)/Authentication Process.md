1. User logs on and machine hashes password and encrypts a timestampt with it
2. Workstation sends the encrypted timestampt and your username to the KDC AUthentication Services
3. DC looks up your account in NTDS.dit and pulls your stored password hash and uses it to decrypt the timestamp send. If it decrypts and the timestamp is recent you're authenticated
4. The DC then replies with an Authentication Service Reply (AS-REP) containing a Ticket Granting TIcket encrypted with the krbtgt accounts hash and a session key encrypted with your hash
5. Your machine decrypts the session key and uses that to access resources

