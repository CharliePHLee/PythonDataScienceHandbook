---


---

<h1 id="如何使用numpy操作資料">如何使用NumPy操作資料</h1>
<p>在開始學習NumPy前,先說明如何啟動Python. 安裝好Anaconda後, 開啟畫面會如下<br>
<strong>Anaconda畫面</strong><br>
<img src="https://lh3.googleusercontent.com/H_9fFrFG9JwbkODtfWRq1Ez1ypMVIGtVK62_Il08ah8wo8UW-BIw0k-SxY1GucJxpxvlMv-wKE-P" alt="enter image description here"></p>
<p>點擊Spyder啟動Python編輯畫面.<br>
<strong>Spyder畫面: 左邊是寫程式碼的地方,右側是執行程式碼結果</strong><br>
<img src="https://lh3.googleusercontent.com/_JGW9WU45Rb4d5YBQCI7usifejuM_5pYXqhLuO1LPLUUfTmaPKE2ooy0WaXTYuJPIlzdjp87fPIw" alt="enter image description here"></p>
<p>PS:我的視窗位置有經過調整,可能跟你的有差異.但聰明如你,可以自己處理</p>
<p>導入NumPy函數庫: 輸入<code>import numpy as np</code></p>
<h6 id="ps-as是將函數庫名子用np代表.這樣你寫程式時就不需要一直寫numpy">PS: as是將函數庫名子用np代表.這樣你寫程式時,就不需要一直寫numpy</h6>
<p>好,準備工作都好了.那我們開始學習numpy操作數據了.<br>
我們先自己建立數據, 大部分時候我們做資料分析, 都是從外部讀入的.<br>
這個後續會教到如何讀取外部資料.</p>
<h2 id="建立數據">建立數據</h2>
<p>這裡我們建立3種數據.分別有1維、2維跟3維的.</p>
<p><strong>導入NumPy函數庫</strong><br>
<code>import numpy as np</code></p>
<p>設定亂數種子<code>np.random.seed(1)</code><br>
這樣你我的程式結果才會一致. 幫助在操作過程中理解</p>
<p>產生1維資料<br>
<code>a1=np.random.randint(3,size=3)</code><br>
size=3指的是產生3個數據. 當你想要100個數據時,就是<code>size=100</code></p>
<p>產生2維資料<br>
<code>a2=np.random.randint(6,size=(2,3))</code><br>
size=(2,3)指的是產生2列3行, 共有6個數據. 當你想要3列4行時,就是<code>size=(3,4)</code></p>
<p>產生3維資料<br>
<code>a3=np.random.randint(12,size=(2,2,3))</code><br>
size=(2,2,3)指的是產生2個2列3行, 共有12個數據. 當你想要3個2列3行,就是<code>size=(3,2,3)</code></p>
<h3 id="補充">補充</h3>
<ol>
<li>常態分佈亂數. 產生1個平均數0標準差1的常態分佈亂數<code>np.random.normal(1,0,1)</code></li>
<li>0-1間的亂數. 產生1個0-1間的均勻分佈亂數<code>np.random.rand()</code></li>
</ol>
<h2 id="取值">取值</h2>
<p>當數值產生後, 首先先介紹取值的方式.</p>
<ul>
<li>1維資料取值<br>
取數列中第一個值, 可以使用<code>a1[0]</code>.<strong>注意: Python是從0開始為第一個位置</strong><br>
以此類推, 取第二個值則為<code>a1[1]</code>.</li>
</ul>
<pre><code>a1
Out[5]: array([1, 0, 0])

a1[0]
Out[6]: 1

a1[1]
Out[7]: 0

