# includes

## 說明

* 這是使用在資料庫的搜尋上，對應於資料庫的in指令，可以一次把想找的資料，

## 使用情境

### 避免N＋1Query的問題（嚴重的拖慢效能！）

* 使用一般的搜尋方式
  user.car.name  #這個方法會丟出十一次的Query，先找出使用者的資料，再依照使用者的資料一筆一筆把使用者擁有汽車的名字抓出來
* 使用includes的搜尋方式
  User.include(:car) #一開始會抓出使用者的資料，然後利用sql in的方式抓出所有的資料

## 使用方式

* 使用在controller裡面

    # your controller
    def index
      @users = User.include(:car).paginate( :page => params[:page], :per_page => 20 )
    end
    
* 使用在model裡面

    # your model
    class User < ActiveRecord::Base
      has_one :foo, :include => [:bar]
    end

## 優點：

* 大幅減低資料庫Query的次數

## 參考資料：

* <http://ihower.tw/rails3/performance.html>
* <http://ihower.tw/blog/archives/1766>
* <http://www.1keydata.com/tw/sql/sqlin.html>