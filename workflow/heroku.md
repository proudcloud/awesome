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
config.serve_static_files = true
```
It is expected that credentials/keys are set in your `secrets.yml`(which is included in the repo), just make sure the these are appropriately set within `production: ` block as well
```
production:
  secret_key_base: 320f4772bb7e84f94f83b05a1e220d6b18c3053e4d601224efbda34434a79183e0f721a7b12c0ae89a91b9eaba092ceba8f145ddb4fd46dc9016fed6202e5a41
  ...
development:
  secret_key_base: 769579477b78657f832f260b62151d8955b3f3bcdd054cc287d17fe0c75a7524f0d8a07c733c55acbe72e1ce8821e1ef11739a14e525a8443129d26742a10f1f
  ...
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