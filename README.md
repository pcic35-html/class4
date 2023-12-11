# HTML basic IV
幫我想想我可以在這邊寫甚麼
# 擲骰子 II
ET01喜歡打日麻，每次開牌時都需要骰兩顆骰子來決定：要從誰前面的排山開始抓牌、從第幾墩抓牌  
問題來了，我們的擲骰子web只有一顆骰子，顯然我們需要寫一個可以擲兩顆骰子的web  

在這之前，我們先整理一下我們的程式碼  
我們之前將"區間亂數產生器"和"顯示骰子點數"的程式碼寫在一起，所以會很亂，現在，我們把它包成一個函數  
```js
function randomint(l,r){
	let loop=r-l+1;
	let a=Math.random();
	a*=loop;
	a+=l;
	a=Math.floor(a);
	return a;
}
function dice(){//擲骰子
	let a=randomint(1,6);
	console.log(a);//當然，可以是其他顯示點數的方式
}
```
相對的，我們的 `HTML` code 也要做相對應的修改  
```html
<button onclick="dice();">擲骰子</button>
```
那如果我想骰兩顆骰子怎麼辦？***呼叫兩次`randomint()`函式***  
```js
function dice(){
	let a=randomint(1,6);
	let b=randomint(1,6);
	console.log(a);
	console.log(b);
}
```
![Alt text](image/image-1.png)  
他成功骰了兩顆骰子，接著搭配我們的 `HTML` code...  
等一下，我們的 `HTML` code 只有安排一個空間（一個`id`）來顯示，但我們有兩顆骰子  
我們要把兩個數字以字串的方式合併，變成一串字串，再把他放進`innerHTML`裡面  
終於來到今天的重點了  
# string 字串
如何宣告
```js
let a="字串";
let b='也可以用單引號';
```
# 字串的合併
把他們加起來就好了
```js
let a="a";
let b=a+a;//  b="aa"
b+="test";//  b=b+"test"	b="aatest"
```
# `String()` 數字轉字串
可以使用 `String(n)` 將數字轉成字串  
注意，這邊的 `S` 要大寫
```js
String(123);//  "123"
```

