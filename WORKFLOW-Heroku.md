# Heroku Deployment for Rails
####Pre-requisites:
- Existing Rails App
- Git & associated SSH Keys
```
# If app isn't associated with git yet
$ git init
$ git add .
$ git commit -m 'Sets initial commit'
```
```
# If no SSH Keys generated yet, run command below;
# Fill-in succeeding prompts as desired but leave out passphrase prompt as empty
$ ssh-keygen -t rsa
```
- Heroku Account. Sign up [here].
- Heroku Toolbelt
```
# OSX (via Homebrew)
$  brew install heroku-toolbelt
# Debian/Ubuntu
$ wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
# Login
$ heroku login
```


####Setup:
Specify ruby version in your `Gemfile`. This is clearly ok unless you indicate a different version from that of your `.ruby-version` et al
```
source "https://rubygems.org"
ruby "2.1.2"
# ...
```
Set static asset serving at `config/application.rb`
```
config.serve_static_assets = true
```
Environment-specific configurations, like that from application.yml or anything that is accessed with `ENV[__]` are set via `heroku config:set`
```
$ heroku config:set PUSHER_APP_ID=324213412342 PUSHER_APP_SECRET=lkjh34k234234j2l3h
```
Set DB-related configurations differ depending on the DB you are using. If you're on `PostgreSQL`, a simple `heroku run rake db:migrate` will do.

If you're using `mongoid`, I prefer [MongoLab] as a starting point

Create Heroku app/instance
```
$ heroku apps:create my-very-own-project-such-wow
```
Push to Heroku
```
$ git push heroku master
```

Open your app deployed from Heroku
```
$ heroku open
```
**<DONE>**


####After all this...
...why not add `rail_12factor` gem to Gemfile? *If you're not concerned with Rails logs being written to file, `config.serve_static_assets = true` is all you need.*

...I use `secrets.yml` instead of `application.yml`? *It's a known limitation for using Heroku. Best stick in using `ENV[___]` approach on this one.*

...why not set `RAILS_ENV=staging` instead of `production` at my Heroku instance? *1) Dev/Prod Parity; get your prod environment as close as that with your local one by minimizing enviroment-related differences on variables for example, also, 2) it is unlikely that you want a real production app deployed at Heroku.*

...why not use `Figaro` for environment variables? *Just use `heroku config:set`*

...why not use `Foreman`? *Use it, then!*

[here]:https://www.heroku.com/
[MongoLab]:https://devcenter.heroku.com/articles/mongolab