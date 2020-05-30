# Encrypting with openssl

From https://www.shellhacks.com/encrypt-decrypt-file-password-openssl/

## Encrypt or decrypt a file with password

Encrypting a file with a password.
```
openssl enc -aes-256-cbc -salt -in {input-filename} -out {output-filename}
```

Decrypting a password encrypted file.
```
openssl enc -aes-256-cbc -d -in {encrypted-file} -out {output-filename}
```

## Base64 Encode and Decode

Base64 encoding is used to translate binary data into ASCII characters for systems that cannot transmit binary data directly, e.g. over TCP.

By default encrypted data are in a binary format. It needs to be base64 encoded.

Encryption:
```
openssl enc -aes-256-cbc -salt -a -in {input-filename} -out {output-filename}
```

Decryption:
```
openssl enc -aes-256-cbc -d -a -in {encrypted-file} -out {output-filename}
```

To base64 encode a file:
```
openssl base64 -in {input-filename} -out {output-filename}
```

To base64 decode the file:
```
openssl base64 -d -in {encoded-filename} -out {output-filename}
```