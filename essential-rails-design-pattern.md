## [[前言| erp-preface ]]

* 為什麼你需要買這本書？
* 維護擴充性的重要性
* 沒有書教你怎麼寫出好的（ Rails ）程式碼
* 每一行都是實戰

## 第一章：The Basic

### 散發著腐臭味的程式碼 ( Code With Bad Smells )
### Readability: 修正不好的程式寫作習慣
### Consistency: 矯正不適當的 Coding Style
### Maintainability: 收納被隨意亂扔的程式碼
### 避免濫用 Rails 內建機制
### DRY: 重複發明輪子

## 第二章：運用 Rails 內建機制整理程式碼

### Anti-patterns

* View : 超過 2.5 頁請注意
* View : 同樣用途的 helper 出現第三次請注意
* Controller : 類似的 code 在同一個 controller 出現第3次請注意
* Controller : 相同的 method 在不同 controller 出現第二次出現請注意
* Controller : 類似形式的 controller 出現第二次請注意
* MVP : Model - View - Presenter
* 儲存之前、儲存之後需要 do something
* Fat Method : 單一 method 超過 15 行請注意
* Model: 類似作用與名稱的 Model 超過 2 個請注意
* column 超過 10 個請注意
* CRUD-LIKE action
* Asset Pipeline

### How to organize codes?

* Model
* View
* Function Partial
* Controller 
* Helper
* CSS
* Library
* Gem

## 第三章：運用 3rd party gem 整理程式碼

* CanCan ( Permission)
* SettingLogin ( Settings )
* Cells ( Cache)
* DelayedJob ( Expensive Job )
* whenever ( Crontab )

## 結語

* What is Good Code?
* How to write Good Code?
* References

