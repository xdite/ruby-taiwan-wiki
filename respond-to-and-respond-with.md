# respond_to 與 respond\_with

## 說明

* Respond to
在Rails 2用來回應不同資料格式的，對於XML request，回應XML的格式，缺點是如果需要在action裡面回應各種格式的需求，會顯得的笨重！

* Respond with
在Rails 3，搭配respond_to，利用respond_with取代繁重的程式碼

## 使用情境

## 使用方式

        # respond_to
        def index  
          @products = Product.all  
          respond_to do |format|  
            format.html  
            format.xml { render :xml => @products }  
          end  
        end 

        #respond_with
        class ProductsController < ApplicationController  
          respond_to :html, :xml  

          def index  
            @products = Product.all  
            respond_with @products  
            end  
          end  

          # Other methods  
        end

## 參考資料

* <http://asciicasts.com/episodes/224-controllers-in-rails-3>