聰明的你應該知道要如何把兩顆骰子併在一起了把？
```js
function dice(){
	let a=randomint(1,6);
	let b=randomint(1,6);
	console.log(String(a)+String(b));
}
```
![Alt text](image/image-2.png)  
21點，好歐  
我們應該要在兩個數字之間加個空格才對，隊把
```js
console.log(String(a)+" "+String(b));
```
同樣的概念，我們也可以用在圖片上面  
上次課程的最後，講師使用圖片來取代文字來顯示骰子點數，但當初，我暴力的使用大量的`if`來寫  
現在，我們可以改變一下寫法  
首先，先把圖片檔明改簡單一點，改成`1.png`、`2.png`...`6.png`  
（講師使用的是.svg檔，但你們不要也把副檔名也改掉，圖片會壞掉，原本是.jpg就改成`1.jpg`...）  
![Alt text](image/image-3.png)  
接著撰寫顯示圖片的`HTML`程式碼  
```html
<img src="6.svg" class="dice_image">
```
把它拆解成[`字串`+`數字`+`字串`]的形式  
```js
'<img src="'+String(a)+'.svg" class="dice_image">'
```
程式碼可以改寫成
```js
function dice(){
	let a=randomint(1,6);
	let b=randomint(1,6);
	let imgtxt='<img src="'+String(a)+'.svg" class="dice_image">';
	imgtxt+='<img src="'+String(b)+'.svg" class="dice_image">';
	document.getElementById("dice").innerHTML=imgtxt;
}
```
[sample](./dice1/)  
[source](https://github.com/pcic35-html/class4/blob/main/dice1/index.html)  

# 擲骰子 III
問題又來了，我們做了可以一次骰兩顆骰子的擲骰子web，但ET01還是不滿意，他想要一次骰100顆骰子  
為甚麼呢？因為[超超超超超喜歡你的100個女朋友（君のことが大大大大大好きな100人の彼女）](https://youtube.com/playlist?list=PL12UaAf_xzfrz7SGyU-5-7E0gmcQ0mNiF)  
（這周日 `22:00` 更第十一集，誰要陪我看）  
很明顯，我們需要"迴圈"  
這邊很複雜，認真聽了歐  
```js
for(初始值;條件;更新){
	//程式碼
}
```
- `初始值`：迴圈開始前，要先做的事  
通常我們會寫`let i=0`，也就是從 `0` 開始 ~~的異世界生活~~  
- `條件`：每次迴圈開始前，都會先判斷這個條件，如果條件成立，就會執行`程式碼`，否則就會跳出迴圈  
通常我們會寫 `i<100`，也就是 `i` 會從 `0` 數到 `99` ，數到 `100` 就會跳出迴圈（因為 `100<100` 不成立）  
- `更新`：每次執行完`程式碼`後，都會執行這個更新，通常是將`初始值`更新，讓`條件`可以成立  
通常我們會寫 `i++` ，也就是說每跑完一次迴圈， `i` 就會加 `1` ，也就是 `i=0`、`i=1`、`i=2`...  
相對的，如果我們寫成 `i+=2` ，就會變成每次都會 `+2` ，變成 `i=0`、`i=2`、`i=4`...  

統整之後如下  
```js  
for(let i=0;i<100;i++){
	//程式碼
	//這邊的程式碼會被執行100次
	//可以使用i來判斷目前是第幾次迴圈
}
```
撰寫建議：可以先試著產生5顆骰子，確認沒問題後再把數字調到100  
```js
function dice(){
	document.getElementById("dice").innerHTML="";//先把上次的結果清空
	//for(let i=0;i<5;i++){  //如果還不熟悉for迴圈，可以先試著用這一行產生5顆骰子
	for(let i=0;i<100;i++){  //產生100顆骰子var，熟悉過後再把數字調大
		let a=randomint(1,6);
		let imgtxt='<img src="'+String(a)+'.svg" class="dice_image">';
		document.getElementById("dice").innerHTML+=imgtxt;//將新的骰子加入
	}
}
```
![Alt text](image/image-4.png)  
破圖辣，大哥  
記得要修改 `HTML` 的顯示樣式  
講師的作法是將圖片size改成整個版面的`10%`，也就是`width:10%;height:10%;`  
```css
.dice_image{
	width:10%;
	height:10%;
}
```
這樣子剛好可以讓100顆骰子在一個版面內  
![Alt text](image/image-5.png)  
[sample](./dice100/)  
[source](https://github.com/pcic35-html/class4/blob/main/dice100/index.html)  

# 擲骰子 IV
沒錯，我們又又双双要寫擲骰子  
我們要一次擲出n顆骰子，n=使用者自行輸入  

# `HTML` `<input>` 輸入框
```html
<!--允許輸入文字，預設值為"輸入框預設值"-->
<input 
	type="text" 
	id="input" 
	value="輸入框預設值"
	onkeydown="按下按鍵時執行的函式"
>
<!--只允許輸入數字，預設值為3-->
<input type="number" id="dice_count" value="3" onkeydown="dice()">
<script>
	document.getElementById("dice_count").value;//取得輸入框的值
	//注意，後面是value，不要打成innerHTML
</script>
```
得到了使用者輸入的值後，我們就可以用`for`迴圈來產生骰子了  
```js
function dice(){
	let n=document.getElementById("dice_count").value;//取得輸入框的值
	document.getElementById("dice").innerHTML="";//先把上次的結果清空
	let str="";
	for(let i=0;i<n;i++){  //產生n顆骰子
		let a=randomint(1,6);
		let imgtxt='<img src="'+String(a)+'.svg" class="dice_image">';
		str+=imgtxt;//將新的骰子加入
	}
	document.getElementById("dice").innerHTML=str;//更新結果
}
```
[sample](./dice_pro/)  
[source](https://github.com/pcic35-html/class4/blob/main/dice_pro/index.html)  

恭喜你，完成第一個網頁小遊戲：擲骰子  

# 嵌入內容
找尋一隻YT影片，點擊分享，應該會出現一個`嵌入`的選項  
![Alt text](image/image-6.png)  
他會給你一串`HTML`程式碼  
![Alt text](image/image-7.png)  
你可以把它貼在網頁上面  
例如，我把它貼在擲骰子網頁的下方  
```html
<body>
	<!--這上面是你擲骰子的程式碼-->
	<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/dQw4w9WgXcQ?si=2JSCSrcjqxABg-wn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</body>
```
![Alt text](image/image-8.png)  
你的網頁也會跟著出現辣個YT影片  
如果要在網頁上分享YT影片，這個功能會很方便  

# `JS` 自動跳轉
各位，注意聽好，這部分特別重要  
它的重要性有多高，看我朋友寫的網頁就知道了  
<https://bennydioxide.github.io>  
放心，他是`github`的靜態網頁({name}.github.io)，而不是(youtube.com)  
[source](https://github.com/BennyDioxide/bennydioxide.github.io/blob/RickRoll/index.html)  
`window.location.href`會回傳目前的網址，也就是上面辣個`https://pcicclass--kagariet01.repl.co/dice/`  
那如果把他設定成其他網址呢，他會把你帶到其他網址  
例如  
```js
window.location.href="https://www.youtube.com/watch?v=dQw4w9WgXcQ";
```
我想這功能要怎麼用，應該不用我教吧  
你可以寫一個