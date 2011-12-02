# Routing


## 說明

* 簡單的說，就是設定你的「網頁路徑」，連接到對應的Action Controller

## 使用情境

* 如何在網址後面再加上字串
* 

## 使用方式

        Forum::Application.routes.draw do
          # The priority is based upon order of creation:
          # first created -> highest priority.

          # Sample of regular route: Rails 3.0 以前預設的開發方式
          match 'products/:id' => 'catalog#view' 
          # Keep in mind you can assign values other than :controller and :action

          # Sample of named route: 命名路由適用於不符合CRUD的情況
          match 'products/:id/purchase' => 'catalog#purchase', :as => :purchase
          # This route can be invoked with purchase_url(:id => product.id)

          # Sample resource route (maps HTTP verbs to controller actions automatically): RESTful路由的設定方式
          resources :products

          # Sample resource route with options:
          resources :products do
            # member 需要傳進ID /products/1/short
            member do
              get 'short'
              post 'toggle'
            end
            # collection 不用傳ID  /products/sold/
            collection do
             get 'sold'
            end
          end

          # Sample resource route with sub-resources: Nests Resources
          resources :products do
            resources :comments, :sales
            resource :seller
          end

          # Sample resource route with more complex sub-resources
          resources :products do
            resources :comments
            resources :sales do
              get 'recent', :on => :collection
            end
          end

          # Sample resource route within a namespace: 這個路由方式可以在相同名稱下的resources設定不同的存取權限，如後台
          namespace :admin do
          #     # Directs /admin/products/* to Admin::ProductsController
          #     # (app/controllers/admin/products_controller.rb)
            resources :products
          end

          # See how all your routes lay out with "rake routes"

          # This is a legacy wild controller route that's not recommended for RESTful applications.
          # Note: This route will make all actions in every controller accessible via GET requests.
          # match ':controller(/:action(/:id(.:format)))'
        end


## 優點
## 參考資料

* <http://ihower.tw/rails3/routing.htm>
* <http://ihower.tw/rails3/routing.htm>
