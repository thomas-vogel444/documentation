# SSL

## Key stores and Trust stores

- Truststore
    - used to store certificates from trusted CAs used to verify certificates presented by a Server in a SSL connection
- Keystore
    - used the store private keys and own identity certificates to present to other parties.

If implementing SSL on the server side
- you need to store your server certificates in a Keystore.
- this certificate will be presented to the client every time there is connection initiated.
- if you require the client to authenticate itself, then you also need a Truststore.

In Java, you specify the Keystore and Truststore by psecifying the following properties
- `-javax.net.ssl.keyStore`
- `-javax.net.ssl.trustStore`
The truststore is stored inside the file `JAVA_HOME/JRE/Security/cacerts`

Use the `keytool` command to view the certificates. 