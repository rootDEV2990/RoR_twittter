# Cloning Twitter with Rails 6
> Scaffolding a Rails app with user sign up, sign in, and dynamic views. Great first app for any one to try with CRUD features. The power of Rails.

## Built With

- Ruby on Rails
- sqlite3 for the local development
- VScode
- Rubocop

## Guide

1. generate Tweets (makes vies controler and models)
    rails g scaffold Tweeet tweet:text
2. migrate db
    rails db:migrate
3. updates config/routes.rb
    root to: "tweeets#index"
4. add gems to Gemfile inside dev block
    gem 'better_errors'
    gem 'guard'
    gem 'guard-livereload', require: false
5. in terminal run command
    bundle install
6. add bulma or css of choice and forms gem. 
    gem 'bulma-rails', '~> 0.6.1'
    gem 'simple_form', '~> 3.5'
7. re run bundle again in terminal
    bundle install
8. generate forms with terminal type and run cmd
    rails generate simple_form:install
    #if with bootstrap or foundation
    #rails generate simple_form:install --bootstrap
    #rails generate simple_form:install --foundation
9. add gravatar gem for easy avatars add to Gemfile
    gem 'gravatar_image_tag', '~> 1.2'
10. add devise gem for log ins and users
    gem 'devise', '~> 4.7', '>= 4.7.3'
11. run in terminal install for devise
    rails generate devise:install
12. add to config/enviroments/development.rb for mailers
    config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
13. add to app/view/application.html.erb inside body tag
    <% if flash[:notice] %>
      <div class="notification is-primary global-notification">
        <p class="notice"><%= notice %></p>
      </div>
    <% end %>
    <% if flash[:alert] %>
      <div class="notification is-primary global-notification">
        <p class="alert"><%= alert %></p>
      </div>
    <% end %>


## Author

👤 **Miguel Angel Enciso Sanchez**

- Github: [@rootDEV2990](https://github.com/rootDEV2990)
- Twitter: [@m29902](https://twitter.com/m29902)
- Linkedin: [linkedin](https://www.linkedin.com/in/miguel-enciso-6474741a1/)
- Medium: [medium](https://medium.com/@website.dev)

## 🤝 Contributing

Contributions, issues and feature requests are welcome!

## Show your support

Give a ⭐️ if you like this project!

## Acknowledgments

- Microverse
- Heroku
## 📝 License

This project is [MIT](LICENSE) licensed.

