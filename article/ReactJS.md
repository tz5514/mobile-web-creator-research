# ReactJS 介紹
React 是 Facebook 在 2013 年所發表的一個處理前端 UI 的開源函式庫。Facebook 創造了 React 是為了解決構建一個大型且資料變動複雜的前端應用程式時所遇到的問題，它也已經被官方用於建構 Web 版本的 Facebook 和 Instagram 服務。

基於 HTML 的前端 UI 開發正變得越來越複雜，其本質問題基本上都可以歸結於如何將後端與使用者輸入的操作資料能夠動態且高效的反映到複雜的 UI 上，並且有系統的進行前端的資料管理以及測試。而來自 Facebook 的 React 正是完全根據此問題而生的一個解決方案。相較於傳統的前端開發，React 開闢了一個相當另類的途徑，實現了前端 UI 的高效率、高性能開發。

## 僅僅是 UI
React 本身並不是一個完整的 MVC 框架，最多可以說是 MVC 中的 V（View），甚至 React 並不非常認同傳統的 MVC 開發模式。因此， Facebook 針對 React 提出了一個配套的前端資料管理的架構概念 ─ [Flux](https://facebook.github.io/flux/)，以構成一套完整的前端解決方案。然而，Flux 只是一個資料流概念，而非定型的程式碼框架，這樣的基礎概念激盪出了社群上的各種 Flux 實作版本，例如其中最主流的 [Redux](https://github.com/rackt/redux)。

因此，比起單純的庫或框架，React 更像是一個只定義好骨幹的開放性生態系，靠著 Facebook 官方以及技術社群的力量共同成長茁壯。

## 聲明式的定義前端 UI
為了讓基於 HTML 所建構出來的 UI 能夠有良好的可組合性和可重用性，React 決定捨棄傳統的 HTML 開發模式，改由 JavaScript 來全面代管 HTML 的渲染與 DOM 操作。

開發者不必再先寫好 HTML 的基礎結構後再使用 JavaScript 來手動操作這些 HTML DOM 的變更，而是將該如何組合與渲染你的 UI 以及 UI 會有的互動事件，都聲明在 JavaScript 程式碼中，然後 React 會根據你的定義將其動態的產生並操作真正的 HTML DOM，以實現 UI 畫面的渲染與變更。

在傳統的前端開發模式中，HTML 只扮演了「定義 UI 最初的基礎 DOM 結構」的角色，所有在 JavaScript 中進行的 DOM 操作都是基於最初定義好的 DOM 再另外堆疊上去的變更，這讓前端 UI 程式碼的執行結果變得難以預測與維護。而 React 希望讓 HTML 退居為建構 UI 的小細胞，並在其之上建構一層虛擬的組件邏輯來管理 UI，這讓前端 UI 程式碼的的可預測性和可維護性大幅提升，這正是 React 最有價值之處 ── 聲明式的，直觀的定義方式。

以下是使用 React（ES6 語法）來定義一個按下之後會跳出 Alert 的按鈕的範例：
```js
class AlertButton extends React.Component {
  handleClick() {
    alert('我是一個通知');
  }
  render () {
    return (
      <button id="btn" onClick={this.handleClick}>我是一個按鈕</button>
    )
  }
};
```

### Virtual DOM
DOM 操作的效能成本非常的高，React 為了解決開發者在手動操作 DOM 時可能造成的效能低落或失誤，建立了一套虛擬 DOM（Virtual DOM，以下簡稱 VDOM）的機制，程式記憶體中將有一份對應真正 DOM 的 VDOM 物件，以代管 UI 儲存的資料與邏輯。當一個 UI 因為資料改變而需要進行畫面變動的時候，React 會根據新的 UI 狀態重繪一份新的 VDOM Tree，並且與變動前的舊 VDOM Tree 以高效率的 Diff 演算法進行比對，然後其中的差異才會真正的由 React 自動幫你更新到實際的 DOM 上，反應出畫面的變更。

透過 VDOM 的機制，開發者將不必煩惱如何操作 DOM，而可以專心於撰寫 UI 的定義與互動邏輯。並且由於 React 能夠自動去最佳化的處理 DOM 操作，前端 UI 程式將可以有效的降低操作成本而達到優秀的效能。

### Component
為了讓 UI 能夠有更好的可組合性與可重用性，React 利用虛擬 DOM 的機制將 UI 在程式中都視為一個一個的組件（Component），每個 Component 中定義了這個 UI 元件所要呈獻的樣貌和事件，然後透過層層嵌套與交互使用來組合出你所需要的整個 View。這意味著透過 React，前端 UI 的開發將不再像過往直接撰寫 HTML 那樣雜亂無章，而是能夠更貼近於物件導向式的開發與管理，有系統的進行抽象化、封裝，甚至是繼承。

### JSX
為了使開發者能夠在定義 UI 語法時更順手，Fackbook 為了 React 提供了一種看起來很像是 XML 的 JavaScript 語法擴充 ─ JSX。它對於開發 React 來說並不是強制需要的，您也可以直接使用原生的 JavaScript 語法來定義 UI。不過，XML 格式有固定的標籤開啟和閉合的優點，這能讓複雜的樹狀結構更易於閱讀，並且有利於函數調用與參數填寫，就像類似於傳統的 HTML 標籤語法那樣。

JSX 並不是一個新的語言，他更像是一種幫助開發體驗的語法糖衣。經由像是 [Babel](https://babeljs.io/) 這樣的轉碼器，JSX 會被編譯成原生 JavaScript 程式碼，才能夠在瀏覽器上順利運作。

例如上例中這段的 JSX 程式碼：
```js
<button id="btn" onClick={this.handleClick}>我是一個按鈕</button>
```

經過轉換之後將會變成以下的原生 JavaScript 程式碼：
```js
React.createElement("button", {id: "btn", onClick: this.handleClick}, "我是一個按鈕")
```

## 單向資料流 & 一律重繪
React 的概念中認為，UI 要照什麼樣子繪製出來，應當是取決於當前的 Model 資料以及 UI 狀態而定。因此，React 對於 View 與 Model 之間採用了的是單向資料流，也是說所有 UI 的呈現都要依照 Model 目前的內容而繪製出來，當 Model 改變時，UI 應當跟著改變。

**這裡指的「一律重新繪製」並不是指重繪整個畫面真正的 DOM，而是一旦 Model 資料發生改變，React 會在程式記憶體中根據最新的 Model 資料重新建立一份全新的 VDOM**，並進行運算與比較來得知何處是真正需要被更改的 DOM，進而做出最小的 DOM 變動來達成 UI 正確且高效能的更新，如此一來將能夠確保 UI 更新的正確性與單純性。

然而，當 View 當中的 UI 操作會觸發 Model 資料的變更時，為了確保所有使用到這份資料的 UI 都能夠同步一致的獲得更新，我們應該將 Model 資料擺放在一個獨立於 UI Component 之外的地方，讓不同的 UI 之間能夠共同存取。在資料被操作修改之後，由於一律重繪的機制，React 將會自動根據最新的 Model 自動重繪所有 UI 的 VDOM ，並且在運算後更新到對應的 DOM。因此，這樣單向資料的流程以及一律重繪的機制將能夠確保 UI 繪製與更新的正確性與單純性 ── 只要 Model 的資料正確，UI 就會自動被更新到正確。
