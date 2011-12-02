# Redner Layout

## 說明

* layout是包裹template樣板，讓不同View可以共用Layout作為文件的頭尾。
* layout可以為全站的頁面建立共用的版型。這個檔案預設是app/views/layouts/application.html.erb。
* 如果在app/views/layouts目錄下有跟某Controller+同名的Layout檔案+，那這個Controller下的所有Views就會使用這個+同名的Layout+。

## 使用情境

* layout預設是使用application.html.erb，如果想要為這個頁面設計特殊的layout，就可以為這個controller的設計一個專屬的layout！

## 使用方式

        #放在layout資料夾裡面的layout（maple.html.erb）
        <!DOCTYPE html>
        <html>
        <head>
        </head>

        <body>

         <%= yield %>  #這就是放template的地方

        </body>
        </html>

<hr>

        #放在Action Views 裡面的template( games/maple.html.erb)
        def show 
          render :template => "games/maple", :layout => "maple" #表示你可以layout一個專屬的頁面，帶著特定的模板與範本給show action
        end

<hr>

        render :layout "admin", :only => "index" #表示你可以layout一個專屬的頁面給index action

## 參考資料

* <http://guides.rubyonrails.org/layouts_and_rendering.html>
* <http://ihower.tw/rails3/actionview.html>
* <http://railscasts.com/episodes/7-all-about-layouts>