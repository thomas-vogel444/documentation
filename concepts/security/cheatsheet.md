# Cheatsheet

From https://www.sslshopper.com/article-most-common-openssl-commands.html

## Generate keys

Generate a private key encrypted with a password.
```
openssl genrsa -des3 -out private.pem 2048
```

Generate the public key from a private key
```
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```

Export the RSA private key to a file (same as above without the -pubout flag)
```
openssl rsa -in private.pem -outform PEM -out unencrypted_private.pem
```

View the public key
```
openssl rsa -inform PEM -pubin -in public.pem
```

## Generate CSR

Generate a new private key and CSR
```
openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr
```



## Signing

Self signing a CSR


Signing a CSR with a given private key




openssl x509 -in cert.crt -text -noout

## Encrypt && Decrypt a file with a password

As a binary file
```bash
# Encrypt
openssl enc -aes-256-cbc -salt -in {input-filename} -out {output-filename}

# Decrypt
openssl enc -aes-256-cbc -d -in {input-filename} -out {output-filename}
```

As a base64 encoded file
```bash
# Encrypt
openssl enc -aes-256-cbc -a -in {input-filename} -out {output-filename}

# Decrypt
openssl enc -aes-256 -d -a -in {input-filename} -out {output-filename}
```

## Base64 Encode and Decode

```bash
# encode
openssl base64 -in {input-filename} -out {output-filename}

# Decode
openssl base64 -d -in {input-filename} -out {output-filename}
```