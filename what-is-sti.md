# STI

## 說明

* 全名是Single-table inheritance 單一表格繼承
* 讓兩個資料表共用一個資料表，就可以使用父類別的資料表

## 使用情境

* 當資料表有很多的欄位需要共用，才使用！不然就直接開一個新的Model！

## 使用方式

        class Post < ActiveRecord::Base
            validates_presence_of :subject
        end

        class GuestPost < Post

        end

        class MemberPost < Post

        end

## 優點

* 如果資料表欄位相同，可以節省新增新的Model

## 參考資料

* <http://abitno.me/restful-routes-with-single-table-inheritance-in-rails#more_148>
* <http://ihower.tw/rails3/activerecord-others.html>
* <http://www.youtube.com/watch?v=F0KH_9ikZiA>