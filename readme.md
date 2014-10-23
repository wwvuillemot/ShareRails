Introduction
======

This project is composed of three (3) `git` repositories.  It is meant as a
proof of concept on how to share components such as CSS, JS, and even HTML
templates between different app frameworks using [Bower](http://bower.io).

  * **[ShareCLAF](http://github.com/wwvuillemot/ShareCLAF)** This repo
  * **[ShareRails](http://github.com/wwvuillemot/ShareRails)** Describes how to setup Bower with Rails
  * **[ShareAngularJS](http://github.com/wwvuillemot/ShareAngularJS)** Describes how to setup Bower with AngularJS

Configuration
=======

`/.bowerrc`
----------

Add `.bowerrc` to the root of your Rails app.  This tells `bower` where to install
any dependencies.

    {
        "directory": "vendor/assets/components"
    }

`/bower.json`
----------

Add `bower.json` to the root of your Rails app.  This will include your CLAF
dependencies.

    {
      "name": "share-rails",
      "private": true,
      "dependencies": {
        "claf": "https://github.com/wwvuillemot/ShareCLAF.git"
      }
    }

`/config/application.rb`
----------

Modify `application.rb` to include the `bower` installed components.  This will
append the `bower` directory to our assets pipeline.

    module RailsShare
      class Application < Rails::Application
        # Use bower for dependencies
        #
        # We also need a file at with the same directory called out
        # PROJECT_ROOT/.bowerrc
        # {
        #     "directory": "vendor/assets/components"
        # }
        config.assets.paths << Rails.root.join('vendor', 'assets', 'components')
      end
    end

`/app/assets/application.css`
----------

Modify `application.css` to include our CLAF `less` file.  Given that our CLAF
is the root dependency for everything else we do, make sure it goes first.

    *= require 'claf'
    *= require_self
    *= require_tree .
