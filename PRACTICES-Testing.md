# General Philosophy

- Test the **app**, not the **framework** or **library**.

- **TDD** is not required, tested code is.

- Code coverage doesn't mean anything. You can never know all the edge cases.

- Code should be easy to test. If it's hard to test, change your code.

- Fast tests are happy tests.


# RSpec

-  The `should` syntax is [dead](https://github.com/rspec/rspec-expectations/blob/master/Should.md#why-switch-over-from-should-to-expect). Use the `expect` syntax. This also means no `shoulda`.

- You can run specific examples by providing their line number when you run your tests.

  ```
  > rspec spec/models/user_spec.rb:11
  ```

- Prefer to run specs with the `--color` or `-c` and the `--format=doc` or `-f d` options. Or store it in an `.rspec` file.

  ```
  # .rspec
  --color
  --format=doc
  ```

- Running specs with the `--profile` or `-p` option will display the top ten slowest examples. It also accepts a number argument.

  ```
  # Displays the 5 slowest examples
  > rspec spec/models/user_spec.rb -p 5
  ```

- Use [shared_examples](https://www.relishapp.com/rspec/rspec-core/docs/example-groups/shared-examples) when possible.

## `describe`

- Consider examples as the project's documentation.

- Describe your methods properly and accurately. If you change what the code does, do **NOT** forget to update the test's description.

- Use double quotes for the description string.

- Your top level `describe` block should indicate the class under test.

  ```ruby
  # This is actually a smoke test
  describe Wat do
    ...
  end
  ```

- No instance varaibles. Use `let` or `let!`. If in doubt, use `let!`.

- `before`, `around`, `after` and `let` blocks should come right after a `describe` block and before the next `describe` or `context` block.

- Prefix your methods with `#` if it's an instance method and `.` if it's a class method or model scope.

  ```ruby
  describe "#instance_method"
  describe ".class_method"
  ```

## `context`

- Use `context` for branching code. Prefer using `with` and `without` or `when`.

  ```ruby
  describe "#some_method" do
    context "with a truthy condition" do
      it "returns true" do
        condition = true
        expect(some_method condition).to eq true
      end
    end

    context "without a truthy condition" do
      it "returns false" do
        condition = false
        expect(some_method condition).to eq false
      end
    end

    # OR

    context "when the condition is truthy" do
      it "returns true" do
        condition = true
        expect(some_method condition).to eq true
      end
    end

    context "when the condition is not truthy" do
      it "returns false" do
        condition = false
        expect(some_method condition).to eq false
      end
    end
  end
  ```

## `it`

- Prefer one expectation per `it` block.

- Be explicit with your descriptions. Say what the code *does*, not what it *should* do.

  ```ruby
  it "returns true"
  it "sends the email"

  # AVOID
  it "should be true"
  it "should send the email"
  ```

- Prefer `eq` over `be` and magic matchers.

  ```ruby
  # PREFER THIS
  expect(user.admin?).to eq true
  expect(user.age).to eq 12

  # OVER THIS
  expect(user).to be_admin
  expect(user.age).to be 12
  ```

- Prefer multiline blocks over one liners.

- If you must use one liners, use `is_expected`. Again, no `shoulda`.


## `pending`

- Always mark an untested method with `pending`.

  ```ruby
  describe "#untested_method" do
    pending "because reasons"
  end
  ```

## Metaprogramming Tests

- Don't.


# Rails

- Follow the `rspec-rails` [directory structure](https://relishapp.com/rspec/rspec-rails/docs/directory-structure) and naming conventions.

- `cucumber` can be cucumbersome. Use RSpec `features` specs with [capybara](https://github.com/jnicklas/capybara) instead.

- Delegate routing and view specs to `features` specs.

- Only write controller specs for actions that cannot be covered by `features` specs. Otherwise, write `features` specs.

- Use [`requests` or `api` specs](https://github.com/rspec/rspec-rails#request-specs) for testing API requests.

- Do not forget to test helpers and rake tasks.

- Prefer `spec_helper` over `rails_helper`. Only require `rails_helper` for tests that need Rails to work.

- Always include the [database_cleaner](https://github.com/DatabaseCleaner/database_cleaner) gem or it's faster cousin, [database_rewinder](https://github.com/amatsuda/database_rewinder).

- Use [factory_girl_rails](https://github.com/thoughtbot/factory_girl_rails) over fixtures.

- Use [ffaker](https://github.com/EmmanuelOga/ffaker) for data generation.

- In your `rails_helper`, always set `config.use_transactional_fixtures` to `false`

- External HTTP requests are slow. Always mock them or use gems like [vcr](https://github.com/vcr/vcr) and [WebMock](https://github.com/bblimke/webmock).

- When mocking/stubbing, never mock/stub the unit you are testing.
  ```ruby
  # AVOID
  allow(User).to receive(:count).and_return(2)
  expect(User.count).to eq 2
  ```


## Model specs

- No mocking. Test the actual models.

- Skip association tests.

- Test validations. Presence validation specs are optional.
  ```ruby
  # Validations
  expect(valid_project.errors.full_messages).to eq []
  expect(invalid_project.errors.full_messages).to include "Video url is not a valid Youtube/Vimeo url"
  ```

- Test scopes for both inclusion and exclusion.
  ```ruby
  # Scopes
  expect(Project.published).to include published_project
  expect(Project.published).to_not include unpublished_project
  ```

- Callbacks testing can be done in a couple of ways.
  ```ruby
  # Assumes an `#ensure_default_role` callback that sets the default role if not provided

  # You can use a proc
  user.role = nil
  expect { user.save }.to change(user, :role).to("default")

  # or test the effect
  user.role = "admin"
  user.save
  expect(user.role).to eq "admin"

  # or test for the just the call
  expect_any_instance_of(User).to receive(:ensure_default_role)
  user.save

  # then test the functionality
  user.nil
  user.send :ensure_default_role
  expect(user.role).to eq "default"
  ```

- `private` method testing can be optional, but only if there is a public method spec that covers it.


## View specs

- See [Features](PRACTICES-Testing.md#features).


## Controller specs

- See [Features](PRACTICES-Testing.md#features).


## Lib specs

- Unless you autoloaded the file you're testing, you will need to `require` it.

- Do not require `rails_helper` if you can avoid it. Mock what you can.


## Helper specs

- RSpec provides a `helper` object so you don't have to include the module in a dummy class to test it.
  ```ruby
  expect(helper.image_url_for user).to eq "http://wat.com/img/fifi"
  ```


## Mailer specs

- Always mock the models.

- Do not test `#deliver`.

- Test for addresses, subject and attachments.
  ```ruby
  expect(mailer.to).to eq recipient.email
  expect(mailer.from).to eq sender.email
  expect(mailer.reply_to).to eq sender.reply_to_email
  expect(mailer.attachments.size).to eq 1
  ```


## Request specs

- Request specs are considered as integration tests. Treat them as such.

- Only use these specs for testing APIs. Use [Features](PRACTICES-Testing.md#features) for pages.

- Test the body and status in the same example.
  ```ruby
  it "returns the correct user" do
    get user_path(user)
    expect(response.body["id"]).to eq user.id
    expect(response.status).to eq 200
  end
  ```

- Use helpers to reduce duplication. For example, assuming you're working on a JSON API, this helper will clean up the parsing logic for you.
  ```ruby
  # support/api_helpers.rb
  module ApiHelpers
    def json
      JSON.parse(response.body)
    end
  end

  # rails_helper.rb
  config.include ApiHelpers, type: :request

  # usage
  expect(json["id"]).to eq user.id
  ```


## Feature Specs

- Use `feature` and `scenario` blocks.
  ```ruby
  feature "User Authentication" do
    scenario "with valid credentials" do
      ...
    end
  end
  ```
- Test for element visibility.
  ```ruby
  expect(page).to have_content "Log Out"

  # AVOID
  expect(user.signed_in?).to eq true # test this somewhere else
  ```
- Multiple expectations per `scenario` is allowed.

- Helper methods inside `feature` blocks or within the spec file is allowed.

- Always use the Capybara version for negations.
  ```ruby
  expect(page).to have_no_content user.name

  # AVOID
  expect(page).to_not have_content user.name
  ```

- Limit the usage of the `js: true` tag only to blocks that have javascript interaction.

- Alternatively, use [teaspoon](https://github.com/modeset/teaspoon) for heavy javascript testing.

- Prefer [poltergeist](https://github.com/teampoltergeist/poltergeist) over the default javascript driver, `selenium`.  Avoid [capybara-webkit](https://github.com/thoughtbot/capybara-webkit).

- There will be cases where you will be needing `selenium` to see what's going on. This snippet provides you with a `selenium: true` tag.

  ```ruby
  # rails_helper.rb
  Capybara.javascript_driver = :poltergeist

  config.before(:each) do |example|
    Capybara.current_driver = :selenium if example.metadata[:selenium]
  end

  ```


## Factories

- Always include the syntax helpers.

  ```ruby
  # rails_helper.rb
  config.include FactoryGirl::Syntax::Methods

  ```

- Prefer `build` over `create`, if you can get away with it.

- Avoid `build_stubbed`.

- Never hard code emails and similar fields that must be unique. Use `sequence`.

  ```ruby
  factory :user do
    sequence :email do |index|
      "user-#{index}@email.com"
    end

    ...
  end
  ```

- [Traits](https://github.com/thoughtbot/factory_girl/blob/master/GETTING_STARTED.md#traits) can be used to remove duplication. But use them sparingly.

- When modifying factories, do not forget to restart `spring`.

- Make sure that factories are always up to date.

- Always provide the simplest defaults for your factories.

