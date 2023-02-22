# README

* Ruby v2.7.4
* Rails v7.0.4

```
$ rails new example-project -T -d=postgresql --api

$ rails db:create

$ bundle add active_model_serializers

uncomment < gem 'bcrypt', '~> 3.1.7' > in Gemfile

$ bundle lock --add-platform x86_64-linux

Add the following to config/application.rb
    # Adding back cookies and session middleware
    config.middleware.use ActionDispatch::Cookies
    config.middleware.use ActionDispatch::Session::CookieStore

    # Use SameSite=Strict for all cookies to help protect against CSRF
    config.action_dispatch.cookies_same_site_protection = :strict

* app/controllers/application_controller.rb
    class ApplicationController < ActionController::API
    include ActionController::Cookies

    def hello_world
        session[:count] = (session[:count] || 0) + 1
        render json: { count: session[:count] }
    end
    end

* config/routes.rb
    Rails.application.routes.draw do
    # route to test your configuration
    get '/hello', to: 'application#hello_world'
    end

$ rails s
```
