# I18n

## 說明

* 轉換網站語言、語系的方式

## 使用情境

## 使用方式

* application_controller

        before_filter :set_locale

        def set_locale
          # 可以將 ["en", "zh-TW"] 設定為 VALID_LANG 放到 config/environment.rb 中
          if params[:locale] && I18n.available_locales.include?( params[:locale].to_sym )
            session[:locale] = params[:locale]
          end

          I18n.locale = session[:locale] || I18n.default_locale
        end

* 放轉換的html code在index.html.erb

        <%= link_to "中文版", :controller => controller.controller_name, 
           	         :action => controller.action_name, :locale => "tw"	%>
        <%= link_to "English", :controller => controller.controller_name, 
           	         :action => controller.action_name, :locale => "en" %>

        <h2><%= t "welcome.title" %></h2>
        <p><%= t "welcome.paragraph" %></p>

* 設計yml

        #en.yml
        en:
          welcome:
            title: "Welcome"
            paragraph: "Thank you for your visiting our store"
        </code></pre>
        <pre><code class="yml">
        tw:
          welcome:
            title: "歡迎光臨"
            paragraph: "歡迎來到我的叢林"
    

## 優點

## 參考資料

* <http://ihower.tw/rails3/i18n.html>
* <http://www.slideshare.net/ihower/rails-i18n-20081125-presentation>
* <http://railscasts.com/episodes/138-i18n>