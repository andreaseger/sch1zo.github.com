---
layout: post
title: "sinatra sprockets and websockets"
date: 2012-03-10 16:14
comments: true
categories: 
- sinatra
- sprockets
- websockets
---

The last few days I tried to run a sinatra application which uses
sprockets for it's assets together with EventMachnine Websockets from
within one rackup file. To get this working I had to setup two things.

<!-- more -->

# Sprockets from within Sinatra

First run the Sprockets Environment within the sinatra application.
Previously I just ran it seperatly and just mapped it to '/assets', now
I have a created a Assets Module which just provides me with the
sprockets environment.

``` ruby assets_helper.rb
module Assets
  module Helpers
    def asset_path(source)
      "/assets/" + ::Assets.sprockets.find_asset(source).digest_path
    end
  end
  def self.sprockets
    return @sprockets if @sprockets
    compass_gem_root = Gem.loaded_specs['compass'].full_gem_path
    @sprockets = Sprockets::Environment.new { |env| env.logger =
Logger.new(STDOUT) }
    @sprockets.append_path File.join 'assets', 'javascripts'
    @sprockets.append_path File.join 'assets', 'stylesheets'
    @sprockets.append_path File.join 'assets', 'images'
    @sprockets.append_path File.join
Gem.loaded_specs['compass'].full_gem_path, 'frameworks', 'compass',
'stylesheets'
    @sprockets.append_path File.join
Gem.loaded_specs['compass'].full_gem_path, 'frameworks', 'compass',
'stylesheets', 'compass'
    @sprockets.append_path File.join
Gem.loaded_specs['compass-susy-plugin'].full_gem_path, 'sass'
    @sprockets
  end
end
```

Within the sinatra application I now just have to require the assets
module and forward get requests to '/assets/*' to the sprockets
environment.

``` ruby app.rb
require_relative 'lib/asset_helper'

class App < Sinatra::Base
  set :root, File.dirname(__FILE__)
  set :public_folder, File.join(root, 'public')

  get '/assets/*' do
    new_env = env.clone
    new_env["PATH_INFO"].gsub!('/assets','')
    ::Assets.sprockets.call(new_env)
  end
end
```

Via `assets_path` from the Assets::Helpers module I can now add the
assets to my views.

# Adding Websockets

The Second part is to add EventMachine::Websockets and start them
correctly.
Here is a simple chat/echo websocket example.

``` ruby ws_app.rb
@channel = EM::Channel.new

EventMachine::WebSocket.start(host: '0.0.0.0', port: 8080) do |ws|
  ws.onopen {
    sid = @channel.subscribe { |msg|
            ws.send msg.to_json
          }
    @channel.push(sid: sid, msg: 'connected!')

    ws.onclose {
      @channel.unsubscribe(sid)
      @channel.push(sid: sid, msg: 'disconnected!')
    }

    ws.onmessage { |msg|
      m = JSON.parse msg
      @channel.push(sid: sid, msg: m['msg'])
    }

    ws.onerror { |error|
      puts "Error occured: " + error.message
    }
  }
end
```

Now lets hock up all parts together in config.ru

``` ruby config.ru
require './app'

EventMachine.run do
  require './ws_app'

  App.run!
end
```

Thats all you now just have to run the application on a other port than
the EventMachine::Websockets listens to.
