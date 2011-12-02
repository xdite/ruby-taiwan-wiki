# Filters : before_filter

## 說明

* 可以將Action Controller裡面重覆的程式碼獨立出來！
* 會在Action Controller被執行之前，就會現執行before filter！

## 使用情境

* 當超過兩個以上的action都出現相同的程式碼

## 使用方式
        class PostsController < ApplicationController
          before_filter :find_post, :only => [:show, :edit, :update, :destroy]
          before_filter :find_board, :only => [:index, :create, :edit, :update, :destroy]

        #.
        #.
        #.
        #.

        protected 
        def find_post
          @post = Post.find(params[:id])
        end
        def find_board
          @board = Board.find(params[:board_id])
        end
        
        
## 優點

* 可以降低撰寫的程式碼的行數
* 保持程式碼的乾淨

## 參考資料

* <http://ihower.tw/rails3/basic.html>
* Rails開發者必備的學習手冊