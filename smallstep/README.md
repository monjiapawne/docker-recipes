# Setup
## Client
Install
```shell
# wget the latest .deb
# https://github.com/smallstep/cli/releases
wget https://dl.smallstep.com/gh-release/cli/gh-release-header/v0.28.7/step-cli_0.28.7-1_amd64.deb
sudo dpkg -i step-cli_0.28.7-1_amd64.deb
```

## Server
1) Update .env with correct fqdn of the signing server
2) Create the volume's folder
```shell
mkdir step
```
3) Start the container
```shell
sudo docker compose up -d
````
4) Check the logs of the container to get the password
```shell
sudo docker compose logs step-ca
```
5) Transfer the `root.crt` and `intermediate_ca.crt` from the server `./step/certs/` to the client
### Client
6) Bootstrap the client
```shell
# get fingerprint
FINGERPRINT=$(step certificate fingerprint root_ca.crt)
# bootstrap
step ca bootstrap --ca-url https://<url_you_used_.env>:9000 --fingerprint $FINGERPRINT
```
### Try generate a certificate
```shell, this will only be a 1 day cert
step ca certificate "gitlab.col.corp" gitlab.crt gitlab.key
# build the chain
cat gitlab.crt intermediate_ca.crt > fullchain.crt
this should provide the two certs needed. transfer them and test.
```
Once that worked generate a year long certs
server
```
./step/config/ca.json
```
edit the max duration, after "key {..},"
```json
"claims": {                                     
        "maxTLSCertDuration": "8760h",          
        "defaultTLSCertDuration": "720h"        
}              
```
client
```
# generate a cert for 1 year
step ca certificate "gitlab.col.corp" gitlab.crt gitlab.key --not-after=8760h
cat gitlab.crt intermediate_ca.crt > fullchain.cert
```

