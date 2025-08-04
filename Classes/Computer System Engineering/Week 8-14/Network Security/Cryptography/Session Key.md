We use public-key [[Cryptography]] to establish a secure connection, meaning that we authenticate (the identity of) our host. Then, one party will generate **symmetric session key** and exchange between sender and receiver using public-key cryptography.

We then use this symmetric session key (instead of the public key) for the subsequent message exchanges throughout the session.