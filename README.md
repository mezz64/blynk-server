# Docker image that runs the Blynk server v0.16.0 

## Run
### Build image

    docker build -t blynk .
    
### Run image

    docker run --restart=always  -p 7443:7443 -p 8443:8443 \
    -v /path/to/blynk-data:/data \
    --name blynk -d blynk

## SSL 

You can obtain free ssl certificates using [Let's Encrypt Certbot](https://certbot.eff.org/) or from [StartSSL](https://www.startssl.com/).

Put your `fullchain.crt` and `privkey.pem` to `blynk-data` folder.

Add these lines to `blynk-data/server.properties`
```
server.ssl.cert=/data/fullchain.crt
server.ssl.key=/data/privkey_pass.pem
server.ssl.key.pass=SeCuR3_Pa$$w0rD
```
Don't forget to encrypt your privkey and set password:

```
openssl pkcs8 -topk8 -inform PEM -outform PEM -in privkey.pem -out privkey_pass.pem
```