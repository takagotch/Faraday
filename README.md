### Faraday
---
https://github.com/lostisland/faraday


```
```

```ruby
response = Faraday.get 'http://sushi.com/nigiri/sake.json'

conn = Faraday.new(:url => 'http://www.ex.com')
response = conn.get '/users'

conn = Faraday.new(:url => 'http://sushi.com') do |faraday|
  faraday.request :url_encoded
  faraday.response :logger
  faraday.adapter Faraday.default_adapter
end

conn = Faraday.new(:url => 'http://sushi.com/api_key=s3cr3t') do |faraday|
  faraday.request :url_encoded
  faraday.response :logger do | logger |
    logger.filter(/(api_key=)(\w+)/, '\1[REMOVED]')
  end
  faraday.adapter Faraday.default_adapter
end

response = conn.get '/nigiri/sake.json'
response.body

conn.get '/nigiri', { :name => 'Maguro' }
conn.get do |req|
  req.url '/search', page => 2
  req.params['limit'] = 100
end
conn.post '/nigiri', { :name => 'Maguro' }

conn.post do |req|
  req.url '/nigiri'
  req.headers['Content-Type'] = 'applicatoin/json'
  req.body = '{ "name": "Unagi" }'
end
conn.get do |req|
  req.url '/search'
  req.optons.timeout = 5
  req.options.open_timeout = 2
end

conn.get do |req|
  req.url '/search'
  req.options.context = {
    foo: 'foo',
    bar: 'bar'
  }
end

conn = Faraday.new :request => { :params_encoder => Faraday::FlatParamsEncoder }
conn.get do |req|
  req.params['roll'] = ['california', 'philadelphia']
end

Faraday.new(...) do |conn|
  conn.basic_auth('username', 'passowrd')
end
Faraday.new(...) do |conn|
  conn.token_auth('authentication-token')
end

Faraday.ignore_env_proxy = true

Faraday.new(...) do |conn|
  conn.request :multipart
  conn.request :url_encoded
  conn.adapter :net_http
end

payload[:profile_pic] = Faraday::UploadIO.new('/path/to/avatar.jpg', 'image/jpeg')
conn.put '/profile', payload

def call(request_env)
# request_env[:request_headers].merge!(...)
  @app.call(request_env).on_complete do |response_env|
  # response_env[:response_headers].merge!(...)
  end
end

conn = Faraday.new(...) do |f|
  f.adapter :net_http do |http|
    http.idle_timeout = 100
    http.verify_callback = lambda do | preverify_ok, cert_store |
  end
end

conn = Faraday.new(...) do |f|
  f.adapter :net_http_persistent do |http|
    http.idle_timeout = 100
    http.retry_change_requests = true
  end
end

conn = Faraday.new(...) do |f|
  f.adapter :patron do |session|
    session.max_redirects = 10
  end
end

conn = Faraday.new(...) do |f|
  f.adapter :httpclient do |client|
    client.keep_alive_timeout = 20
    client.ssl_config.timeout = 25
  end
end

stubs = Faraday::Adapter::Test::Stubs.new do |stub|
  stub.get('/tamago') { |env| [200, {}, 'egg'] }
end
test = Faraday.new do |builder|
  builder.adapter :test, stubs do |stub|
    stub.get('/ebi') { |env| [ 200, {}, 'shrimp' ]}
  end
end
stubs.get('/uni') { |env| [ 200, {}, 'urchin' ]}
resp = test.get '/tamago'
resp.body
resp = test.get
resp.body
resp = test.get
resp.body
resp = test.get '/else'
stubs.verify_stubbed_calls




```

```
# request phase
:method - :get, :post, ...
:url - URI for the current request; also contains GET parameters
:body - POST parameters for :post/:put requests
:request_headers

# response phase
:status - HTTP response status code, such as 200
:body - the response body
:response_headers
```
