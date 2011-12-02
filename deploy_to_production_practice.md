本文由 xdite 授權提供，為 [Rails 101](http://rails-101.logdown.com/) 第七章部分內容

# 第一部分

## 佈署 Rails Production 所需要的環境


佈署 Rails Application 是件說簡單很簡單，說複雜也很複雜的事。佈署的手法有很多種搭配，筆者最推薦的其實是在 Ubuntu / Debian 安裝 Ruby Enterprise Edition，web sever 使用 nginx + mod_rails 的組合。之後再撰寫 Capistrano 的 recipe 來 deploy。


## 為什麼要用獨立的 Ruby 版本，而不使用系統 Ruby？


因為系統 Ruby 通常綑綁了背後的套件系統（RubyGem），Rails 是個腳步前進很快的生態圈。而各樣相依套件有時候也會限定 RubyGem 的版本。很多時候，在開發或佈署上就會踩到大地雷。

所以會建議在系統上跑獨立的 Ruby 。而 Ruby Enterprise Edition 是業界比較推薦的一個 Ruby 版本，節省記憶體，效率也較佳。所以就變成了首選。


## 為什麼要用 Ubuntu / Debian ，而不是使用 CentOS？


還是跟 Rails 是個腳步前進很快的生態圈有相當大的關係。Gem 的前進腳步很快，很多時候只 compatible 新的 library，而 CentOS 上很多 package 都已經 outdate 了。實際佈署上會踩到很多雷。而 Ubuntu / Debian 上的 package 更新速度非常快。所以也是首選。


## 有沒有 Best Practice 懶人包？


有。其實佈署真的不算是件易事，在佈署中最容易踩到的雷當數 ImageMagick ( rmagick gem) 與 MySQL ( mysql2 gem)。偏偏這幾乎是每個網站最常會用到的兩個 gem。而且裝爛了很難重裝。

因此社群前輩們就將這些血淚們整理了成一份 recipe :  [rails-nginx-passenger-ubuntu](https://github.com/jnstq/rails-nginx-passenger-ubuntu) 。


## 哪裡買域名和租 VPS？

我是在 enom.com 買域名，管理介面還算蠻好用的。

至於 VPS 是去 [linode](http://linode.com) 租的。算便宜大碗，速度上也能接受。若純練習也可到 [AWS EC2](http://aws.amazon.com/ec2/) 租東京的 micro instance。

## 裝機


請依照 [rails-nginx-passenger-ubuntu](https://github.com/jnstq/rails-nginx-passenger-ubuntu) 將需要的環境都裝好。

# 第二部分

## 佈署 Rails Application

### 開設 deploy 專用帳號 apps

    $ sudo useradd apps
    $ sudo passwd apps 
    # 設定 apps 密碼
    $ sudo mkdir /home/apps
    $ sudo chown -R apps:apps /home/apps
    # 為 apps 這個帳號開設家目錄, 並設定權限
    


變身成為 apps，產生 ssh public key，並將 id_rsa.pub 貼到 github 專案的 deploy key 。

.. code-block:: console

    $ sudo su apps
    $ ssh-keygen
    $ more ~/.ssh/id_rsa.pub

.. image:: fig/ex7-github.png

在開發本機運行 ssh-keygen，然後 more ~/.ssh/id_rsa.pub 貼到 /home/apps/.ssh/authorized_keys 內。（如此一來以後可以 deploy 時可以免密碼 ）


### 為 capistrano deploy 做前置準備
   
    $ ssh-keygen

.. warning ::
    
    實務上絕對不鼓勵把任何密碼 commit 進 SCM。因此都是把密碼放進database.yml.production，每次佈署時再 自動 symlink 過去。

database.yml.production ::

    production:
      adapter: mysql2
      encoding: utf8
      reconnect: false
      database: logdown_production
      pool: 5
      username: root
      password: '123456'

編輯 /opt/nginx/conf/nginx.conf ::

    server {
        listen 80;
        server_name forum_demo.yourdomain.com;
        root /home/apps/forum_demo/current/public;
        passenger_enabled on;
    }

# 第三部分



## Capistrano


Capistrano[https://github.com/capistrano/capistrano/wiki] 是 37 signals 開發的一套 automate deploy tool。也是許多 Rails Developer 推薦的一套佈署工具。

也許你要問，為什麼要用工具 deploy 專案呢？那是因為佈署 application 是由數道繁瑣的手續構成。首先，Rails 佈署程式並不像 php 那樣簡單，上傳檔案成功就完事了。要佈署一個 Rails Application，你必須連到遠端 server，然後 checkout 程式碼，跑一些 migration，重開 server 生效，重開 memcached，重開 search daemon ....

這些連續動作有時候往往一閃神即是災難。

而手動 deploy 在只有一個人一台機器時還勉強說得過去。當開發人員一多或機器一多，馬上就會要了大家的命。

Capistrano 固然強大，但官方網站的文件卻讓人不易讀懂。在此分享我的 deploy 步驟與 recipe。

## 設置 Capistrano

在 Gemfile 下加入這兩行
 
    gem 'capistrano'
    gem 'capistrano-ext'
  
在專案內新增 Capfile

	load 'deploy' if respond_to?(:namespace) # cap2 differentiator
	Dir['vendor/gems/*/recipes/*.rb','vendor/plugins/*/recipes/*.rb'].each { |plugin| load(plugin) }
	load 'config/deploy' # remove this line to skip loading any of the default tasks
    
新增 config/deploy.rb

	require 'capistrano/ext/multistage'
	require 'bundler/capistrano' #Using bundler with Capistrano

	set :stages, %w(staging production)
	set :default_stage, "production"
    
新增 config/deploy/production.rb

	set :application, "forum_demo"
	set :domain, "forum_demo.yourdomain.org"
	set :repository,  "git@github.com:someone/forum_demo.git"
	set :deploy_to, "/home/apps/forum_demo"

	role :app, domain
	role :web, domain
	role :db, domain, :primary => true

	set :deploy_via, :remote_cache
	set :deploy_env, "production"
	set :rails_env, "production"
	set :scm, :git
	set :branch, "master"
	set :scm_verbose, true
	set :use_sudo, false

	set :user, "apps"
	set :group, "apps"

	default_environment["PATH"] = "/opt/ree/bin:/usr/local/bin:/usr/bin:/bin:/usr/games"
	namespace :deploy do
  	  desc "restart"
  	  task :restart do
	  run "touch #{current_path}/tmp/restart.txt"
  	end
	end

	desc "Create database.yml and asset packages for production"
	after("deploy:update_code") do
  	  db_config = "#{shared_path}/config/database.yml.production"
  	  run "cp #{db_config} #{release_path}/config/database.yml"
	end

第一次使用，運行此行指令，Capistrano 就會遠端到機器上幫你把 Capistrano 所需的一些目錄和檔案先預備好

    $ cap deploy:setup

Deploy 專案到遠端

    $ cap deploy

遠端執行 migration

.. code-block:: console

    $ cap deploy:migrate

deploy 的這一版本爛了，想回到沒爛的上一版本。

    $ cap deploy:rollback

純粹重開 application

    $ cap deploy:restart


## 小結

至此，你學習到了怎麼將作品佈署到遠端 Server 上。
