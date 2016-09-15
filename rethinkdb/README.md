RethinkDB
==========

RethinkDB microservice with basic auth for Admin UI and default password on DB connection

Preparing the environment
-------------------------

```
heroku dh:generate rethinkdb    # generates dockhero-compose.yml
heroku config:set RETHINKDB_PASSWORD=<db connection password>
heroku config:set RETHINKDB_ADMIN_PASSWORD=<admin UI password>
```


Running the stack
-----------------

```
heroku dh:compose up -d
```

Now you should be able to open admin UI in the browser and login with
the following credentials: `admin:<admin UI password>`

```
heroku dh:open    
```


Connecting from Heroku
----------------------

The address of RethinkDB host is exposed to `DOCKHERO_HOST` environment variable.
Here is a Ruby example using NoBrainer ORM:

```
NoBrainer.configure do |config|
  config.rethinkdb_urls = ["rethinkdb://admin:#{ENV.fetch('RETHINKDB_PASSWORD')}@#{ENV.fetch('DOCKHERO_HOST')}:28015/<dbname>"]
end
```
