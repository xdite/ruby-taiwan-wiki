# Form

## 說明
* 網頁傳遞資訊的方式，收集使用者所輸入以及設定的參數，傳遞到Action Controller，來進行資料庫的操作，稱為 表單（Form）

## 使用情境
* 需要使用者輸入資料的時候

## 使用方式

        # @post是從Action Controller傳遞進來的參數，然後要把使用者輸入的資料傳遞到那裡去，用什麼方法傳遞
        <%= form_for @post, :url => post_path(@post), :html => {:method => :put} do |post| %> #前面要加上等號，表示顯示到頁面上的意思
           <%= post.label :subject, "Subject:" %>
           <%= post.text_field :subject %>
           <%= post.label :content, "Content:" %>
           <%= post.text_area :content %> 
           <%= post.submit "Update" %>
        <% end %>

## 優點
## 參考資料