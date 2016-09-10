Caddy Server reverse proxy
==========================

At the first start it generates an SSL certificate via LetsEncrypt.
It also comes with QUIC experimental protocol support - see [example](https://github.com/dockhero/quic-protocol-demo)

```bash
heroku dh:generate caddy-proxy
```

By default it generates a proxy for your Heroku app, but this behavior can be
adjusted by setting environment variables in `dockhero-compose.yml`

| ENV VAR      	| DEFAULT           	| EXPLANATION                    	|
|--------------	|-------------------	|--------------------------------	|
| VIRTUAL_HOST 	| ${DOCKHERO_HOST}  	| Caddy server will generate an SSL certificate for that domain          	|
| TARGET_URL   	| ${HEROKU_APP_URL} 	| URL which receives the request 	|

It's recommended to always use a volume to store SSL certificate and key
to avoid generating the certificate every time the container starts and hitting the limits.

You can see the Caddy's access.log using Heroku logs command

```bash
heroku logs -p dockhero --tail
```
