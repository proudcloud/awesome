# Development practices

This is a list of things to prefer and avoid in projects. These practices are a result of trials-and-errors across many Proudcloud projects. We've learned what works and what doesn't, and these are the lessons that stuck.

## Ethics

- Always be online on Slack
- Better to ask forgiveness than permission
- Respect your team and individual schedules
- Always work on targeted release versions or milestones. We use `alpha`, `beta` for early stage projects. Moving forward, practice the use of [Semantic Versioning](http://semver.org).
- Be aware of the product roadmap.
- Work will never run out. Focus on approximately 2 weeks (1 sprint) worth of targets only. Close a version release. Repeat the cycle.
- Conserve energy. Do not overwork yourselves.
- Code clarity. Readable code.
- Consistency with team practices but feel free to discuss improvements.
- Consistency but correct and raise what you feel is wrong.
- Do your best not to be a blocker to your teammates.
- Got a problem? Ask on Slack.

## Starting a new project

- Create a Github repo and make the default branch to `develop`.
- Create and update the project's `README.md`
- Add proper installation instructions. Notes and caveats.
- Github Slack channel integration. The amount of notifications you want to receive depends on you. Usually, we like to get notified with new pull requests and comments only.
- Continuous integration. Currently, we're using [Circleci](https://circleci.com). Ask an organization admin or a collaborator to add it for you if you don't have access. Circleci uses Github authentication so you don't need an invite. Don't forget the Slack integration.

## For ongoing projects

- Keep README.md updated (always assume a new team member will join anytime)
- Ensure `db:migrate` runs properly
- Ensure `db:rollback` runs properly
- Ensure `db:seed` runs properly (They get outdated fast!). Alternatively, provide a way to seed a newcomer's project.
- Ensure painless turnovers

## Rails

In general:

- Prefer [rspec](https://github.com/rspec/rspec) for testing with the `expect().to` syntax
- Prefer to commit your `config/*.yml` files, except database.yml (_PRIVATE_ _REPOS_ _ONLY!_)
- Make use of special Rails ANNOTATIONS like `TODO`, `FIXME`, and `OPTIMIZE` so rake notes can pick it up.

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

Avoid:

- Avoid [less-rails](https://github.com/metaskills/less-rails/). Slow to update, and doesn't support [import globbing](https://github.com/less/less.js/issues/1181)
- Avoid [compass](http://compass-style.org/) unless necessary. Use autoprefixer instead
- Avoid [bootstrap-on-rails](https://github.com/jasontorres/bootstrap-on-rails) because it's .less and not currently maintained
- Avoid [twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails) because it's .less and has too many abstractions
- Avoid [coffeescript](http://coffeescript.org/). Prefer to use [sprockets-es6](https://rubygems.org/gems/sprockets-es6) instead. ([article](https://robots.thoughtbot.com/replace-coffeescript-with-es6))
- Avoid [bower-rails](https://rubygems.org/gems/bower-rails). Heroku setup can be a pain, and rails-assets is a better choice nowadays.

## Testing:

- Prefer [rspec & rspec-rails](http://rspec.info/) as the testing framework
- Prefer [capybara with rspec](https://github.com/jnicklas/capybara#using-capybara-with-rspec) for acceptance tests
- Prefer [factory-girl-rails](https://github.com/thoughtbot/factory_girl) for test data requirements
- Ensure sensible and updated factories
- Ensure passing tests
- Prefer the `expect` syntax

Avoid:

- Avoid [cucumber](https://github.com/cucumber/cucumber). Integration tests get messy fast
- Avoid `shoulda` and the `should` syntax

## Sass

- Prefer `.scss` (nested) syntax over .sass (indented), since most projects use that
- Enable [CSS antialiasing](http://ricostacruz.com/cheatsheets/css-antialias) globally
- Prefer to make new components rather to extend/override Bootstrap components
- Prefer to break CSS into multiple files and use `@import 'components/*'` ([info](https://github.com/rstacruz/rscss#one-component-per-file))
- Prefer to start a styleguide as early on in the project

## JavaScript

- Follow [airbnb/javascript](https://github.com/airbnb/javascript) the styleguide (feel free to discard ES6-isms for non-ES6 projects)
- Prefer [babel](http://babeljs.io/) as a preprocessor. For rails, use [sprockets-es6](https://rubygems.org/gems/sprockets-es6)

Avoid:

- Avoid [coffeescript](http://coffeescript.org/). See above

## iOS

- Follow the [Ray Wenderlich Styleguide](https://github.com/raywenderlich/swift-style-guide) except using 2 spaces as indentation. We'll use 4 spaces as recommended by Apple.
- Prefer [realm.io](http://realm.io) over CoreData.
- Use CocoaPods whenever available. When you need a library/plugin, check [Cocoa Controls](https://www.cocoacontrols.com/) first before trying to do it yourself.

## Design

See **[Design practices](PRACTICES-Design.md).**

## Git

See **[Git practices](PRACTICES-Git.md).**
