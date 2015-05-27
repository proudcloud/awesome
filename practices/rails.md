# Rails

In general:

- Prefer to commit your `config/*.yml` files, except database.yml (_PRIVATE_ _REPOS_ _ONLY!_)
- Make use of special Rails ANNOTATIONS like `TODO`, `FIXME`, and `OPTIMIZE` so rake notes can pick it up.
- Keep README.md updated (always assume a new team member will join anytime)

CSS and JS:

- Prefer [sass-rails](https://github.com/rails/sass-rails) as a preprocessor
- Prefer [autoprefixer-rails](https://github.com/ai/autoprefixer-rails) for vendor prefixes
- Prefer [haml](http://haml.info/) for templating
- Prefer [bootstrap](http://getbootstrap.com) if a CSS framework is needed
- Prefer [bootstrap-sass](https://github.com/twbs/bootstrap-sass) for Bootstrap + Rails integration
- Prefer [rails-assets.org](https://rails-assets.org) for managing 3rd-party JS/CSS
- Prefer [teaspoon](https://github.com/modeset/teaspoon) for JS testing

Emails:

- Prefer [letter_opener](https://rubygems.org/gems/letter_opener) for locally testing emails
- Prefer [premailer-rails](https://rubygems.org/gems/premailer-rails) for managing inline email CSS

Rake tasks:

- Ensure `db:migrate` runs properly
- Ensure `db:rollback` runs properly
- Ensure `db:seed` runs properly (They get outdated fast!). Alternatively, provide a way to seed a newcomer's project.
- Ensure painless turnovers

Configuration:

- Use `config/secrets.yml` to store config
- Use 12-factor style when overrides are needed: `pusher_id: <%= ENV['PUSHER_ID'] || '...' %>`
- Access them in your app via `Rails.application.secrets.pusher_id`

Avoid:

- Avoid [less-rails](https://github.com/metaskills/less-rails/). Slow to update, and doesn't support [import globbing](https://github.com/less/less.js/issues/1181)
- Avoid [compass](http://compass-style.org/) unless necessary. Use autoprefixer instead
- Avoid [bootstrap-on-rails](https://github.com/jasontorres/bootstrap-on-rails) because it's .less and not currently maintained
- Avoid [twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails) because it's .less and has too many abstractions
- Avoid [coffeescript](http://coffeescript.org/). Prefer to use [sprockets-es6](https://rubygems.org/gems/sprockets-es6) instead. ([article](https://robots.thoughtbot.com/replace-coffeescript-with-es6))
- Avoid [bower-rails](https://rubygems.org/gems/bower-rails). Heroku setup can be a pain, and rails-assets is a better choice nowadays.
- Avoid configuration gems like [figaro](http://rubygems.org/gems/figaro), [dotenv](http://rubygems.org/gems/dotenv), etc. Rails 4.1 should render them useless now.

## Sass

- Prefer `.scss` (nested) syntax over .sass (indented), since most projects use that
- Enable [CSS antialiasing](http://ricostacruz.com/cheatsheets/css-antialias) globally
- Prefer to make new components rather to extend/override Bootstrap components
- Prefer to break CSS into multiple files and use `@import 'components/*'` ([info](https://github.com/rstacruz/rscss#one-component-per-file))
- Prefer to start a styleguide as early on in the project

## Also see

- **[JavaScript practices](javascript.md)**
- **[Testing practices](testing.md)**
- **[Git practices](git.md)**
