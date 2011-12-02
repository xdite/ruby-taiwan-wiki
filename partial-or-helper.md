# 什麼東西應該放在 partial / 什麼東西應該放在 helper

## 說明

* [什麼是 helper](/wiki/what-is-helper)
* [什麼是 partial](/wiki/what-is-partial)
	
## 使用情境

* helper和partial是把邏輯判斷與頁面設計分開！
> 最簡單的區分方式：
> 只要有包含「邏輯判斷」的都應該放在helper，而單純「輸出Rails html」的就放在Partial Template（局部模版）

### 放在Helper裡的東西：

- 自動產生的html表建 - Repeating [nearly] identical statements producing a single shallow html tag?
- 超過四行ruby程式碼就建議放Helper - Common expression used as an argument or condition?
- Long expression (more than 3 terms) used as an argument for another helper?
- 4 or more lines of ruby (that is not evaluated into HTML)?

### 放在Partial的東西
- 可以自動輸出loop的部份，利用collection - Part of an iterative loop (for, each, etc)?
- AJAX返回一部分的變動 - Section that could be returned as part of an AJAX call?
- 程式碼常出現在多個view裡面 - Common code occurring in multiple views?

## 優點

* 程式碼好修改
* 程式碼好閱讀

## 參考資料

* <http://www.viget.com/extend/helpers-vs-partials-a-performance-question/>
* <http://emeryfinkelstein.ca/web-design/refactoring-views-in-rails-helpers-or-partials/>
