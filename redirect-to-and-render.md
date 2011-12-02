# Redirect & Render

## 說明

* Redirect to
> 重新導向到action所指定的頁面
> 簡單的說，就是經過action controller的，在由action來重新收集、整理頁面所需的資訊

* Render
> 給予你適合的template，然後呈現html給你
> 簡單的說，不經過Action controller，單純的到那個頁面上

## 使用情境

* Redirect to
> 當你需要把Action Controller收集、處理、整理好的傳送到頁面上

* Render
> 當你只是需要回到上個頁面，並且保留剛剛輸入的值

## 使用方式

* Redirect to

        redirect_to admin_posts_path

* Render

        render :action => "edit"
        
## 優點

## 參考資料

* <http://markmail.org/message/lbcpv7hzlhvatxxq>
* <http://ihower.tw/rails3/actioncontroller.html>