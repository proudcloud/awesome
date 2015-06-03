# Git

Using GitHub:

- Send pull requests for code review. Tag it with `review` when you're done
- Be overly communicative about your pull requests. Best practice is to add screenshots to your pull requests ([example](https://github.com/proudcloud/crowd-funding/pull/371)) for your reviewer's convenience.
- Long running PRs are welcome. Always get your branches checked against the main branch (usually `develop`)
- Get your PRs updated. Rebase on top of the latest `develop` branch.
- If your PR references a Github Issue, make sure to mention it in your PR's description using [this format ](https://help.github.com/articles/closing-issues-via-commit-messages/).

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
- Always delete `merged`, `stale`, `outdated` branches. *Ang past ay para sa mga bitter lamang. Wag clingy.* <sup>[1](https://github.com/proudcloud/awesome/issues/23#issuecomment-108285010)</sup>

Branching:

- Use `feature/xyz` branches for features, `fix/xyz` for code fixes, `hotfix/xyz` for emergency hotfixes (see [git-flow])
- Use the `develop` branch for development
- Use the `master` branch for deployable versions
- Make sure `develop` is always passing CI tests
- Make sure `master` is always at a deployable state

Avoid:

- Avoid `production` branches, they're usually the same as master

[git-flow]: http://nvie.com/posts/a-successful-git-branching-model/
