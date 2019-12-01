# Client Side SSL

From https://gist.github.com/mtigas/952344

## Using Self-Signed Certificate

### Create a Certificate Authority Root

```bash
# Generates a password protected RSA private key for the CA
openssl genrsa -aes256 -out ca.pass.key 4096 

# Removes the password protection
openssl rsa -in ca.pass.key -out ca.key

rm ca.pass.key
```

### Create the Client Key and CSR

```bash
CLIENT_ID="01-alice"
CLIENT_SERIAL=01

# Generate a RSA private key for the client
openssl genrsa -aes256 -out ${CLIENT_ID}.pass.key 4096
openssl rsa -in ${CLIENT_ID}.pass.key -out ${CLIENT_ID}.key
rm ${CLIENT_ID}.pass.key

# Generates a CSR with the client key
openssl req -new -key ${CLIENT_ID}.key -out ${CLIENT_ID}.csr

# Sign the certificate with the CA private key
openssl x509 -req -days 3650 -in ${CLIENT_ID}.csr -CA ca.pem -CAkey ca.key -set_serial ${CLIENT_SERIAL} -out ${CLIENT_ID}.pem

# Bundle the private key & cert for end-user client use
cat ${CLIENT_ID}.key ${CLIENT_ID}.pem ca.pem > ${CLIENT_ID}.full.pem
```

## Install CA certificate on NGINX

```
ssl_client_certificate /path/to/ca.pem;
ssl_verify_client optional; # or `on` if you require client key
```