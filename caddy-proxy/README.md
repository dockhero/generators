Caddy Server proxy for your Heroku app
==============================

```bash
heroku dh:generate caddy-proxy
```

`dockhero-compose.yml` contains the following environment variables:

| ENV VAR      	| DEFAULT           	| EXPLANATION                    	|
|--------------	|-------------------	|--------------------------------	|
| VIRTUAL_HOST 	| ${DOCKHERO_HOST}  	| Caddy server will generate an SSL certificate |
|               |                     |  via LetsEncrypt for that domain          	|
| TARGET_URL   	| ${HEROKU_APP_URL} 	| URL which receives the request 	|

It's recommended to always use a volume to store SSL certificate and key
to avoid generating the certificate every time the container starts and hitting the limits.
