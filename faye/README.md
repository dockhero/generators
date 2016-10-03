Faye: Simple pub/sub messaging for the web
===========================

```bash
heroku dh:generate faye
```

This stack depends on FAYE_PUSH_TOKEN environment variable, which should be some random token, e.g.:

```bash
# DO NOT USE THIS TOKEN, GENERATE YOUR OWN!
heroku config:set FAYE_PUSH_TOKEN=25087a8154b2b4b859362a2442bcf8a8bc0fc53b70fb3dfe57e67928d9aad8608cecabea58999bdd4fa5094b4c9032b7255d7ceb7aee6c29fbbdab43a33bf8f0

heroku dh:compose up -d
```

Using with Rails
-----------------

```slim
-# application.slim
  = javascript_include_tag "#{ENV["DOCKHERO_FLEXIBLE_SSL_URL"]}/client.js"
  javascript:
    document.addEventListener("DOMContentLoaded", function() {
      var client = new Faye.Client('#{ENV["DOCKHERO_FLEXIBLE_SSL_URL"]}', {timeout: 120});

      client.subscribe('/channel', function(message) {
        console.log('Received message: ' + JSON.stringify(message));
      });
    })
```

Then publish some message from your Rails console:

```ruby
message = {
  channel: "/channel",
  data: { text: "Hello" },
  ext: { pushToken: ENV['FAYE_PUSH_TOKEN'] }
}

Net::HTTP.post_form(URI(ENV["DOCKHERO_FLEXIBLE_SSL_URL"]), message: message.to_json)
```

Find more in [official docs](https://faye.jcoglan.com/browser.html)