a1[2]
Out[8]: 0```
</code></pre>
<ul>
<li>2維資料取值<br>
和1維取值相同, 需要先從0開始為第一個位置. 所以要取第1列第1行的資料, 則使用a2[0,0]<br>
取第2列第2行的資料, 則使用a2[1,1]</li>
</ul>
<pre><code>a2
Out[14]: 
array([[1, 3, 5],
       [0, 0, 1]])

a2[0,0]
Out[15]: 1

a2[1,2]
Out[16]: 1
</code></pre>
<ul>
<li>3維資料取值<br>
和1維取值相同, 需要先從0開始為第一個位置. 所以要取第1個第1列第1行的資料, 則使用a3[0,0,0]<br>
取第2個第1列第2行的資料, 則使用a3[1,0,1]</li>
</ul>
<pre><code>a3
Out[18]: 
array([[[ 7,  6,  9],
        [ 2,  4,  5]],

       [[ 2,  4, 11],
        [10,  2,  4]]])

a3[0,0,0]
Out[19]: 7

a3[1,0,1]
Out[20]: 4
</code></pre>
<p>如果我們不是要1個值1個值取出,而是要取出多個數值. 需要使用<code>:</code>符號<br>
x[開始位置<code>:</code>結束位置<code>:</code>間距]</p>
<p>以下用例子說明, 幫助理解<br>
我們先建立一個由0到9的數值列</p>
<pre><code>x=np.arange(10)
x
Out[27]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
取第1個到第5個數值,間距1
x[0:5:1]
Out[31]: array([0, 1, 2, 3, 4])
或簡單寫法
x[:5]
Out[32]: array([0, 1, 2, 3, 4])

取第間距2的數值
x[0:10:2]
Out[33]: array([0, 2, 4, 6, 8])```
或簡單寫法
x[::2]
Out[34]: array([0, 2, 4, 6, 8])`

取第2個數以後並且間距2的數值
x[2::2]
Out[35]: array([2, 4, 6, 8])
</code></pre>
<p>從2維資料中, 同樣可以利用<code>:</code>符號. 只要使用<code>,</code>隔開<br>
x[開始位置<code>:</code>結束位置<code>:</code>間距, 開始位置<code>:</code>結束位置<code>:</code>間距]</p>
<p>同樣用一個例子說明, 幫助理解<br>
我們先建立一個由0到8, 3X3的數據</p>
<pre><code>x=np.arange(9).reshape((3,3))
x
Out[60]: 
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])
取第1到第2列,第1到第2行的數值,間距1
x[0:2:1,0:2:1]
Out[62]: 
array([[0, 1],
       [3, 4]])
或簡單寫法
x[:2,:2]
Out[64]: 
array([[0, 1],
       [3, 4]])
取間距2的數值
x[0:3:2,0:3:2]
Out[66]: 
array([[0, 2],
       [6, 8]])
或簡單寫法
x[::2,::2]
</code></pre>
<p>3維資料中, 同樣可以利用<code>:</code>符號. 只要使用<code>,</code>隔開<br>
x[開始位置<code>:</code>結束位置<code>:</code>間距, 開始位置<code>:</code>結束位置<code>:</code>間距,開始位置<code>:</code>結束位置<code>:</code>間距]<br>
3維資料大家可以自己試試產生3維資料<code>x=np.arange(8).reshape((2,2,2))</code><br>
對資料進行操作, 就不增加文章篇幅了.</p>
<h3 id="邏輯取值">邏輯取值</h3>
<p>邏輯取值也是很重要的技巧之一, 做資料分析一定會用到.<br>
先介紹Python中的邏輯處理符號, 邏輯取值就是利用邏輯處理符號來進行取值.<br>
如下即是Python中的邏輯處理符號<br>
1. 且<code>&amp;</code><br>
2. 或<code>|</code><br>
3. 互斥<code>^</code><br>
4. 否<code>~</code><br>
5. 大於<code>&gt;</code><br>
6. 小於<code>&lt;</code><br>
7. 大於等於<code>&gt;=</code><br>
8. 小於等於<code>&lt;=</code><br>
9. 等於<code>==</code></p>
<p>**先產生一組美金薪資數據好了(薪資比較引起興趣^^) **<br>
<code>salary=np.array([2300,3200,1700,1453,730,951,856,2671])</code><br>
如果你想取薪資大於1000美金的數值, 很簡單.</p>
<pre><code>salary[salary&gt;1000]
Out[73]: array([2300, 3200, 1700, 1453, 2671])
</code></pre>
<p>如果你想取薪資小於1000美金的數值</p>
<pre><code>salary[salary&lt;1000]
Out[74]: array([730, 951, 856])```
</code></pre>
<p>如果你想取薪資大於1000美金且小於2000的數值</p>
<pre><code>salary[(salary&gt;1000) &amp; (salary&lt;2000)]
Out[89]: array([1700, 1453])
</code></pre>
<h2 id="合併與分割數據">合併與分割數據</h2>
<p>在Python中,主要有3種方式來合併數值<br>
1. <code>np.concatencate</code><br>
2.  <code>np.vstack</code><br>
3. <code>np.hstack</code><br>
<code>np.vstack</code>和<code>np.hstack</code>都可以用<code>np.concatencate</code>來取代, 就不做介紹.<br>
以下用例子說明<br>
<strong>np.concatencate: 將資料由最後串接起來</strong></p>
<pre><code>1維資料
a=np.array([2,4,6])
b=np.array([3,6,9])

