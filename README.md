# HerokuDeploy

A (for now) very opinionated gem which has 3 sections:

* pipeline/app setup
* db restore (pull down your heroku database and `psql < tmp/latest.db`)
* deploys (push to heroku remotes)

These tasks all assume your heroku application names are of the format `"#{Rails.application.class.parent_name.underscore.gsub('_','-')}-#{environment}"`, where environment is one of staging, production. Setting up an app includes the following free Heroku addons:

*heroku-postgresql:hobby-dev
*newrelic:wayne
*papertrail:choklad
*rediscloud:30 
*scheduler:standard
*sendgrid:starter

App name configuration flags and more detailed documentation will come in a later version.


## Installation

Add this line to your application's Gemfile:

```ruby
gem 'heroku_deploy', group: :development # No need to include this on production or staging
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install heroku_deploy

## Usage
To see an updated list of tasks and descriptions:
`bundle exec rake heroku_deploy -T heroku_deploy`

~~~bash
rake db:restore                  # Pull Down a copy of the database from the specified heroku environment
rake db:restore:from_local_dump  # Restore from local dump file (defaults to '/tmp/latest.dump' - specify with DUMP_FILE Environmental Variable)
rake db:restore:local            # Erase local development and test database and restore from the local dump file
rake db:restore:production       # Restore a local copy of Heroku's Production Environment database
rake db:restore:staging          # Restore a local copy of Heroku's Staging Environment database
rake deploy                      # Deploy Safely to Heroku
rake deploy:production           # Deploy to Heroku's Production Environment
rake deploy:production:quick     # Quick Deploy to Production, without running migrations
rake deploy:staging:quick        # Quick Deploy to Staging, without running migrations
~~~


## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/ldstudios/heroku_deploy.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

