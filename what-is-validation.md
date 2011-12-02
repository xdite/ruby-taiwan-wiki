# Validation

## 說明

* Rails對資料庫欄位進行各種資料驗證的方法
* 確保資料儲存到資料庫之前是正確的

## 使用情境

* :acceptance => Boolean   
> 檢查使用者必須核選一個checkbox方塊
* :confirmation => Boolean
> 檢查使用者在表單必須輸入兩次的情況
* :exclusion => { :in => Enumerable }
> 檢查資料一定不會是某些值
* :inclusion => { :in => Enumerable }
> 確保資料只能是某些值
* :format => { :with => Regexp, :on => :create }
> 確保格式正確，可以用來檢查Email、網址
* :length => { :maximum => Fixnum }
> 檢查字串的長度
* :numericality => Boolean
> 檢查是數字，設定數字的大小
* :presence => Boolean
> 確保必填，用來檢查資料為非 nil 或空字串
* :uniqueness => Boolean
> 檢查資料確保唯一


## 使用方式

        class Person < ActiveRecord::Base
          validates :email, :presence => true
        end

## 優點
## 參考資料

* <http://guides.rubyonrails.org/active_record_validations_callbacks.html>
* <http://railscasts.com/episodes/211-validations-in-rails-3>
* <http://lindsaar.net/>
* <http://yehudakatz.com/2010/01/10/activemodel-make-any-ruby-object-feel-like-activerecord/>
* <http://edgeguides.rubyonrails.org/3_0_release_notes.html#validations>
* <http://thelucid.com/2010/01/08/sexy-validation-in-edge-rails-rails-3/>
* <http://ihower.tw/rails3/activerecord-lifecycle.html>