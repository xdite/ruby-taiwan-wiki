# Packing Gems


## What is Gem 

RubyGems 是 Ruby 的 Package 管理系統。它的作用類似 Linux 系統下的 apt-get 或者是 yum。不同的是：RubyGems 是提供「打包」好的 Ruby Library 讓開發者能夠重複利用別人已造好的輪子，提高開發效率。

而目前 Rails 3.0+ 起，幾乎都也推薦使用 RubyGems 的方式，將 Plugin 打包成 Gem 的方式搭配 Bundler 使用。

## 打包 Gem

隨著時代進步，打包和發佈 Gem 的方式一直在進步。

最早以前大家都是手工製造 ( [RailsCast #135](http://railscasts.com/episodes/135-making-a-gem) )，後來 Jeweler( [RailsCast #183](http://railscasts.com/episodes/183-gemcutter-jeweler) ) 被發明出來，讓打包變得非常容易。

而到最後，更演變成了 Bundler 內建 ( [Rails 245](http://asciicasts.com/episodes/245-new-gem-with-bundler) )。

包裝一個 Gem 變得越來越容易。

## Gem 的基本結構

若以 Bundler 內建的指令 `bundle gem GEM_NAME` 自動生出來的檔案。其實 Gem 的結構也相當簡單。

        [~/projects/exp] $ bundle gem my_plugin
              create  my_plugin/Gemfile
              create  my_plugin/Rakefile
              create  my_plugin/.gitignore
              create  my_plugin/my_plugin.gemspec
              create  my_plugin/lib/my_plugin.rb
              create  my_plugin/lib/my_plugin/version.rb
        Initializating git repo in /Users/xdite/projects/exp/my_plugin

* `Gemfile` # 描述 dependency
* `Rakefile` # 發佈和打包的 rake tasks
* `GEM_NAME.gemspec` # gem 的 spec
* `GEM_NAME/lib/GEM_NAME.rb` 與 `GEM_NAME/lib/GEMNAME/` # gem 裡的 library
* `GEM_NAME/lib/GEM_NAME/version.rb` # 版本紀錄

主要的 Library 需放置在 lib/ 底下。

若需使用到相依套件的話，需在 Gemfile 以及 .gemsepc 定義。
 
### Bundler 提供的基本 Task

Bundler 基本上算是提供半自動的打包，只提供非常基本的三個 Task：

* `rake build`    # Build my_plugin-0.0.1.gem into the pkg directory
* `rake install`  # Build and install my_plugin-0.0.1.gem into system gems
* `rake release`  # Create tag v0.0.1 and build and push my_plugin-0.0.1.gem to Rubygems

## Jeweler

若你有更多懶人需求，不妨 check [Jeweler](https://github.com/technicalpickles/jeweler) 這個 gem，它提供了更多 rake tasks 讓打包更加方便。

## Best Practices

Rails Core Team member 「Josh Peek」曾經在 Rails 官方 blog 寫過一篇文章 [Gem Packaging: Best Practices](http://weblog.rubyonrails.org/2009/9/1/gem-packaging-best-practices) 講解如何寫出比較乾淨正確的 Gem。
