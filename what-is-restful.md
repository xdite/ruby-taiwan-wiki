# RESTful

## 說明

* 是一種軟體設計架構（Design Pattern），主要利用資源(Resources)來當做識別的資源。而對於網站來說，網址(Uniform Resource Locator - URL)就是指向resources的一個東西。
* 符合REST的設計方式
* 同一個resource有不同的Representations的格式變化，透過解析格式變化來判定使用者的動作，充分利用HTTP各種與網頁伺服器的溝通方式（GET、POST、PUT、DELETE...etc），例如GET是取得資源、列表，POST是建立新資源、PUT是修改現有資源內容，DELETE則是刪除指定的資源等。

## 使用情境

* 當你需要連接到其他網址的時候

## 使用方式

* redirect_to posts_path ＃index, 產生的網址 http://localhost:3000/posts
* redirect_to post_path(@post) ＃show, Rails會自己抓出@post的id 傳遞過去 http://localhost:3000/posts/post_id

## 優點

* 使用者端/伺服器端 Client/Server
* 狀態無關 Stateless
* 可以快取 Cacheable
* 分層的 Layered

## 參考資料

* ![CRUD](http://cl.ly/3W301o2v2j2J1R2Y0y0o/content)

* <http://rails.pixnet.net/blog/post/22956704>
* <http://ihower.tw/rails3/restful.html>
* <http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html>
* [[如何開始CRUD RESTFul Rails專案]]