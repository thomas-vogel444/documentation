# SSL Certificates

From https://sites.google.com/site/amitsciscozone/home/security/digital-certificates-explained

- A certificate is a digital form of identification, like a passport. It provides information about the identity of the entity
- A certificate is issued by a Certification Authority (CA).
- The user obtains the Public Key of the server from the digital certificate.

## Public Key Infrastructure

A Public Key Infrastructure (PKI) consists of protocols, standards, and services allowing users to authenticate to each other using certificates issued by a CA.

Standard formats for certificates:
- X.509
    - Format of the public key certificates
- PKI X.509
- Public Key Cryptography Standard (PKCS)
    - Format for CSRs

Standard formats for encoding:
- DER: binary format for certificates
- PEM: base64 format for certificates and keys
    - .pem
    - .cer/.crt for certificates
    - .key for keys

## Types of certificates

- Domain Validation (DV)
- Organization Validation (OV)
- Extended Validation (EV)