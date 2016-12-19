# ECMAScript 6 
ECMAScript 5 （簡稱 ES5）寫過大量前端應用的都知道多人開發且沒有一定的規範往往造成程式碼閱讀及維護性不佳的問題，ESMAScript 6（簡稱 ES6）針對這些痛點一一解決，就讓我們一個個看下去，會開始接觸 ES6 也是因為 Vue.js 的範例都已採用 ES6 ，這邊順便推薦一下 Vue.js 這套框架，這邊就不多贅述。

## Template Literals
ES 5 本身對字串本身沒有內建 Template ，所以要達到這功能往往要透過第三方元件，或自己刻一個，相信網路上有一堆範例，某種程度也會造成程式碼不易維護的狀況，ES 6 的出現解決了這問題，來看看下列範例。
```
var player = { name : 'Bill'};
var message = `hello ${player.name}`;
console.log(message);
```
字串前後採用 `（鍵盤數字1的左邊），再將需要的變數放入 ${} 內，除了顯示之外還可以在${} 內進行運算式的操作如下

```
var numa = 1
var numb = 2
var message = `a + b = ${ a + b}`
console.log(message);
```
會先說明 Template Literals 是因為後面的例子都會直接採用，讓各位能加強記憶。

## Constants 常數
程式開發往往需要定義一些常數且任何情況下都不被改變，在 ES5 能達到這目地但需要寫上一段 Object.defineProperty 的語法宣告。
```
var myConst = {};
Object.defineProperty(myConst, "PI", {
    value:        3.141593,
    enumerable:   true,
    writable:     false,
    configurable: false
});
console.log(myConst.PI);
myConst.PI = 99;
console.log(myConst.PI);
```
我們會看到 `3.141593` 印出兩次的結果，而且這樣的程式在 ES5 裡面合法，也就是不會有任合錯誤訊息發生。

看看 ES6 的做法
```
const PI = 3.141593
console.log(PI)
PI = 99
console.log(PI)
```
這邊宣告了一個PI的常數，動作是列印修改常數在列印，由下列結果發現在 `PI=99`的定義會發生錯誤，且錯誤訊息非常直白告訴我們不能賦予 constant 值並中斷程式碼，這告訴我們做錯事情因該要被處罰。
```
3.141593
VM231:3 Uncaught TypeError: Assignment to constant variable
```

## Scope 範圍
看一下現實程式碼裡可能發生的悲劇。
```
// A工程師
var i= 1;
// ... 經過了幾百行程式碼後
// B工程師
function go(){
  for(var i=0 ; i < 3 ; i++){
  }
}
console.log('i',i);
go();
console.log('i',i);
```
B工程師將 i 重新定義成`3`了，而且也不會被提示意思就是B工程師根本不知道自己造就了這場悲劇，而要在 ES 5 避免這場悲劇也可以這麼寫。
```
var i=1;
(function(){
  for(var i=0 ; i < 3 ; i++){}
  console.log('i',i);
})();
console.log('i',i);
```
馬上來看 ES 6 怎麼解決這問題。
```
let i =1
{
for(let i=0 ; i< 3 ; i++){}
}
console.log(i);
```
這確保了變數再定義後在該範圍內的唯一性，試著在同範圍定義重複定義如 `let i=0 ; let i=0;` 會直接產生語法錯誤。

## Arrow Functions 
```
function showMembers(){
  var self = this;
  this.preWorld = 'Hello ';
  ['Bill' , 'Kris' , 'Tommy'].forEach(function(v){
    console.log(self.preWorld + v);
   });
}
showMembers();
```
看到 var self = this 因該滿熟悉的，這是為了解決匿名方法為了取得外層區塊 this 的做法，原本定義方法語法 [function] [argraments]，可以想像把他們顛倒過來在吧[function]改成 => 變成 [argraments] [=>]如下，而且匿名方法還可以直接透過 this 取得外層區塊的 this，ES 6 的這改變對我最有感。
```
var showMembers = () => {
  this.preWorld = 'Hello ';
  ['Bill' , 'Kris' , 'Tommy'].forEach((v) => {
    console.log(this.preWorld + v);
   });
}
showMembers();
```

## Extended Literals

## Enhanced Regular Expression

## Enhanced Object Properties

## Destructuring Assignment

## Modules

## Classes

## Symbol Type

## Iterators

## Generators

## Map/Set & WeakMap/WeakSet

## Typed Arrays

## New Built-In Methods

## Promises

## Meta-Programming

## Internationalization & Localization
