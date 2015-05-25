# Basic OS X Machine Setup for RoR Development 
####Pre-requisites
1. Update to Yosemite(OSX 10.10) from App Store

2. Install xCode 6.x 
3. Install xCode Command Line Tools
```
$ xcode-select --install
```
4. Install Homebrew & update packages
```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew update
```
5. Verify Homebrew installation
```
$ brew doctor
```

####Setup Git, Homebrew, RVM, & Default Ruby & Gemset
Run GCC then confirm appropriate root privileges
```
$ sudo gcc --version
```
Setup initial git config
```
$ git config --global user.name "Your Real Name"
$ git config --global user.email me@example.com
$ git config -l --global
```
Add SSH key
```
$ ssh-keygen -t rsa -C "YOUR@EMAIL.com"
```
Or copy from existing; create directory
```
$ mkdir ~/.ssh
$ cp ~/Downloads/id_rsa ~/.ssh
$ cp ~/Downloads/id_rsa.pub ~/.ssh
```
Install RVM and follow additional procedure such as sourcing RVM to profile
```
$ \curl -L https://get.rvm.io | bash -s stable --ruby
```
Install latest or appropriate ruby version
```
$ rvm install ruby
$ rvm --default use ruby-2.2.0
```
For faster bundling
```
$ echo "gem: --no-ri --no-rdoc" >> ~/.gemrc
```
Double ruby version and gemset (default) is active then install
```
$ gem install rails
```

####Install PostgreSQL
```
$ brew install postgresql
```
> Caveats: If builds of PostgreSQL 9 are failing and you have version 8.x installed, you may need to remove the previous version first. See:
  https://github.com/Homebrew/homebrew/issues/2510

> To migrate existing data from a previous major version (pre-9.4) of PostgreSQL, see:
  http://www.postgresql.org/docs/9.4/static/upgrading.html

To have launchd start postgresql at login
```
$ ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
```
Then to load postgresql now
```
$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```
Or, if you don't want/need launchctl, you can just run
```
$ postgres -D /usr/local/var/postgres
```

#### Install MongoDB
$ brew install mongodb
To have launchd start mongodb at login:
```
$ ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
```
Then to load mongodb now
```
$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
```
Or, if you don't want/need launchctl, you can just run
```
$ mongod --config /usr/local/etc/mongod.conf
```