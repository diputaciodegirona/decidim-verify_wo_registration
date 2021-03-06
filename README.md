# Decidim::VerifyWoRegistration

Adds the hability for proposals and budgets components to allow users to give support without being registered. Enabling this feature the user is requested for verification and then, on success, logged in in a 30min session..

## Usage

VerifyWoRegistration will be available as a Component for a Participatory
Space.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'decidim-verify_wo_registration'
```

And then execute:

```bash
bundle
```

## Usage

This module allows admins to enable participants to open sessions from Proposals and Budgets components (login in) without being registered.

For this feature to be enabled admins should do two things:

- navigate to the corresponding component, select the "Enable suports without registration (user only verifies)" ("Poder donar suports sense registre (només verificant-se)") check and save.
- navigate to this component's permissions, and select a direct verifier for some of its actions. Note that multi-step verifiers are not supported.

This will enable the feature in the public views.

Once enabled, non registered (thus not logged in) participants will have to navigate to the given component (a proposal or a budget) and click in the support/vote/select project action. The login modal now will have a new "I have no user and I do not want to" button that takes the participant to a verification screen. Once the user is correctly verified, a 30min session starts for her to participate.

Note that although the only way for participants to open a session is by clicking the "Support" button, once verified, she will be able to perform all the actions that require the authentications she has verified for.

### Run tests

Create a dummy app in your application (if not present):

```bash
bin/rails decidim:generate_external_test_app
cd spec/decidim_dummy_app/
bundle exec rails decidim-verify_wo_registration:install:migrations
RAILS_ENV=test bundle exec rails db:migrate
```

Edit dummy_app's `config/application.rb` file to enforce railties ordering:
```ruby
module DecidimDepartmentAdminTestApp
  class Application < Rails::Application

...
    config.railties_order = [Decidim::Core::Engine, Decidim::DepartmentAdmin::Engine, :main_app, :all]
...

  end
end
```

And run tests:

```bash
bundle exec rspec spec
```

## Contributing

See [Decidim](https://github.com/decidim/decidim).

## License

This engine is distributed under the GNU AFFERO GENERAL PUBLIC LICENSE.
