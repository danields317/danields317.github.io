# SSL

Secure Socket Layer (SSL) is a technique to securely transmit data between computers.
:::info
In practice, the actual SSL protocol is not used anymore. It is mostly replaced by TLS. But it is still commonly called SSL since humans seem to like the name a lot.
:::

## Roles
Setting up SSL requires a few different parties to work together. Each party has their own role in the process.
- **Client** - Entity initiating the SSL handshake (e.g. web browser, IOT devices)
- **Server** - Entity recieving the SSL handshake (e.g. NginX, load balancer)
- **Certificate Authority** - A governing entity that issues SSL certificates.

:::tip
In 2021, five organizations handle the SSL security of ~98% of the internet.  
:::

## TLS Sequence
The TLS Sequence is the process between a Client and a Server which proves to the client that the server is who they say they are and a secure connection can be established.

1. A Certificate Authority has a Private Key and Public Key. The CA holds a self signed certificate containing the public key.
2. A Server generates its own Private Key and Public Key.
3. A Server generates a Certificate Signing Request (CSR), containing the server's Public Key and signed with the private key.
4. The CSR is send to the CA who will validate the CSR and the servers legitimacy.
5. CA creates a certificate based on the data in the CSR and signs it with its own Private Key.
6. CA hands over the certificate to the server.
7. Clients have pre-installed the CA self signed certificates in their browsers or OS.
8. Client makes a request to the server and receives the servers certificate.
9. The Client uses the installed CA Certificate Public key to decrypt the Server Certificate Signature to ensure the Server Certificate is indeed given from the CA.
10. The client encrypts a random value with the Server Public Key and sends it to the server. The server will decrypt it with the private key and send it back, proving it owns the certificate.

Now the client has validated that the certificate is valid since it was able to decrypt the signature with the CA public key. Proving the CA private key was used to create the signature.
And the client has validated that the server is the owner of the certificate since it is able to decrypt values encrypted with the public key. Proving it has the private key.
After this, the rest of the SSL process can continue to set up a safe tunnel to share further data securely.

:::note

Signing is the process of using a private key to prove legitimacy of a certificate.
The content of a certificate is encrypted with the private key and added to the certificate.
The recipient can then decrypt the signature with the public key.
If the content is the same, it proves the sender is in possesion of the private key.

:::

## CA validation
Certificate Authorities can validate the legitimacy of a CSR on both technical and opertional levels.

- Domain Validated (DV) - Confirms control over a website domain without verifying the identity of the site owner. DV certificates are suitable for internal or personal sites but not recommended for businesses.
- Organization Validated (OV) - Verifies the identity of the business behind the website, providing more trust for users. OV certificates are the standard for commercial and public-facing websites.
- Extended Validation (EV) - EV certificates offer the highest level of verification, displaying the organization’s name in the certificate details. They’re used by financial institutions, major eCommerce brands, and government agencies to establish maximum trust.

---

*References*
- [*Key Players of SSL & TLS: Client, Server, Certificate Authority (CA) - Practical TLS*](https://youtu.be/C7Y4UEBJ0Og?si=BTQSrCPc20FWdBIE)
- [*What is a certificate authority?*](https://www.digicert.com/blog/what-is-a-certificate-authority)
- [*TLS Handshake - EVERYTHING that happens when you visit an HTTPS website*](https://youtu.be/ZkL10eoG1PY?si=t-yolKJi5ILmiVeS)

