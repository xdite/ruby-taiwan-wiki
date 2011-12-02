# collect & id

## 說明

* collect
> 從字面上就是收集的意思
> 是一個iterator，會複製一份array並且返回array
> NOTE: The collect method is not the right way to do copying between arrays. There is another method called a clone which should be used to copy one array into another array.

* &:id
> id是資料庫的欄位名稱

* collect(&:id)
> 兩個合起來就是收集id的值

## 使用情境

## 使用方式

* collect(&:id)
> 取出欄位名稱為id的所有值，傳回陣列

##例子

        # 抓出所有的值，並且收集返回它的name欄位的值
        def self.all_names
            find(:all).collect(&:name)
        end

<hr>
        # 把 name 欄位取出，並改為小寫
        projects.collect(&:name).collect(&:downcase)


<hr>



        Post.all.collect(&:title) #=> ["1 week from now", "Now", "1 week ago", "2 weeks ago"]
        Post.published.collect(&:title) #=> ["Now", "1 week ago", "2 weeks ago"]

        # Search combinations
        Post.search('1').collect(&:title) #=> ["1 week from now", "1 week ago"]
        Post.search('1').published.collect(&:title) #=> ["1 week ago"]
        Post.search('w').published_since(10.days.ago).collect(&:title) #=> ["Now", "1 week ago"]
        Post.search('w').order('created_at DESC').limit(2).collect(&:title) #=> ["2 weeks ago", "1 week ago"]

## 優點

## 參考資料

* <http://edgerails.info/articles/what-s-new-in-edge-rails/2010/02/23/the-skinny-on-scopes-formerly-named-scope/index.html>
* <http://zhangcaiyanbeyond.iteye.com/blog/1007121>
* <http://cactis.pixnet.net/blog/post/16659330>
* <http://www.tutorialspoint.com/ruby/ruby_iterators.htm>
* <http://makandra.com/notes/902-preloaded-associations-are-filtered-by-conditions-on-the-same-table>