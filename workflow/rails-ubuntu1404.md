# Ubuntu 14.04 Trusty Tahr Setup for RoR Development 
---
####Installing Ruby
---
Install Ruby dependencies  
```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```
Install Ruby (choose one of the methods below)  

* Rbenv
```
cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
rbenv install 2.2.2
rbenv global 2.2.2
ruby -v
```
* RVM
```
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
curl -L https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.2.2
rvm use 2.2.2 --default
ruby -v
```
* Compile from Source
```
cd
wget http://ftp.ruby-lang.org/pub/ruby/2.2/ruby-2.2.2.tar.gz
tar -xzvf ruby-2.2.2.tar.gz
cd ruby-2.2.2/
./configure
make
sudo make install
ruby -v
```
Install bundler  
* To skip installation of documentation for each package (Optional)
```
echo "gem: --no-ri --no-rdoc" >> ~/.gemrc
```
* Install Bundler
```
gem install bundler
```
---
####Setting up Git
---
* Setup initial git configuration
```
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
```
* Generate SSH key
```
ssh-keygen -t rsa -C "YOUR@EMAIL.com"
```
* Or copy from existing; create directory
```
$ mkdir ~/.ssh
$ cp ~/Downloads/id_rsa ~/.ssh
$ cp ~/Downloads/id_rsa.pub ~/.ssh
```
* Add key to Github
```
cat ~/.ssh/id_rsa.pub
```
* Test git
```
ssh -T git@github.com
```
---
####Installing Rails
---
* Install NodeJS
```
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
```
* Install Rails
```
gem install rails -v 4.2.1
```
If you are using rbenv
```
rbenv rehash
```
* Check if rails has been installed
```
rails -v
```
---
####Setting Up MySQL
---
* Install MySQL
```
sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```
---
####Setting Up PostgreSQL
---
* Install PostgreSQL
```
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.3 libpq-dev
```
* Setup postgres user
```
sudo -u postgres createuser mark -s
sudo -u postgres psql
postgres=# \password mark
```
---
####Setting Up MongoDB
---
* Import MongoDB's public key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```
* Create list file for MongoDB
```
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
```
* Install MongoDB
```
sudo apt-get update
sudo apt-get install -y mongodb-org
```
* Start MongoDB
```
sudo service mongod start
```
