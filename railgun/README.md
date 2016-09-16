With [Cloudflare's Railgun](https://www.cloudflare.com/railgun/) you can decrease your Heroku app’s load time across the world by 2-3 times.

Prerequisites
-------------
Railgun is only available on Business plan.

We assume your Heroku app is already
[configured](https://support.cloudflare.com/hc/en-us/articles/205893698-Configure-CloudFlare-and-Heroku-over-HTTPS)
to use CloudFlare DNS and CDN features. 

You'll need a *Railgun Activation Key*. Copy it from *My Subscriptions* page 
and assign to `RAILGUN_ACTIVATION_KEY` Heroku config variable

```
heroku config:set RAILGUN_ACTIVATION_KEY=xxxxxxxxx
```

![My Subscriptions page](https://monosnap.com/file/MqNeUzt8g3Qj7GjrTJFbVmfOWnJ3zp.png)


Running the stack
-----------------

```
heroku addons:create dockhero; heroku plugins:install dockhero

heroku dh:generate railgun    # this generates dockhero-compose.yml
heroku dh:compose up -d
```

Now you should be able to turn on Railgun for your entire Cloudflare domain.
Click “Test” button to make sure everything works.

![Alt text](https://monosnap.com/file/omhbv2iSJK7D7xLmoQEOZRmicZuPDd.png)

Troubleshooting
---------------

Try sending requests to your app via CloudFlare domain name. 
`Cf-Railgun` HTTP header should appear on all of the responses from your app.

If the steps above didn’t work for you, please create a Github issue and attach your Docker’s logs:

```
heroku logs -p dockhero --tail
```

