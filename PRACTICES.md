# Development practices

A list of things to prefer and avoid in projects.

## Rails

- Prefer [sass-rails](https://github.com/rails/sass-rails) as a preprocessor
- Prefer [autoprefixer-rails](https://github.com/ai/autoprefixer-rails) for vendor prefixes
- Prefer [haml](http://haml.info/) for templating
- Prefer [bootstrap](http://getbootstrap.com) if a CSS framework is needed
- Prefer [bootstrap-sass](https://github.com/twbs/bootstrap-sass) for Bootstrap + Rails integration
- Prefer [rspec](https://github.com/rspec/rspec) for testing
- Prefer [teaspoon](https://github.com/modeset/teaspoon) for JS testing
- Prefer [figaro](https://rubygems.org/gems/figaro) for 12-factor style app configuration

Avoid:

- Avoid [less-rails](https://github.com/metaskills/less-rails/). Slow to update, and doesn't support import globbing
- Avoid [cucumber](https://github.com/cucumber/cucumber). Integration tests get messy fast
- Avoid [compass](http://compass-style.org/) unless necessary. Use autoprefixer instead

## Design

- Prefer [Sketch](http://bohemiancoding.com/sketch/) for UI design
- Prefer [ionicons](http://ionicons.com/) for UI icons (instead of FontAwesome)

## Git

- Prefer [git-flow branching model](http://nvie.com/posts/a-successful-git-branching-model/) - use `feature/` branches
- Prefer `develop` branch for development
- Prefer `master` branch for deployments
- Prefer to tag releases if possible

Avoid:

- Avoid `production` branches, they're usually redundant
