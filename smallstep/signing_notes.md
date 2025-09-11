# Signing Commands

## Key generation
Generate RSA private key
```bash
openssl genrsa -out gitlab.key 2048
```

Generate CSR with SAN
``` bash
openssl req -new -newkey rsa:2048 -nodes \
  -keyout gitlab.key -out gitlab.csr \
  -subj "/CN=gitlab.col.corp" \
  -addext "subjectAltName=DNS:gitlab.col.corp"
```

## Signing
If no CSR (auto generate key + cert)
```bash
step ca certificate "gitlab.col.corp" gitlab.crt gitlab.key --not-after=8760h
```
If using a CSR (gitlab.crt = signed cert output)
```bash
step ca sign req.csr gitlab.crt --not-after=8760h
```

Create fullchain (signed cert + intermediate)
```bash
cat gitlab.crt intermediate_ca.crt > fullchain.cert
```
