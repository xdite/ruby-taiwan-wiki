# has_many :through

## 說明

* 用在多對多的關係，多對多的關係，會藉由額外的表格來連接它們的關係
* 舉例來說，一篇文章有很多的類型，一種類型也有很多的文章，藉由一個額外的文章_類型表格來關連在一起

## 使用方式

        class Post < ActiveRecord::Base
          has_many :post_categories
          has_many :categories, :through => :post_categories
        end

<hr>

        class Category < ActiveRecord::Base
          has_many :post_categories
          has_many :posts, :through => :post_categories
        end


## 優點
## 參考資料