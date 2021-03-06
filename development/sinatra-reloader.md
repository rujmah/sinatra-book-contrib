Sinatra::Reloader
-----------------

The `sinatra-reloader` gem offers a faster alternative, that also works on
Windows and JRuby. It only reloads files that actually have been changed and
automatically detects orphaned routes that have to be removed. Most other
implementations delete all routes and reload all code if one file changed,
which takes way more time than reloading only one file, especially in larger
projects.

Install it by running

    gem install sinatra-reloader

If you use the top level DSL, you just have to require it in development mode:

    require "sinatra"
    require "sinatra/reloader" if development?
    
    get('/') { 'change me!' }

When using a modular style application, you have to register the
`Sinatra::Reloader` extension:

    require "sinatra/base"
    require "sinatra/reloader"
    
    class MyApp < Sinatra::Base
      configure :development do
        register Sinatra::Reloader
      end
    end

For safety and performance reason, Sinatra::Reloader will per default only
reload files defining routes. You can, however, add files to the list of
reloadable files by using `also_reload`:

    require "sinatra"

    configure :development do |config|
      require "sinatra/reloader"
      config.also_reload "models/*.rb"
    end


