Caddy Server reverse proxy
==========================

Caddy Server is a simple yet powerful multi-purpose web server, which includes reverse proxy capability. It supports HTTP/2 and SSL (at the first start it generates an SSL certificate via LetsEncrypt).
It also comes with QUIC experimental protocol support - see [tutorial](https://docs.dockhero.io/tutorials/caddy.html)

```bash
heroku dh:generate caddy-proxy
```

By default it generates a proxy for your Heroku app, but this behavior can be
adjusted by setting environment variables in `dockhero-compose.yml`

| ENV VAR      	| DEFAULT           	| EXPLANATION                    	|
|--------------	|-------------------	|--------------------------------	|
| VIRTUAL_HOSTS 	| https://${DOCKHERO_HOST}  	| Caddy server will generate an SSL certificate for that domain          	|
| TARGET_URL   	| ${HEROKU_APP_URL} 	| URL which receives the request 	|

It's recommended to always declare a volume to store SSL certificate and key
to avoid generating the certificate every time the container starts and hitting the limits.

You can see the Caddy's access.log using Heroku logs command

```bash
heroku logs -p dockhero --tail
```
