# TLS

## TLS Basics

### What is a certificate

* A certificate is used to guarantee trust between two parties during a transaction.
* For example, when a user tries to access a web server, TLS certificates ensure that
the communication between the user and the server is encrypted and the server is who it says it is.

### What is TLS

* TLS stands for transport layer security. It is a cryptographic protocol that provides end-to-end security of data sent between applications over the Internet.
* TLS certificates ensure that the communication between the user and the server is encrypted and the server is who it says it is.

### What is a CA

* It stands for certificate authority
* They're well known organizations that can sign and validate your certificates for you.
* CA has its own set of public and private key pairs that it uses to sign server certificates.
* There are three types of certificates, including server certificates configured on the servers, root certificate configured on the CA servers, and the
 client certificates configured on the clients.

### Symmetric Encryption

* It uses a secret key that can either be a number, a word or a string of random letters.
* It encrypts and decrypts using the same secret key. 
* A sender encrypts the data with the public key and then send the encrypted data and the public key to the receiver. The receiver uses the public key to decrypt the data.
* The sender and the receiver should know the secret key that is used to encrypt and decrypt all the messages.

### Asymmetric Encryption

* It uses two keys, i.e. a public and a private key.
* A message encrypted with a public key can only be decrypted with the corresponding private key.
* We generate a public and private key pair on the receiver.
* A sender encrypts the data with the public key which is got from the receiver, and then sends the encrypted data to the receiver. The receiver descrypts the data with the private key.

### How TLS works

* The client device sends an initial message (Client Hello) to the destination server. It includes the version of TLS it supports as well as the cryptographic algorithms it supports (cipher suite).
* The server responds with a Server Hello message that includes its corresponding certificate with its public key.
* The client device verifies the server’s TLS certificate.
* The client device then creates a pre-master secret that’s encrypted using the public key.
* The server decrypts the pre-master secret with its own private key.
* Both the client device and server confirm that the process has been completed and have a symmetric (master) key that can now be used for encryption and decryption.
* The handshake uses asymmetric encryption. Once the process is complete, symmetric encryption is used to send data safely and securely.

## TLS in Kubernetes

There are three type of certificates below.

* root certificate configured on the CA servers
    * ca.key and ca.crt
* server certificates configured on the servers. Each server certificate has crt and key.
    * etcdserver
    * apiserver (kube-api server)
    * kubelet (kubelet server)
* client certificates configured on the clients
    * admin
    * scheduler
    * controller-manager 
    * kube-proxy
    * apiserver-kubelet-client
    * kubelet-client
* The process to create certificates is below.
    * generate keys (.key)
    ```
    openssl genrsa -out a.key 2048
    ```
    * certificate signing requests (.csr)
    ```
    openssl req -new -key a.key -subj "/CN=xxx-CA" -out b.csr
    ```
    * sign certificates (.crt and this is the cert.)
    ```
    openssl x509 -req -in b.csr -signkey a.key -out c.crt
    ```
* manage TLS certifictes in a cluster
    * Trusting TLS in a cluster
    * Requesting a certificate
        * create a certificate signing request
        * create a CertificateSigningRequest object to send to the Kubernetes API
        * get the CertificateSigningRequest approved
    * sign the CertificatesSigningRequest
        * create a certificate authority
        * issue a certificate
        * upload the signed certificate
    * download the certificate and use it


## View Certificate Details
### openssl commands
* The showcerts flag appended onto the openssl s_client and connect command, and show the entire certificate chain in PEM format.
```
openssl s_client -showcerts -connect <domain name>:port number
```
* The x509 command is a multi purpose certificate utility. It can be used to display certificate information. 
* The -text prints out the certificate in text form, , including its public key, signature algorithms, etc.
```
openssl s_client -showcerts -connect <domain name>:port number | openssl x509 -text
```
* The -noout flag is used to prevent the output of the encoded version of the request.
```
openssl req -in xx.csr -noout -text
```

## Misc

### base64 decode and encode

* Base64 is used to encode binary data 
* Base64 encode example

```bash
echo Hi | base64
```

The output is below.

```bash
SGkK
```

* Base64 decode example
```
echo SGkK | base64 -d
```
The output is below.
```
Hi
```

## References
* https://www.trentonsystems.com/blog/symmetric-vs-asymmetric-encryption
* https://www.digicert.com/how-tls-ssl-certificates-work
* https://sematext.com/glossary/ssl-tls-handshake/
* https://www.avast.com/c-what-is-transport-layer-security
* https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/
* https://pleasantpasswords.com/info/pleasant-password-server/b-server-configuration/3-installing-a-3rd-party-certificate/openssl-commands
* https://www.digicert.com/kb/ssl-support/openssl-quick-reference-guide.htm
* https://www.ibm.com/support/pages/qradar-how-verify-certifcate-connections-using-openssl
* https://www.freecodecamp.org/news/openssl-command-cheatsheet-b441be1e8c4a/
* https://www.sslshopper.com/article-most-common-openssl-commands.html
* https://www.freecodecamp.org/news/what-is-base64-encoding/
* https://www.redhat.com/sysadmin/base64-encoding