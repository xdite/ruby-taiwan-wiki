# Bundler

## 說明

* 是一個管理Gem的管理工具，根據Gemfile的設定自動下載以及安裝Gem的套件，解決不同Gem之間的相互依賴的關係。

## 使用情境

* 當你需要使用其他人開發的Gem時

## 使用方式

* 在Gemfile宣告你要使用的Gem
        
        # 來源
        source 'http://rubygems.org'

        # 第二個參數指定版本
        gem 'rails', '3.1.0.rc1' 

        # Bundle edge Rails instead: 指定Git當作來源
        # gem 'rails',     :git => 'git://github.com/rails/rails.git'

        gem 'sqlite3'

        # Asset template engines
        gem 'json'
        gem 'sass'
        gem 'coffee-script'
        gem 'uglifier'

        gem 'jquery-rails'

        # Use other plugin
        gem "devise"
        # 指定:branch
        gem "will_paginate", :git => "https://github.com/p7r/will_paginate.git", :branch => "rails3"

* 修改Gemfile過後，執行在專案資料夾裡面執行bundle install，安裝所有的gem

## 優點

## 參考資料

* <http://ihower.tw/rails3/environment-and-bundler.html>