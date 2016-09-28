![00-01](https://github.com/lilithchen/lilithchen/blob/master/html/img/index.png)

上面這張圖片是我的臨摹作業截圖，版面大致已經完成了。  
但是最後發現彈出表單的效果還是跟原本預期的不同，所以也有可能會再調整...>"<  
不過這邊想寫的是關於架構的部分，所以其他就暫時不考慮了(被毆)  
    
製作一個網頁之前，先規劃整個頁面的架構，  
可以在腦中有一個藍圖（或是畫下來讓自己隨時參考），比較不會越寫越亂。  
先附上自己當初畫下來的架構圖XD...  
（其實這是草圖畫完後再整理過的，原本是鉛筆畫的亂七八糟草稿）  
  
![00-02](https://github.com/lilithchen/lilithchen/blob/master/html/img/02.jpg)
  
最一開始的草圖沒有這麼複雜，只是簡單的標出大的框架，  
例如 : body、main、h1、contenr、footer  
一邊寫，一邊修改草圖，一邊畫出細節，  
最後才變成這張圖，再標上關鍵的 id 或 class，  
這個動作乍看之下好像有點不知為啥要這樣，  
但其實一邊撰寫過程才發現這張圖對於一個初學超級菜鳥來說其實很有用，  
因為對一切都還不熟悉，很容易寫著寫著就不知道自己在寫什麼了...XD  
尤其是寫到細節處，誰和誰是父層與子層的關係、誰和誰是"兄弟"，  
因為關係著 css 的安排，這時候如果有張圖可以參考，會方便許多呢～  
下面簡單的說明一下是為什麼那麼多層的....  
  
  
##body
![body](https://github.com/lilithchen/lilithchen/blob/master/html/img/body.png)  
大家都知道 html 的主體是要寫在 < body > 標籤裏頭  
但也可以在 body 下面多放一層 div 包住整個網頁的東西，預防看不懂 html5 跟 css3 的舊版瀏覽器  
在這邊我將這層 div 設定為 id="main"，  
main 裏頭再分割出 h1 / div id="content" / div id="footer" 三個大區塊  
如此，主要的大框架就弄出來了！  
h1 -------- 自然是這個頁面最重要的資訊，一般來說h1只要一個就好了，這有助於搜尋優化(SEO)。  
content --- 放的則是主要的內容，因為這個網頁是登入頁面，所以主要內容自然是表單的部分。  
footer ---- 就放置關於版權的資訊。  
  
  
##content
![content](https://github.com/lilithchen/lilithchen/blob/master/html/img/content.PNG)  
在上面的截圖中可以看到整個主內容區還可以分成兩個部分  
所以在 content 中再劃分兩個 div 分別是：  
上面 輸入登入資訊的區域 div class="loginInner"  
下面 連結其他社群網站的區域 div class="socialIcons"  
因為登入資訊是表單，社群網站是超連結，  
分成兩個區塊不僅不易混淆，  
更重要的是可以在撰寫語法時更加便利清楚。  
  
  
##loginInner
![loginInner](https://github.com/lilithchen/lilithchen/blob/master/html/img/loginInner.PNG)  
這區塊裡頭又包含 logHead 和 form 兩區，  
（我把 form 包在了 logTop 裡面，整串被我收起來了...）  
這邊想特別提一下的是 表單 < form >  
form 包含帳密輸入框和 submit 按鈕，因為 "submit 按鈕" 必須在 form 裡面，  
是為了提交帳號密碼的表單資訊，所以將 form 獨立成一個區塊是必須的。  
w3菜鳥教程裏頭也有詳細的介紹 [HTML < form > 標籤](http://www.runoob.com/tags/tag-form.html)  
  
  
##socialIcons
![socialIcons](https://github.com/lilithchen/lilithchen/blob/master/html/img/socialIcons.PNG)  
最後社群網站的區域還包刮 facebook / twitter / Google+ 三小塊。  
這邊使用 < ul > 包覆三個 < li >  
另外因為想要整個 < li > 都有作用，又希望各自有 logo 和名稱，  
所以在 < li > 中放入 < a >  
 < a > 再包含兩個 < span > 分別放置 logo 和名稱。  
如此也可以在 logo 的 span 上做一點特效囉～  
  
  
##註解
介紹完基礎的架構之後，很重要的一件事情是註解，  
因為語法什麼的一串又一串，如果不做個記號，到最後不要說別人看不懂你在寫啥，自己也看不懂XD"  
所以說在文件中有條不紊的分區撰寫每個區塊，再運用註解標示清楚，  
這樣不僅清楚明瞭也不容易混淆～  
比方說這樣......  
  
![comment](https://github.com/lilithchen/lilithchen/blob/master/html/img/comment.png)  
是不是看起來一目瞭然呢XD?  
  
  
最後在順帶一提一下，草圖這東西基本上是給自己參考用的，所以也不是就不能再修改的東西，  
就像我寫到了最後，發現還是有點問題，搞不好有些地方要打破原本的框架才可以O.O，  
但這樣寫下來會覺得頭腦比原本更加清楚了許多。  
所謂寫過的就是自己的 大概就是這麼一回事XD....  
沒有親自寫過一遍，只是純粹看書爬網頁，其實不會知道自己哪裡會有問題。  
  
那今天就寫到這裡....  
這實在是非常基礎的東西...總之...獻醜了...  
萬一...有什麼寫得不好的地方...請不用客氣，用力糾正我XD"...  
希望可以趕快學得好一點OAQ
