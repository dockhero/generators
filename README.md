Dockhero example stack generators
==================================

*TL;DR: templates for `heroku dh:generate <name>`*

Prerequisites
--------------

You'll need Dockhero add-on and CLI plugin installed

```bash
heroku addons:create dockhero
heroku plugins:install dockhero
heroku dh:wait
```

Usage
------

```bash
heroku dh:generate <name>
```

This will create `dockhero-compose.yml` with a template stack
Review it with your editor - it may contain placeholders

Running the stack
------------------
```bash
heroku dh:compose up -d            # deploys to Dockhero
heroku dh:open                     # opens the stack in the browser
heroku logs --tail -p dockhero     # watch logs
```

See more commands in [CLI plugin docs](https://github.com/cloudcastle/dockhero-cli)

Available templates
------------------------

| Generator   	| Description                                                   	|
|-------------	|---------------------------------------------------------------	|
| helloworld  	| Sample static website                                         	|
| caddy-proxy 	| Reverse proxy with HTTP/2 and QUIC support and automatic SSL via LetsEncrypt	|
|             	|                                                               	|
