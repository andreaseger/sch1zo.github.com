--- 
layout: post
title: How to setup rails on redis
categories: 
- tumblr
- rails
- rspec
- setup
- redis
- spork
- watchr
date: 2011-07-05
---
just some steps to setup rails 3.1 with redis as database, rspec for testing
and watchr/spork to automate testing.

<!-- more -->

# scripts to run

``` sh
rails new app_name -OT
rake rspec:install
spork --bootstrap
```

# add some gems to Gemfile

``` ruby Gemfile
# Database
gem redis
gem redis_storage, >= 0.2.9

gem therubyracer    # to get coffee script running

# testing
group :test, :development do
  gem rspec-rails
  gem mocha
  gem watchr
  gem spork, ~> 0.9.0.rc
end
```

# add or edit those files

``` ruby .rspec
--colour
--format d
--drb
```

``` ruby .watchr
def run_spec(file)
  unless File.exist?(file)
    puts "#{file} does not exist"
    return
  end

  puts "Running #{file}"
  system "bundle exec rspec #{file}"
  puts
end

watch("spec/.*/*_spec\.rb") do |match|
  run_spec match[0]
end

watch("app/(.*/.*)\.rb") do |match|
  run_spec %{spec/#{match[1]}_spec.rb}
end
```

``` ruby lib/tasks/watchr.rake
desc "Run watchr"
task :watchr do
  sh %{bundle exec watchr .watchr}
end
```

``` ruby config/application.rb
config.generators do |g|
  g.orm             :redis
  g.template_engine :haml
  g.test_framework  :rspec
  g.stylesheet_engine = :sass
end
```

``` ruby spec/spec_helper.rb
require spork

Spork.prefork do
  # Loading more in this block will cause your tests to run faster. However,
  # if you change any configuration or code from libraries loaded here, youll
  # need to restart spork for it take effect.

  # This file is copied to spec/ when you run rails generate rspec:install
  ENV["RAILS_ENV"] ||= test
  require File.expand_path("../../config/environment", __FILE__)
  require rspec/rails

  # Requires supporting ruby files with custom matchers and macros, etc,
  # in spec/support/ and its subdirectories.
  Dir[Rails.root.join("spec/support/**/*.rb")].each {|f| require f}

  RSpec.configure do |config|
    config.mock_with :mocha
    config.before :each do
      $db.flushdb
    end
  end
end

Spork.each_run do
  # This code will be run each time you run your specs
end
```
