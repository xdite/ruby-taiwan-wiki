# Render Template

## 說明

* 使用 render 指定要使用的樣板（template）
* rails 預設 Action Controller 會執行 render 方法，這個 render 方法會回傳預設的 template！
> 假設你的 Action Controller 名字是 `posts_controller.rb` ，裡面有 `def index`
> 你的 template 就在 `app/views/posts/index.html.erb`

## 使用情境

* 如果要 render 其他的模板，而非預設的，舉例來說，如果你的 action 是 show，那預設的 template 就是 @show.html.erb@

## 使用方式

假設要 render 的 template 是在 @app/view/books/edit.html.erb@ ，在 Rails 3 之後，這樣寫就可以了：

        def show
          render "books/edit"
        end

Rails 2.2 或更早以前的寫法：

        def show
          render :template => "books/edit"
        end

如果要 render 同 controller 裡別的 action 的 view，在 Rails 3 裡只要給該 action 的 symbol（或字串）就可以了：

        def update
          render :edit
        end

寫清楚要 render 的是 action（非必要）：

        def update
          render :action => "edit"
        end

在這裡雖然指定 action 給 rails，但只是使用 view 而已，並不會多跑該 action 在 controller 裡的動作。

## 參考資料

* <http://ihower.tw/rails3/actioncontroller.html>
* <http://rails3.blogspot.com/2010/11/render-template.html>
* <http://guides.rubyonrails.org/layouts_and_rendering.html>
* <http://edgeguides.rubyonrails.org/layouts_and_rendering.html>