np.concatenate([a,b])
Out[90]: array([2, 4, 6, 3, 6, 9])

np.concatenate([b,a])
Out[91]: array([3, 6, 9, 2, 4, 6])
</code></pre>
<p>2維資料也可以串接, 但需指定列串接或行串接,只要使用axis參數來指定<br>
請看例子</p>
<pre><code>a=np.arange(4).reshape((2,2))
b=np.arange(4,8).reshape((2,2))

a
Out[98]: 
array([[0, 1],
       [2, 3]])
b
Out[99]: 
array([[4, 5],
       [6, 7]])

np.concatenate([a,b],axis=0)
Out[102]: 
array([[0, 1],
       [2, 3],
       [4, 5],
       [6, 7]])

np.concatenate([a,b],axis=1)
Out[103]: 
array([[0, 1, 4, 5],
       [2, 3, 6, 7]])
</code></pre>
<p>介紹過合併後, 分割數據也是常使用的數據方析工具<br>
在Python中,主要有3種方式來分割數值<br>
1. <code>np.split</code><br>
2. <code>np.vsplit</code><br>
3. <code>np.hsplit</code><br>
<code>np.vsplit</code>和<code>np.hsplit</code>都可以用<code>np.split</code>來取代, 就不做介紹.<br>
以下用例子說明</p>
<pre><code>x
Out[113]: [1, 2, 3, 99, 99, 3, 2, 1]
使用np.split需要給分割位置,我們將資料的第3個跟第5個位置當分割點.
x1, x2, x3 = np.split(x, [3, 5]) 
x1
Out[114]: array([1, 2, 3])
x2
Out[115]: array([99, 99])
x3
Out[116]: array([3, 2, 1])
</code></pre>
<p>2維資料也可以分割, 但需指定列串接或行串接,只要使用axis參數來指定<br>
請看例子</p>
<pre><code>a=np.arange(4).reshape((2,2))
a
Out[117]: 
array([[0, 1],
       [2, 3]])

np.split(a,[1],axis=0)
Out[118]: [array([[0, 1]]), array([[2, 3]])]

np.split(a,[1],axis=1)
Out[119]: 
[array([[0],
        [2]]), array([[1],
        [3]])]
</code></pre>
<h2 id="計算">計算</h2>
<ul>
<li><strong>數據的個數與維度相同時</strong><br>
在相對應的位置做四則計算.</li>
</ul>
<ol>
<li><strong>1维</strong></li>
</ol>
<pre><code>x=np.array([1,3,5])
y=np.array([2,4,6])
相加
x+y
Out[35]: array([ 3,  7, 11])
相減
x-y
Out[36]: array([-1, -1, -1])
相乘
x*y
Out[37]: array([ 2, 12, 30])
相除
x/y
Out[38]: array([0.5       , 0.75      , 0.83333333])
</code></pre>
<ol start="2">
<li><strong>2维</strong></li>
</ol>
<pre><code>a=np.array([[1,2],[3,4]])
b=np.array([[2,4],[6,8]])
相加
a+b
Out[46]: 
array([[ 3,  6],
       [ 9, 12]])
相減
a-b
Out[47]: 
array([[-1, -2],
       [-3, -4]])
相乘
a*b
Out[48]: 
array([[ 2,  8],
       [18, 32]])
相除
a/b
Out[49]: 
array([[0.5, 0.5],
       [0.5, 0.5]])
