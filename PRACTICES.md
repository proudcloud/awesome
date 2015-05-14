# Development practices

A list of things to prefer and avoid in projects.

## Rails

In general:

- Prefer [rspec](https://github.com/rspec/rspec) for testing with the `expect().to` syntax
- Prefer [figaro](https://rubygems.org/gems/figaro) for 12-factor style app configuration
- Prefer to commit your `config/*.yml` files, except database.yml (private repos only!)

CSS and JS:

- Prefer [sass-rails](https://github.com/rails/sass-rails) as a preprocessor
- Prefer [autoprefixer-rails](https://github.com/ai/autoprefixer-rails) for vendor prefixes
- Prefer [haml](http://haml.info/) for templating
- Prefer [bootstrap](http://getbootstrap.com) if a CSS framework is needed
- Prefer [bootstrap-sass](https://github.com/twbs/bootstrap-sass) for Bootstrap + Rails integration
- Prefer [bower-rails](https://rubygems.org/gems/bower-rails) for managing 3rd-party JS
- Prefer [teaspoon](https://github.com/modeset/teaspoon) for JS testing

Emails:

- Prefer [letter_opener](https://rubygems.org/gems/letter_opener) for locally testing emails
- Prefer [premailer-rails](https://rubygems.org/gems/premailer-rails) for managing inline email CSS

Avoid:

- Avoid [less-rails](https://github.com/metaskills/less-rails/). Slow to update, and doesn't support [import globbing](https://github.com/less/less.js/issues/1181)
- Avoid [cucumber](https://github.com/cucumber/cucumber). Integration tests get messy fast
- Avoid [compass](http://compass-style.org/) unless necessary. Use autoprefixer instead
- Avoid [bootstrap-on-rails](https://github.com/jasontorres/bootstrap-on-rails) because it's .less and not currently maintained
- Avoid [twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails) because it's .less and has too many abstractions
- Avoid [coffeescript](http://coffeescript.org/). Prefer to use [sprockets-es6](https://rubygems.org/gems/sprockets-es6) instead. ([article](https://robots.thoughtbot.com/replace-coffeescript-with-es6))

## Design

- Prefer [Sketch](http://bohemiancoding.com/sketch/) for UI design
- Prefer [ionicons](http://ionicons.com/) for UI icons (instead of FontAwesome)
- Prefer [Styledown](https://github.com/styledown/styledown) for making a Living Styleguide

## Git and GitHub

- Prefer [git-flow branching model](http://nvie.com/posts/a-successful-git-branching-model/)
- Use `feature/xyz` branches for features, `fix/xyz` for code fixes, `hotfix/xyz` for emergency hotfixes
- Use the tag `review` for "done" PR's awaiting code review
- Prefer `develop` branch for development
- Prefer `master` branch for deployments
- Prefer to tag releases if possible

Avoid:

- Avoid `production` branches, they're usually redundant

## Sass

- Prefer .scss (nested) syntax over .sass (indented), since most projects use that
- Enable [CSS antialiasing](http://ricostacruz.com/cheatsheets/css-antialias) globally
- Prefer to make new components rather to extend/override Bootstrap components
- Prefer to break CSS into multiple files and use `@import 'components/*'` ([info](https://github.com/rstacruz/rscss#one-component-per-file))
- Prefer to start a styleguide as early on in the project

## JavaScript

- Prefer [babel](http://babeljs.io/) as a preprocessor. For rails, use [sprockets-es6](https://rubygems.org/gems/sprockets-es6)

Avoid:

- Avoid [coffeescript](http://coffeescript.org/). See above
