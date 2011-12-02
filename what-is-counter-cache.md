# Counter Cache

## 說明

* 是rails內建的計算關連表格的資料數，像是一個討論版有很多文章，當文章新增刪除的時候，可以自動加一、減一

## 使用情境

* 需要計算數目的時候

## 使用方式

    class Post < ActiveRecord::Base
      belongs_to :board, :counter_cache => true
      belongs_to :user
    end

`rails generate migration add_posts_count_to_board`


    class AddPostsCountToBoard < ActiveRecord::Migration
      def change
        add_column :boards, :posts_count, :integer, :default => 0
      end
    end
    

`rake db:migrate`

rails就會自動的去posts_count抓數目

## 參考資料

* <http://railscasts.com/episodes/23-counter-cache-column>