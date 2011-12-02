# Scope

## 說明

* 主要是將常用的查詢條件宣告起來重覆使用
* 針對資料庫設計欄位限制、或者選取資料的範圍

## 使用情境

* 當有過於複雜的資料查詢
* 當有重覆使用的資料查詢

## 使用方式

* 沒帶參數的方式

        scope :public, where( :is_public => true )
          
* 帶有參數的方式

        class Product < ActiveRecord::Base 
          scope :cheap, cheaper_than(5)

          def self.cheaper_than(price)  
            where("price < ?", price)  
          end  
        end
        </cod

* 可以串接在一起，順序沒有影響
        
        class Event < ActiveRecord::Base
          scope :public, where( :is_public => true )
          scope :recent_three_days, where(["created_at > ? ", Time.now - 3.days ])
        end


        Event.public.recent_three_days

## 優點
## 參考資料

* <http://edgerails.info/articles/what-s-new-in-edge-rails/2010/02/23/the-skinny-on-scopes-formerly-named-scope/index.html>
* <http://asciicasts.com/episodes/215-advanced-queries-in-rails-3>