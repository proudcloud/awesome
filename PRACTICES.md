# Development practices

This is a list of things to prefer and avoid in projects. These practices are a result of trials-and-errors across many Proudcloud projects. We've learned what works and what doesn't, and these are the lessons that stuck.


## Starting a new project

- Create a Github repo and make the default branch to `develop`.
- Create and update the project's README.md
- Add proper installation instructions. Notes and caveats.
- Github Slack channel integration. The amount of notifications you want to receive depends on you. Usually, we like to get notified with new pull requests and comments only.
- Continuous integration. Currently, we're using [Circleci](https://circleci.com). Ask an organization admin or a collaborator to add it for you if you don't have access. Circleci uses Github authentication so you don't need an invite. Don't forget the Slack integration.

## For ongoing projects

- Keep README.md updated (always assume a new team member will join anytime)
- Ensure db:migrate runs properly
- Ensure db:seed runs properly (They get outdated fast!). Alternatively, provide a way to seed a newcomer's project.
- Ensure painless turnovers

## Work Principles

- Better to ask forgiveness than permission
- Respect your team and individiual schedules
- Always work on targeted release versions or milestones. We use `alpha`, `beta` for early stage projects. Moving forward, practice the use of [Semantic Versioning](http://semver.org)
- Code clarity. Readable code.
- Consistency with team practices but feel free to discuss improvements.
- Consistency but correct and raise what you feel is wrong.
- Do your best not to be a blocker to your teammates.
- Got a problem? Ask on Slack.

Code:
- Make use of special ANNOTATIONS like # TODO:, FIXME:, OPTIMIZE: so rake notes can pick it up.

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

Avoid:

- Avoid [cucumber](https://github.com/cucumber/cucumber). Integration tests get messy fast
- Avoid `shoulda` and the `should` syntax

## Design

- Prefer [Sketch](http://bohemiancoding.com/sketch/) for UI design
- Prefer [ionicons](http://ionicons.com/) for UI icons (instead of FontAwesome)
- Prefer [Styledown](https://github.com/styledown/styledown) for making a Living Styleguide

## Git

Using GitHub:

- Send pull requests for code review. Tag it with `review` when you're done
- Be overly communicative about your pull requests. Best practice is to add screenshots to your pull requests ([example](https://github.com/proudcloud/crowd-funding/pull/371)) for your reviewer's convenience.
- Long running PRs are welcome. Always get your branches checked against the main branch (usually `develop`)
- Get your PRs updated. Rebase on top of the latest `develop` branch.

Git:

- Always commit. Small commits are acceptable.
- Make your commits contextual. Avoid commits that does other things that the commit was intended to.
- Commit messages that makes sense. Usually in this pattern: `"{action} {purpose|reason} {target}"`, order may vary.

Avoid:
  ```
    1) "Adds price validation"
    2) "Refactors the decorator"
    3) "Fixes bug"
    4) "Hotfix for the form bug"
  ```

Ideal:
  ```
    1) "Adds price validation to Product"
    2) "Refactors product.total_price decorator"
    3) "Fixes permitted params bug on orders#create"
    4) "Hotfix for the product form's price input bug"
  ```

[Here's an example of a good PR and commit](https://github.com/proudcloud/crowd-funding/pull/371)

- Target as the most important as without it `"Fixes bug"`, `"Adds price validation"` or `"Refactors"` doesn't actually make sense if people review the project commit history.

Branching:

- Use `feature/xyz` branches for features, `fix/xyz` for code fixes, `hotfix/xyz` for emergency hotfixes (see [git-flow])
- Use the `develop` branch for development
- Use the `master` branch for deployable versions
- Make sure `develop` is always passing CI tests
- Make sure `master` is always at a deployable state

Avoid:

- Avoid `production` branches, they're usually the same as master

[git-flow]: http://nvie.com/posts/a-successful-git-branching-model/

## Sass

- Prefer .scss (nested) syntax over .sass (indented), since most projects use that
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
- Prefer [realm.io](http://realm.io) over CoreData. Realm.io
- Use CocoaPods whenever available. When you need a library/plugin, check [Cocoa Controls](https://www.cocoacontrols.com/) first before trying to do it yourself.
