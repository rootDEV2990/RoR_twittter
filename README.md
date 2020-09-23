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
14. run in terminal view generator with devise
    rails g devise:views
15. add to view/application.html.erb
    <nav class="navbar is-info">
      <div class="navbar-brand">
      
        <%= link_to root_path, class: "navbar-item" do %>
          <h1 class="title is-5">Twitter</h1>
        <% end %>
        <div class="navbar-burger burger" data-target="navbarExample">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
      <div id="navbarExample" class="navbar-menu">
          <div class="navbar-end">
            <div class="field is-grouped">
              <p class="control">
                <%= link_to 'New Tweeet', new_tweeet_path, class: "button is-info is-inverted" %>
              </p>
              <p class="control">Sign Up</p>
            </div>
          </div>
      </div>
    </nav>
16. add to assests/stylesheets/application.scss
     @import "bulma";

    .nav-brand .title {
        color: white;
    }

    // round images
    .image {
        border-radius: 50%;
        img {
            border-radius: 50%;
        }
    }
    .notification:not(:last-child){
        margin-bottom: 0;
    }
17. replace file views/tweets/index.html.erb with render for patial
  <section class="section">
    <div class="container">
      <div class="columns">
        <%= render 'feed'%>
      </div>
    </div>
  </section>
  
18. make partial file for feed and add content views/tweeets/_feed.index.html
  <div class="column is-half">
    <article class="media-box">
      <figure class="media-left">
        <p class="image is-64x64">
            <img src="https://bulma.io/images/placeholders/64x64.png">
        </p>
      </figure>
      <div class="media-content">

      </div>
    </article>

    <% @tweeets.each do |item| %>
      <div class="box">
        <article class="media">
          <div class="media-left">
            <figure class="image is-64x64">
              <img src="https://bulma.io/images/placeholders/64x64.png">
            </figure>
          </div>
          <div class="media-content">
            <div class="content"> 
              <strong>Otto</strong><br/>
              <email>@microverse</email><br/>
              <p><%= item.tweeet%></p>
            </div>
          </div>
        </article>
      </div>
    <% end %>
  </div>

19. add options to post like edit and delete in _feed.html.erb
  <div class="media-content">
    ...
  </div>
  <div class="level">
    <div class="level-left is-mobile">
      <%= link_to item, class: "level-item" do %>
        <span class="icon"><i class="fa fa-link" aria-hidden="true"></i></span>
      <% end %>
      <%= link_to edit_tweeet_path(item), class: "level-item" do %>
        <span class="icon"><i class="fa fa-pencil" aria-hidden="true"></i></span>
      <% end %>
      <%= link_to item, method: :delete, data: { confirm: "Are you sure you want to delete this tweeet?" } do %>
        <span class="icon"><i class="fa fa-trash-o" aria-hidden="true"></i></span>
      <% end %>
    </div>
20. add partial to display column with followers render who_to_follow under the feed partial
  <% render 'who_to_follow' %>
21. create new partial file _who_to_follow.html.erb add the following html
  <div class="column">
    <nav class="panel">
        <p class="panel-heading">Who to Follow</p>
    </nav>
    <div class="panel-block">
        <article class="media">
            <div class="media-left">
                <figure>
                    <img src="https://bulma.io/images/placeholders/64x64.png">
                </figure>
            </div>
            <div class="media-content">
                <div class="content">
                    <p>
                        <strong>Satoshi Nakamoto</strong>
                        <strong>@btc</strong>
                    </p>
                </div>
            </div>
        </article>
    </div>
</div>

22. implent trends column inside of index.html.erb before feed
  <%= render 'trends' %>
23. create partial file view/tweeets/_trends.html.erb and add
  <div class="column is-one-quarter">
    <nav class="panel">
        <p class="panel-heading">Trends</p>
        <a class="panel-block">
            Trend 1
        </a>
        <a class="panel-block">
            Trend 2
        </a>
        <a class="panel-block">
            Trend 3
        </a>
        <a class="panel-block">
            Trend 4
        </a>
        <a class="panel-block">
            Trend 5
        </a>
    </nav>
  </div>

24. render form to post tweeet add in _feed.html.erb
  <div class="column is-half">
    <article class="media-box">
      <figure class="media-left">
        ...
      </figure>
      <div class="media-content">
        <!--add this render line-->
        <%= render 'tweeets/form' %>
        <!--add this render line-->
      </div>
    </article>
  </div>
26. change code in _form.html.erb add our new form 
  <%= simple_form_for(@tweeet_it) do |form| %>
  <%= form.error_notification %>
  <div class="field">
    <div class="control">
      <%= form.input :tweeet, lable: "Tweeet about it", input_html: { class: "textarea"}, wrapper: false, label_html: {class: "label"}, placeholder: "Compose a new tweeet..." %>
    </div>
  </div>
  <%= form.button :submit, class: "button is-info" %>
  <% end %>
27. add @tweeet varriable in index method of tweeets_controller.rb
  @tweeet = Tweeet.new
28. make app refresh to home after user sends new tweet to db in tweeets_controller.rb
  if @tweeet.save
        #delete this line
        #format.html { redirect_to @tweeet, notice: 
        #add this one
        format.html { redirect_to root_path, notice: 'Tweeet was successfully created.' }
        format.json { render :show, status: :created, location: @tweeet }
      else


## USERS set up

1. made devise migration in terminal type   
  rails g devise User
2. run migration with rails in terminal 
  rails db:migrate
3. rake routes with rake or rails
  rails routes




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

