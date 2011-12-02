# Polymorphic Assoiciaion

## 說明

透過 polymorphic association，可以讓一個 model 同時屬於數個 model。

## 使用情境

假設網站裡有 Article、Photo、Event 三個 model，都希望可以讓使用者加入 comment，因此可能需要三種 comment model。

若設定 polymorphic association，則可讓一個 Comment model 同時為上述三個 model 加入 comment。

## 使用方式

Step 1. 建立 Comment model
> 一開始必須新增 model，裡面包含 #{model_name}able_id 是整數，表示哪些 record 有關連到這個 comment；
> \#{model_name}able_type 儲存關連到 comment 的 model name。

    rails generate model Comment content:text commentable_id:integer commentable_type:string
    
Step 2. 設定 Common model 有 polymorphic association 關係
    
    class Comment < ActiceRecord::Base
      belongs_to :commentable, :polymorphic => true
    end

Step 3. 為每個需要 comment 的 model 建立 polymorphic association 到 Comment model，透過 commentable

    class Article < ActiceRecord::Base
      has_many :comments, :as => :commentalbe
    end

## 參考資料

* <http://railscasts.com/episodes/154-polymorphic-association>
* <http://asciicasts.com/episodes/154-polymorphic-association>
* <http://edgeguides.rubyonrails.org/association_basics.html#polymorphic-associations>