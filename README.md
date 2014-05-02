# sidekiq-gelf

Enables Sidekiq logging to a GELF-supported server, such as Graylog2.

## Usage

``` ruby
# Adds the GELF logger as middleware in Sidekiq in order
# to include important logging information.
# These arguments are passed through to gelf-rb.
Sidekiq::Logging::GELF.hook!('127.0.0.1', 12201, 'LAN', facility: "my-application")
```

**Note:** by default, normal logging is left as-is. If you wish to log only to the GELF input, you can do:

``` ruby
Sidekiq.configure_server do |config|
  config.server_middleware do |chain|
    chain.remove Sidekiq::Middleware::Server::Logging
  end
end
```