# DevelopmentNotification

## Installation

```
gem 'development_notification', "0.1.3" # and bundle
```

Copy and run migration
```
$ rake development_notification:install:migrations
$ rake db:migrate
```

## Configuration

```ruby
# in /config/initializers/development_notification.rb
DevelopmentNotification.configure do |config|
  config.leadersend_username = "email@example.com"
  config.leadersend_api_key = "0933e545acxc063cb8a101a374cc721f"
  config.domain = "example.com"
  config.validate! # must be called in the very end.
end
```

## Usage
After setup you gain access to:
* DevelopmentNotification::Email model that logs email prepared and sent.
* DevelopmentNotification::Email.send_email(parameter_hash) #=> sends emails

### Email sending :bear: (the good stuff) :honeybee:
```
DevelopmentNotification::Email.send_email(
  title: "Systemside identifier",
  to: ["dump@example1.com", "dump@example2.com"],
  from: "creative@inbox.lv",
  fromname: "Creative",
  subject: "test",
  template: "html body"
)
```

`to:` key accepts both array of strings and a single string  

## Gotchas
* Sometimes production does not load the gem. Append `require: false` in gemfile, and add the line `require 'development_notification'` to `/config/application.rb`

## Development
1. Set up Ruby >= 2 (try `rvm use 2.2.3@dev_noti --create`)  
2. Install bundler, bundle
3. Review dummy app database in `spec/dummy/config/database.yml`
4. `rake db:create db:migrate db:seed RAILS_ENV=test`
5. `rspec`
