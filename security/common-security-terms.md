######################################################################
- SLL/TLS is the protocol for secure communication
- TLS handshake
    - Server sends the client a Public Key which the later uses for encrypting subsequent messages
    - The two negotionate on the best encryption algorithm to use.
    - A symmetric algorithm is chosen and the server send the client a symmetric Key
    - Normal HTTP communication entails encrypted with the symmetric key
- RSA: Public Key Encryption algorithm 
    - First generate a private key, then a public key based on the private key
        - .e.g. `openssl genrsa -out {private-key-filename} 2048`
            - 2048 is the size of the private key
        - `openssl rsa -pubout -in {private-key-filename} -out {public-key-filename}`
- PEM protocol (Privacy Enhanced Mail)
    - PEM is a text representation of the real binary key in DER format
        i.e. it is a base64 encoding of the DER format
- Digital Identity
    - SSL Certificates
- Public Key Infrastructure (PKI)
    - infrastructure/services created to manage digital certificates.
        - e.g. Certificate Authorities
- X.509
    - A digital certificate consists of a digital identity (identity information) and a public key
    - X.509 is the format for the certificate
        1) Version Number
        2) Serial Number
        3) Signature Algorithm ID 
        4) Issuer Name
        5) Validity Period
            - Not Before
            - Not After
        6) Subject Name
        7) Subject Public Key Info
            - Public Key Algorithm
            - Subject Public Key
        8) Issuer Unique Identifier (optional)
        9) Subject Unique Identifier (optional)
        10) Extensions (optional)
        11) Certificate Signature Algorithm
        12) Certificate Signature
- CSR: Certificate Signing Request
    - PEM formatted file with the following information
        - Common Name
        - Organization
        - Organizational Unit
        - City
        - State/County/Region
        - Country
        - Email Address
        - Public Key
    - e.g. `openssl req -new -sha256 -key privatekey.key -out request.csr
`
    openssl genrsa -out my-private-key 2048
    openssl rsa -pubout -in my-private-key -out my-private-key.pub