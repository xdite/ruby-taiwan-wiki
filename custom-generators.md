## 說明

自從 Rails 3.0 之後，Generators 寫作方式開始基於 [Thor](https://github.com/wycats/thor)。Thor 提供了一系列利於處理檔案的 API 。 

## Getting Started

`rails generate` 是 Rails 的 generator 指令。

你可以利用這個指令，搭配 Rails 內建或 Gem 提供的 generator，快速產生需要的檔案。

        Usage: rails generate GENERATOR [args] [options]

        General options:
          -h, [--help]     # Print generator's options and usage
          -p, [--pretend]  # Run but do not make any changes
          -f, [--force]    # Overwrite files that already exist
          -s, [--skip]     # Skip files that already exist
          -q, [--quiet]    # Suppress status output

        Please choose a generator below.

        Rails:
          assets
          controller
          generator
          helper
          integration_test
          mailer
          migration
          model
          observer
          performance_test
          plugin
          resource
          scaffold
          scaffold_controller
          session_migration

        Coffee:
          coffee:assets

        Jquery:
          jquery:install

        Js:
          js:assets

### 開始建造第一支 Generator

不過在這裡我們要作的是，產生一支自己寫的 Generator。以產生一支 Initializer 為例。

`$ rails generate generator Initializer`

便會在 Rails project 下產生這些檔案 : 

        create  lib/generators/initializer
        create  lib/generators/initializer/initializer_generator.rb
        create  lib/generators/initializer/USAGE
        create  lib/generators/initializer/templates

> Note : ``$ rails generate generator`` 可以觀看詳細說明：

        Usage:
          rails generate generator NAME [options]

        Options:
          [--namespace]       # Namespace generator under lib/generators/name
                              # Default: true
          [--skip-namespace]  # Skip namespace (affects only isolated applications)
          [--old-style-hash]  # Force using old style hash (:foo => 'bar') on Ruby >= 1.9

        Runtime options:
          -q, [--quiet]    # Supress status output
          -f, [--force]    # Overwrite files that already exist
          -p, [--pretend]  # Run but do not make any changes
          -s, [--skip]     # Skip files that already exist

        Description:
            Stubs out a new generator at lib/generators. Pass the generator name as an argument,
            either CamelCased or snake_cased.

        Example:
            `rails generate generator Awesome`

            creates a standard awesome generator:
                lib/generators/awesome/
                lib/generators/awesome/awesome_generator.rb
                lib/generators/awesome/USAGE
                lib/generators/awesome/templates/

#### 解釋

檔案 `lib/generators/initializer/initializer_generator.rb` : 

        class InitializerGenerator < Rails::Generators::NamedBase
          source_root File.expand_path('../templates', __FILE__)
        end

* 這個 Generator 的名字就叫做 Initializer。若你時候再執行一次 `rails generate`。可以看到已經新增了一個 generator 叫 Initializer。

        Initializer:
          initializer

* `source_root` 這一行是表示 template 檔案放在這個資料夾下的 templates 資料夾下。也就是 `lib/generators/initializer/templates` 下。

#### Generator Template

為了要了解 Generator Template 是怎麼運作的。讓我們來新增一個檔案吧 : `lib/generators/initializer/templates/initializer.rb`。

內容是

        API_KEY = "secret_number_1234"

再修改 `lib/generators/initializer/initializer_generator.rb` 加入一行 `copy_file`。

        class InitializerGenerator < Rails::Generators::NamedBase
          source_root File.expand_path("../templates", __FILE__)

          def copy_initializer_file
            copy_file "initializer.rb", "config/initializers/#{file_name}.rb"
          end
        end

> Note : `copy_file` 是 Thor 的 API

接著執行我們客製的 Generator：

`$ rails generate initializer api_key`

        create  config/initializers/api_key.rb

這個 Rails project 下的 `config/initializers` 目錄下就會產生一個 `api_key.rb` 。內容是由剛剛的 initializer.rb 拷貝過去的。

### Thor API

Thor 提供了很多客製 [API](http://rdoc.info/github/wycats/thor/master/Thor/Actions.html)，可以讓你做更多的事。

#### gem 

若要在 Gemfile 下自動新增 dependency，新加入  `add_rspec_and_device_to_gemfile` 這個 method，使用 `gem` 這個 Thor API。

        class InitializerGenerator < Rails::Generators::NamedBase
          source_root File.expand_path("../templates", __FILE__)

          def copy_initializer_file
            copy_file "initializer.rb", "config/initializers/#{file_name}.rb"
          end

          def add_rspec_and_device_to_gemfile
            gem("rspec", :group => "test", :version => "2.1.0")
            gem("devise", "1.1.5")
          end
        end

執行： `$ rails generate initializer api_key`

Rails project 下的 Gemfile 最底端就會自動產生這兩行：

        gem "rspec", "2.1.0", :group => "test"
        gem "devise", "1.1.5"

#### application

`application` 這個 API

          application "config.asset_host = 'http://example.com'"

會自動在 `application.rb` 裡面新增 `config.asset_host`。 

#### 其他

其他可能會比較常用到的 API ：

* plugin
* git
* vendor
* lib
* rakefile
* generate
* rake

## 客製 Rails 自己的 Generators
TODO

## 撰寫 template 搭配 rails new

這是一個典型的 generator template。可以搭配 `rails new` 使用

        gem("rspec-rails", :group => "test")
        gem("cucumber-rails", :group => "test")

        if yes?("Would you like to install Devise?")
          gem("devise")
          generate("devise:install")
          model_name = ask("What would you like the user model to be called? [user]")
          model_name = "user" if model_name.blank?
          generate("devise", model_name)
        end

執行 `rails new thud -m template.rb`

甚至你可以把 teamplte 放在 gist 裡。

`rails new thud -m https://gist.github.com/722911.txt`

## 客製有 Namespace 的 generator 

`$ rails generate generator rails/generators/my_plugin/config`

打開 `lib/generators/rails/generators/my_plugin/config/config_generator.rb`

把內容

        class Rails::Generators::MyPlugin::ConfigGenerator < Rails::Generators::NamedBase
          source_root File.expand_path('../templates', __FILE__)
        end

替換成
        module MyPlugin
          module Generators
            class ConfigGenerator < Rails::Generators::Base
              source_root File.expand_path('../templates', __FILE__)
            end
          end
        end

這樣就能造出

        MyPlugin:
          my_plugin:config

#### 參考資料：
<http://stackoverflow.com/questions/3091909/creating-a-ruby-on-rails-3-gem-with-a-generator-incl-namespace>

## 把 Genertor 包進 Rails Gem

如何打包 Gem 可看 [包裝 Gem](/wiki/packing-gems) 一節。

現在我們要做的是把 Generator 搬到 Gem 裡面去。假設你實驗中的 gem 在同目錄下的 my\_plugin 目錄下。修改 `Gemfile` 將這一行加入：

        gem "my_plugin", :path => "../my_plugin"

然後運行

`$ bundle check`。

執行 `$ mv lib/generators/ ../my_plugin/lib/` 把寫好的 generator 搬過去。


這樣就完成了搬家動作。可以執行 `$ rails generate `看看

        MyPlugin:
          my_plugin:config

是否還在。如果還在就是搬成功了。

待你發佈完新的 Gem，就可以把 Gemfile 中的 `:path => ` 這一段拿掉。

> Note: `:path =>` 是 Bundler 內讓開發者測試 local 開發中 Gem 的方法。

## 相關連結：

* <http://guides.rubyonrails.org/>