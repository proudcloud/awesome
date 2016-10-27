# Setup for Elixir projects

It's mostly the same as setting up environments for Ruby or JavaScript, with some nuances:

- [Postgres](#postgres): to make your life easier, create a user with name `postgres` password `postgres`. This is the default for most Phoenix projects.
- [Asdf](#asdf): this is the preferred version manager for Elixir, Erlang and Node.js.

All of these steps are optional, but recommended.

<br>

## Postgres

> Phoenix projects default to connecting to Postgres with the username `postgres` and password `postgres`. This isn't so easy to override, so let's just keep that as the default.

* __Install postgres.__ In OSX, use [Homebrew](http://brew.sh/) to install it.

  ```sh
  # OSX only
  brew install postgres
  ```

* Use [homebrew/services](http://github.com/homebrew/homebrew-services) to start Postgres. Optional but recommended.

  ```sh
  # OSX only
  brew tap homebrew/services
  brew services start postgres
  ```

* __Create a `postgres` user.__ Use PostgreSQL's `createuser` to create a new user. Give it a password `postgres`.

  ```sh
  $ createuser --superuser postgres -P
    Enter password for new role:
    Enter it again:
  ```

<br>

## asdf

> [Asdf](https://github.com/asdf-vm/asdf) is a version manager for everything: Ruby, Elixir, Erlang, Node.js, and so on.

* __Install asdf__ via git.

  ```sh
  git clone https://github.com/asdf-vm/asdf.git ~/.asdf
  ```

* __Add it to bashrc.__ (If you're on zsh, add it to `~/.zshrc`. For fish shell and others, see [asdf setup docs](https://github.com/asdf-vm/asdf#setup)).

  ```sh
  # bash / Ubuntu
  echo '. $HOME/.asdf/asdf.sh' >> ~/.bashrc
  echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc
  ```

  ```sh
  # bash / OSX
  echo '. $HOME/.asdf/asdf.sh' >> ~/.bash_profile
  echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bash_profile
  ```

  ```sh
  # Zsh
  echo '. $HOME/.asdf/asdf.sh' >> ~/.zshrc
  echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.zshrc
  ```

* __Add plugins__ for Erlang, Elixir and Node.js.

  ```sh
  asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git
  asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git
  asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs.git
  ```

<br>

## Install Erlang/Elixir/Node.js

* If you have a project with a `.tool-versions`, simply run `asdf install`.

  ```sh
  cd my-project
  asdf install
  ```

* To configure "global" versions in asdf, create `~/.tool-versions`. Here's a fair starting point.

  ```sh
  # These are stable versions as of July 2016
  cd ~
  echo 'erlang 19.0'   > .tool-versions
  echo 'nodejs 6.2.2' >> .tool-versions
  echo 'elixir 1.3.1' >> .tool-versions
  asdf install
  ```

<br>

## Alternatives

* [Postgres.app](http://postgresapp.com/) is another way to install Postgres.
* [Kiex](https://github.com/taylor/kiex) is an Elixir version manager. It doesn't manage Erlang installations (a dependency of Elixir), however.
* You may also install Erlang and Elixir via Homebrew, though it may be difficult to switch versions later on.
