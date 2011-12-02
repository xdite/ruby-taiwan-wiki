# Unobtrusive Javascript

## 說明

* Javascript的一種設計模式，讓HTML與Javascript徹底分離

## 使用情境

* Javascript放在js裡面、Html放在html檔裡面

## 使用方式


        <code class="javascript">
        //test.js
        function init()
        {
            var elem =  $("emailfield")
            Event.observe(elem, "change", validateEmail);
        }
        </code>


<hr>

        <input type="text" name="email" id="emailfield" size="40" />


## 優點


* 讓程式碼變得跟方便維護與開發

## 參考資料

* http://blog.ericsk.org/archives/699
* http://kewang.pixnet.net/blog/post/24177235
* http://railscasts.com/episodes/205-unobtrusive-javascript