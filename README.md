### bower-rails
---
https://github.com/rharriso/bower-rails

```
gem "bower-rails", "~> 0.11.0"
rails g bower_rails:initialize json
rails g bower_rails:initialize

```

```js
//= require d3/d3
//= require underscore/underscore

# ./vendor/asets/bower_components
asset "backbone"
asset "moment", "2.0.0"
asset "secret_styles", "git@github.com:initech/secret_styles"
asset "secret_logic", "1.0.0", git: "git@github.com:initech/secret_logic"
asset "secret_logic", github: "1.0.0", ref: '0adff'
asset 'secret_logic', github: "initech/secret_logic", "initech/secret_logic"
asset "three.js", "https://raw.github.com/mrdoob/three.js/master/build/three.js"


assets_path "assets/my_javascripts"
assets "backbone"
asset "moment"

assets_path "assets/javascript"
group :vendor, :assets_path => "assets/js" do
  asset "jquery"
  asset "backbone", "1.1.1"
end
group :lib do
  asset "jquery"
  asset "backbone", "1.1.1"
end

asset "moment", "2.10.1", main_files: ["./locale/en-gb.js"]
asset "moment", "2.10.1" do
  main_files [
    "./locale/en-gb.js",
    "./locale/fr.js",
    "./locale/lv.js"
  ]
end

asset "backbone", "1.1.1"
dependency_group :dev_dependencies do
  asset "jasmine-sinon"
  asset "jasmine-matchers"
end
dependency_group :dependencies do
  asset "emberjs"
end

resolution "angular", "1.2.22"

```

```json
{
  "lib": {
    "name": "bower-rails generated lib assets",
    "dependencies": {
      "threex": "git@github.com:rharriso/threex.git",
      "gsvpano.js": "https://github.com/rharriso/GSVPano.js/blob/master/src/GSVPano.js"
    }
  },
  "vendor": {
    "name": "bower-rails generated vendor assets",
    "dependencies": {
      "three.js": "https://raw.github.com/mrdoob/three.js/master/build/three.js"
    }
  }
}

{
  "name": "dsl-generated-dependencies".
  "dependencies": {
    "backbone": "1.1.1",
    "angular": "1.2.18"
  },
  "devDependencies": {
    "jasmine-sinon": "latest",
    "jasmine-matchers": "latest"
  }
}

{
  "name": "dsl-generated-dependencies",
  "dependencies": {
    "angular": "1.2.22"
  },
  "resolutions": {
    "angular": "1.2.22"
  }
}

```

```ruby
BowerRails.configure do |bower_rails|
  bower_rails.root_path = Dir.pwd
  bower_rails.install_before_precomile = true
  bower_rails.resolve_before_precompile = true
  bower_rails.clean_before_precompile = true
  bower_rails.exclude_from_clean = ['moment']
  bower_rails.use_bower_install_deployment = true
  bower_rails.user_gem_deps_for_bowerfile = true
  bower_rails.force_install = true
  bower_rails.bower_components_directory = 'bower_components'
end

module YourAppName
  class Application < Rails::Application
    require "#{Rails.root}/config/initializers/bower_rails.rb"
  end
end

namespace :bower do
  desc 'Install bower'
  task :install do
    on roles(:web) do
      within release_path do
        with rails_env: fetch(:rails_env) do
          execute :rake, 'bower:install CI=true'
        end
      end
    end
  end
end
before 'deploy:compile_assets', 'bower:install'
```
