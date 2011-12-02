# Yield in View


## 說明

* 會被替換成樣版（template）的地方
* 用來輸出樣版的內容

## 使用情境

* 製作一個版形，可以套用在很多頁面，利用yield可以輸出所想要的內容以及呈現方式

## 使用方式

* 全站版形

        #預設application layout，application.html.erb，全站的版形
        <!DOCTYPE html>
        <html>
        <head>
          <title>YourApplicationName</title>
          <%= stylesheet_link_tag    "application" %>
          <%= javascript_include_tag "application" %>
          <%= csrf_meta_tags %>
        </head>
        <body>
        
        <%= yield %>
        
        </body>
        </html>

* 如果你有指定自己的layout，就不會使用application的全站版形

        #自己設計一個常用版形，standard.html.erb
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
        <html xmlns="http://www.w3.org/1999/xhtml">
          <head>
            <title>Library Info System</title>
            <%= stylesheet_link_tag "style" %> 
          </head>
            <body id="library">
            <div id="container">
              <div id="header">
                <h1>Library Info System</h1>
                <h3>Library powered by Ruby on Rails</h3>
              </div>
              <div id="content">
                <%= yield %>
              </div>
              <div id="sidebar"></div>
            </div>
          </body>
        </html>
        

* 在Action Controller裡面調用要用的layout，就不會使用預設的application layout

        # book_controller.rb  
        class BookController < ApplicationController  
           layout 'standard'#表明我們要調用standard.html.erb作為Layout
           def list  
              @books = Book.all
           end  
        ...................

## 優點

* 未來如果需要更改版型內容，則不需要一個頁面一個頁面去更改

## 參考資料

* <http://hlee.iteye.com/blog/407640>
* <http://ihower.tw/rails3/actionview.html>
* <http://ihower.tw/rails3/ruby.html>
