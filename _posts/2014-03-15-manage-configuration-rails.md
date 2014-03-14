---
layout: post
title: Managing Configuration in Ruby on Rails Application
sitemap:
  lastmod: 2014-03-15
  priority: 0.7
  changefreq: monthly
---


**Motivation**

Almost all applications have global variables. Including your API Keys, Enviroment Specific variables etc. Turns out there are multiple ways to set them. Either you can hard-code it or can setup a seperate file and load it form there.


**Research**

1. [Seperate File Inside Application](http://railscasts.com/episodes/85-yaml-configuration-revised?) - This is a clean way to do it. But not the best. Reason is you might end up using some library/plugin where you will need to use some of the configuration before hand. For e.g. API key in an Initializer. Or just don't want your team to see the production config and end up being a [story](http://thedailywtf.com).
2. [DOT files](http://dotfiles.github.io) - We have been using this since ages. And seems fair and more secure and more geeky. 

**Usage**

There is a [Gem]() called [dotenv-rails](https://github.com/bkeepers/dotenv) for same. Make sure to load that gem before anyother gems relying on the configuration in Gemfile.

Now you can use `.env.<enviroment-specific>` file to store your configuration. Even [YAML](http://docs.ansible.com/YAMLSyntax.html) like syntax is supported.

For e.g.,

Configuration for development env goes in:

/.env.development

```
ig_client_id=<yourid>
ig_client_secret=<secret>
ig_redirect_url=localhost:4000/callback
```

And this are available in ENV variable inside your application as follows,

/initializers/instagram.rb 

```ruby
Instagram.configure do |config|
  config.client_id = ENV['ig_client_id']
  config.client_secret = ENV['ig_client_secret']
end

CALLBACK_URL = ENV['ig_redirect_url']
```
