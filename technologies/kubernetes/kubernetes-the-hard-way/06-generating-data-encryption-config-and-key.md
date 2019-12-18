# Generating the Data Encryption Config and Key

Kubernetes can encrypt various types of data at rest: e.g. cluster state, secrets, application configuration.

You need to generate an encryption key and encryption config for K8s secrets.

## The encryption key
Generate an encryption key:

```bash
ENCRYPTION_KEY=$(head -c 32 /dev/urandom | base64)
```

## The encryption config file

Create the encryption-config.yaml encryption config file
```bash
cat > encryption-config.yaml <<EOF
kind: EncryptionConfig
apiVersion: v1
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: ${ENCRYPTION_KEY}
      - identity: {}
EOF
```

Copy the encryption-config.yaml encryption config file to each controller instance
```bash
for instance in controller-0 controller-1 controller-2; do
  gcloud compute scp encryption-config.yaml ${instance}:~/
done
```