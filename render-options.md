# Render Options


## 說明

### Calls to the render method generally accept four options

* :content_type
> By default, Rails will serve the results of a rendering operation with the MIME content-type of text/html (or application/json if you use the :json option, or application/xml for the :xml option.). There are times when you might like to change this, and you can do so by setting the :content_type option:

* :layout
> With most of the options to render, the rendered content is displayed as part of the current layout. You’ll learn more about layouts and how to use them later in this guide.

* :status
> Rails will automatically generate a response with the correct HTML status code (in most cases, this is 200 OK). You can use the :status option to change this:

* :location
> You can use the :location option to set the HTTP Location header

## 使用情境



## 使用方式

* :content_type

        render :file => filename, :content_type => "application/rss"

* :layout

        render :layout => "special layout"

* :status

        render :status => 500
        render :status => :forhidden

* :location

        render :xml => photo, :location => photo url(photo)

## 優點
## 參考資料

* <http://guides.rubyonrails.org/layouts_and_rendering.html>
