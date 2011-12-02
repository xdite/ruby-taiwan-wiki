# Render Text


## 說明

* render純文字的字串

## 使用情境

* Rendering pure text is most useful when you’re responding to AJAX or web service requests that are expecting something other than proper HTML.

## 使用方式

        render :text => "OK"
        #By default, if you use the :text option the text is rendered without using the current layout. If you want Rails to put the text into the current layout, you need to add the :layout => true option.
        
<hr>

        render :text => csv_string

## 優點
## 參考資料

* <http://ihower.tw/rails3/actioncontroller.html>
* <http://rails3.blogspot.com/2010/11/render-template.html>
* <http://guides.rubyonrails.org/layouts_and_rendering.html>
