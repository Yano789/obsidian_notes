A Certificate Authority (CA) is a **trusted** entity responsible for issuing digital certificates that verify the identities of individuals, organizations, or devices on the internet. These certificates bind cryptographic keys to entities, ensuring **secure communication** through protocols like SSL/TLS by validating the authenticity of parties and enabling encrypted data exchange.

![|722x383](https://natalieagus.github.io/50005//docs/NS/images/05-network-security-app/2024-05-02-22-00-46.png)

The steps goes as follows:

- A has to obtain a **certificate** from trusted CA
    - As shown in the figure above, a certificate contains: **public key**, **identity information**, **issuer information**, **validity period**, and more
    - Refer to [Appendix](https://natalieagus.github.io/50005/ns/05-network-security-app#certificate) if you’d like to find out more
- CA **verifies** that A exists, checks A’s documents etc
- CA **issues a certificate** that the Public Key of A indeed belongs to A
- This certificate is **signed** by CA’s **private** key
- CA’s public key is **widely** known, so we trust that nobody can impersonate the CA
- B can obtain A’s public key from the certificate by decrypting it using the CA’s widely known public key

> How is CA’s public key widely known?
> 
> CA’s certificates (also known as Root certificates) containing CA’s public key are typically pre-installed with both web browsers and operating systems, providing users with a trusted foundation for validating SSL/TLS certificates during secure internet communication. This inclusion ensures that users can securely access websites and services without needing to manually manage trust settings.
> 
> The client (e.g., web browser) verifies the SSL/TLS certificate’s validity by checking if it’s signed by a trusted root certificate. If the certificate chain can be traced back to a root certificate stored in the client’s trust store, the certificate is considered valid.
> 
> This analogous to us trusting government-issued ID.

To this end, A CA obviously has to be a trusted entity such as: government (e.g., IDA) or well known provider. Real-life examples of trusted CAs are: **IdenTrust, Comodo, GlobalSign, DigiCert, GoDaddy**, and many more. Modern browsers will warn you if some website’s certificates are not verified. Below is an example of a legal certificate of netflix.com’s public key, signed by DigiCert as its CA.