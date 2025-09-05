#
1) Generate private key
```shell
openssl genrsa -out plantuml.key 2048
```

2) Generate self-signed certificate (valid for 365 days)
```shell
#  Set the CN to the github url or if external use that url
openssl req -new -x509 -key plantuml.key -out plantuml.crt -days 365
```

3) Place the two certs in ./ssl
4) Start the containers.
```shell
docker compose up -d
```
5) Add the PlantUML url to gitlab:  
```Admin -> General -> PlantUML```
https://gitlab.example.com:8443

`.puml` and `plantuml` .md code blocks should now render.
