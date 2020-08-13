# Security
TLS - a certificate is to guarantee trust between two parties during a transaction
    - it ensure the transaction is secure and encrypted and the server says that who it is.

Symmetric Encryption - using one key to decrypt and encrypt the data between a client and web server transaction.
                     - not that secure because the attacker can still sniff the key and can decrypt the data during a transaction.

Asymmetric Encryption - instead of using a single key to encrypt and decrypt a data. Asymmetric encryption use a pair of keys
                        which is the public key and private key. A public key is the one that is expose to the public and it
                        decrypts the data and the private key is going to be use to decrypt the data. The private key should not
                        be shared to anyone it must be save in a secure environment.

Asymmetric Encryption

in order for you to access a server using an ssh you need to add the public key to the `~/.ssh/authorized_keys`
```bash
                                                            ________________________________________________
                                                            |                                               |
Client1                                                     |            _______________________            |        
PrivateKey1 Publickey1 -------------------------------------|---------->|     Server1           |           |
                                                                        |PublicKey1(has access) |           |
                                                                        |PublicKey2(has access) |           |
                                                                        |_______________________|           |
                                                                                ^                           |
                                                  ------------------------------|                           |
Client2                                           |                                                         |
PrivateKey1 PublicKey2 ---------------------------|                                                         |
                                                  |                                                         |
                                                  |                                                         |
                                                  |                      _______________________            |
                                                  |-------------------->|     Server2           |           |
                                                                        |PublicKey1(has access) |<----------|
                                                                        |PublicKey2(has access) |
                                                                        |_______________________|

```
### Quicknote for private and public key pair
A private key can encrypt the data too and only the public key can decrypt the data but if you encrypt a data
with a private key anyone can read the data because of the public key. If a public key encrypt the data the private key
can only decrypt the data if the private key encrypted the data the public key can only decrypt the data.

### To generate a `Certificate Signing Request(CSR)`

In order to have a legitimate certificate it needs to be signed by the CERTIFICATE AUTHORITY(CA)

```bash
openssl req -new -key ${key_name.key} -out ${csr_name.csr} -subj "/C=US/ST=CA/O=MyOrg, Inc./CN=my-bank.com"
#e.g.
openssl req -new -newkey rsa:2048 -nodes -keyout app01.key -out app01.csr

openssl req -new -key my-bank.key -out my-bank.csr -subj "/C=US/ST=CA/O=MyOrg, Inc./CN=my-bank.com"

#create own self signed certificate location for apache server
/etc/httpd/certs

#create own self signed certificate command
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout app01.key -out app01.crt

#ssl configuration for apache server location
/etc/httpd/conf.d/ssl.conf
```
## Certificate Authority

Every certificate authority has a private key and public key the public key is being save in the browser in order for the browser
to know if the certificate is legitimate.

### Location of the public key of the authorized Certificate Authority
Browsers Certificates Tab > Trusted Root Certification Authorities

## Public Key Infrastructure(PKI)
This whole infrastructure including the servers, the people, the Certificate Authority, distributing and maintaning
the digital certificates is known as Public Key Infrastructure(PKI).

## Best Practice for naming convention
Certificate(public key) is named *.crt and *.pem extensions
Private key  is named *.key or *-key.pem