</code></pre>
<ul>
<li><strong>數據的個數與維度不相同時</strong><br>
當個數與維度不相同時, Python是用以下規則順序處理的.<br>
1. 維度較小的資料, 維度尺寸往左增加1個維度<br>
2. 維度值為1的維度, 調整為另一資料集的維度<br>
3. 維度值不為1,且兩資料集維度不相符的, 無法進行運算	<br>
<strong>以下以2個例子舉例</strong><br>
-eg1:</li>
</ul>
<pre><code>	a=np.array([[1,2],[3,4]])
	s=np.array([2])
	a
	Out[87]: 
	array([[1, 2],
	       [3, 4]])	
	s
	Out[88]: array([2])
	
	a+s
	Out[89]: 
	array([[3, 4],
	       [5, 6]])
</code></pre>
<pre><code>說明a為2x2資料,s為0x1. 依照規則1, Python將s轉為1x1資料後. 再依規則2將s轉為2x2後再相加

	- eg2:
</code></pre>
<pre><code>	a=np.array([[1,2],[3,4]])
	s=np.array([4,6])
	a
	Out[55]: 
	array([[1, 2],
	       [3, 4]])	
	s
	Out[56]: array([4, 6])
	
	a+s
	Out[57]: 
	array([[ 5,  8],
	       [ 7, 10]])
</code></pre>
<pre><code>說明a為2x2資料,s為1x2. 依照規則2, Python將s轉為2x2資料後,再相加
</code></pre>
<ul>
<li><strong>統計量</strong><br>
在計算統計量時, NumPy有以下個常用函數
<ol>
<li>總和<code>np.sum()</code></li>
<li>連乘<code>np.prod()</code></li>
<li>平均數 <code>np.mean()</code></li>
<li>中位數 <code>np.median()</code></li>
<li>標準差 <code>np.std()</code></li>
<li>變異數 <code>np.var()</code></li>
<li>最小值<code>np.min()</code></li>
<li>最大值<code>np.max()</code></li>
<li>百分位數 <code>np.percentile()</code></li>
</ol>
</li>
</ul>
<h3 id="維資料">1維資料</h3>
<p><strong>例子</strong></p>
<pre><code>a1
Out[5]: array([1, 0, 0])

np.sum(a1)
Out[7]: 1

np.max(a1)
Out[8]: 1

np.min(a1)
Out[9]: 0
</code></pre>
<h3 id="維資料-只需要在函數中.-使用axis1標明列計算或axis0行計算">2維資料: 只需要在函數中. 使用axis=1標明列計算或axis=0行計算</h3>
<p><strong>例子</strong></p>
<pre><code>a2
Out[11]: 
array([[1, 3, 5],
       [0, 0, 1]])

np.sum(a2,axis=0)
Out[12]: array([1, 3, 6])

np.sum(a2,axis=1)
Out[13]: array([9, 1])
</code></pre>
<h3 id="使用邏輯判斷取值計算">使用邏輯判斷取值計算</h3>
<h2 id="資料排序">資料排序</h2>
<p>有些時候,我們需要對資料進行排序. 可以使用np.sort函數. 要知道排序後的資料位置則可以使用np.argsort函數</p>
<p><strong>例子</strong></p>
<pre><code>x=np.array([3,1,5,4,9])
資料排序位置
np.argsort(x)
Out[4]: array([1, 0, 3, 2, 4], dtype=int32)
資料排序後
np.sort(x)
Out[3]: array([1, 3, 4, 5, 9])
</code></pre>
<p>當資料是多維時, 我們也可以延著行或列去排序</p>
<pre><code>x=np.arrange([[3,1,2],[8,7,6]])
延著行排序
np.sort(x,axis=0)
Out[7]: 
array([[3, 1, 2],
       [8, 7, 6]])

延著列排序
np.sort(x,axis=1)
Out[8]: 
array([[1, 2, 3],
       [6, 7, 8]])
</code></pre>
<h3 id="補充-1">補充</h3>
<ol>
<li>基本的計算功能, Pyhon其實是有內建函數的. 但是使用NumPy可以提升計算的效率.</li>
</ol>

