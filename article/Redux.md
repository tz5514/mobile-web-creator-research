# Redux 介紹
Redux 是 JavaScript 的狀態容器，提供可預測化的狀態管理。它從 Facebook 所提出的 [Flux](https://facebook.github.io/flux/) 所演變而來，但避開了 Flux 的複雜性，非常的簡單易用。

Redux 由 React 社群大神 Dan Abramov 所開發，日前他被 Facebook 招募，Redux 也成為官方項目，成為前端狀態管理的主流解決方案，並且由於 Reudx 跟 React 沒有相依關係，所以亦可以單獨使用或搭配其他前端框架使用。

## 三大原則
### 單一資料來源
整個前端應用的 State 都被儲存在一顆 Object Tree 當中，成為唯一的 Store，而所有 React 的 Component 都共享這一個 Store 中的資料。由於是單一的 State tree ，測試也變得非常容易。在開發中，你可以把應用的 state 保存在本地，從而加快開發速度。此外，受益於單一的 State tree ，以前難以實現的如「撤銷/重做」這類功能也變得輕而易舉。

### State 是唯讀的
唯一改變 state 的方法就是觸發 Action，Action 是一個用於描述已發生事件的普通物件。

這樣確保了 View 和 AJAX 等請求都不能直接修改 State，它們只能表達想要修改的意圖。因為所有的修改都被集中化處理，且嚴格按照一個接一個的順序執行，因此也不用擔心 Race condition 的出現。

### 使用純函數來執行 State 的修改
Action 只是描述了發生了什麼行為，而描述 Action 如何真正改變 State tree ，你需要編寫 Reducer。

Reducer 只是一些純函數，它接收先前的 state 和 action，並返回新的 state。Reducer 負責真正將資料合併或取代到 Store 當中，因此在此處不應該進行無法預期結果的操作，例如計算隨機值或是發送一個 AJAX Request，這些操作你應該透過在非同步 Action 時來完成。

Redux 與 React 搭配可以達到非常好的單向資料流效果，讓前端 UI 的所有狀態變得可預期，更容易維護與測試，且簡單易用。
