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
2) Start the container
```shell
sudo docker compose up -d
````
3) Check the logs of the container to get the password
```shell
sudo docker compose logs step-ca
```
4) Transfer the `root.crt` from the server `./step/certs/` to the client
### Client
5) Bootstrap the client
```shell
# get fingerprint
FINGERPRINT=$(step certificate fingerprint root_ca.crt)
# bootstrap
step ca bootstrap --ca-url https://<url_you_used_.env>:9000 --fingerprint $FINGERPRINT
```
### Try generate a certificate
```shell
step ca certificate "gitlab.col.corp" gitlab.crt gitlab.key
```
