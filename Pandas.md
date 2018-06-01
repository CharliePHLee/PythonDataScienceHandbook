---


---

<h1 id="如何使用pandas操作資料">如何使用Pandas操作資料</h1>
<p>在開始學習Pandas前,先說明如何啟動Python. 安裝好Anaconda後, 開啟畫面會如下<br>
<strong>Anaconda畫面</strong><br>
<img src="https://lh3.googleusercontent.com/H_9fFrFG9JwbkODtfWRq1Ez1ypMVIGtVK62_Il08ah8wo8UW-BIw0k-SxY1GucJxpxvlMv-wKE-P" alt="enter image description here"></p>
<p>點擊Spyder啟動Python編輯畫面.<br>
<strong>Spyder畫面: 左邊是寫程式碼的地方,右側是執行程式碼結果</strong><br>
<img src="https://lh3.googleusercontent.com/_JGW9WU45Rb4d5YBQCI7usifejuM_5pYXqhLuO1LPLUUfTmaPKE2ooy0WaXTYuJPIlzdjp87fPIw" alt="enter image description here"></p>
<p>PS:我的視窗位置有經過調整,可能跟你的有差異.但聰明如你,可以自己處理</p>
<p>導入Pandas函數庫: 輸入<code>import pandas as pd</code></p>
<h6 id="ps-as是將函數庫名子用pd代表.這樣你寫程式時就不需要一直寫pandas">PS: as是將函數庫名子用pd代表.這樣你寫程式時,就不需要一直寫pandas</h6>
<h1 id="建立pandas資料">建立Pandas資料</h1>
<p>Pandas資料有兩種結構Series與DataFrame</p>
<h3 id="建立series">建立Series</h3>
<p>使用pd.Series建立Series並且可以使用index來自定義行名稱.<br>
如果沒有給行名稱,Python會以0開始的數字開始編號</p>
<pre><code>ds=pd.Series([1,2,3,4])
ds
Out[2]: 
0    1
1    2
2    3
3    4
ds=pd.Series([1,2,3,4],index=['A', 'B', 'C', 'D'])
ds
Out[3]: 
A    1
B    2
C    3
D    4
或使用此方式
ds=pd.Series({'A':1,'B':2,'C':3,'D':4})
ds
Out[29]: 
A    1
B    2
C    3
D    4
</code></pre>
<p><strong>選取資料值</strong><br>
要選取Series中資料值時,可以使用對應的列名稱取值</p>
<pre><code>ds[[0,2]]
Out[6]: 
0    1
2    3
或
ds[['A','C']]
Out[7]: 
A    1
C    3
</code></pre>
<p>你也可以使用slice<code>:</code>來取多個數值</p>
<pre><code>ds['A':'C']
Out[12]: 
A    1
B    2
C    3
</code></pre>
<p><strong>增加新資料值</strong></p>
<pre><code>ds['E']=5
ds
Out[14]: 
A    1
B    2
C    3
D    4
E    5
</code></pre>
<p><strong>邏輯取值</strong><br>
邏輯取值也是很重要的技巧之一, 做資料分析一定會用到.<br>
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
<p>再來利用邏輯判斷來對Series取值.<br>
例如我們想取ds中大於等於3的值</p>
<pre><code>ds[ds&gt;=3]
Out[16]: 
C    3
D    4
E    5
</code></pre>
<p>或是我們想取ds中大於等於2且小於4的值</p>
<pre><code>ds[(ds&gt;=2)&amp;(ds&lt;4)]
Out[17]: 
B    2
C    3
</code></pre>
<p><strong>重要: <font color="blue">精確的取值方法<font></font></font></strong><br>
由於Series是使用列名稱來取值,在使用slice方式取值時.會有以下特殊狀況.<br>
舉例:<br>
當我們的列標籤是數字而且不是連續時.</p>
<pre><code>ds=pd.Series(['dog','cat','monkey'],index=[1,3,5])
ds
Out[19]: 
1       dog
3       cat
5    monkey
</code></pre>
<p>如果使用slice方式取值, 想取列名稱為1,3的值. 但是使用slice取出的卻是列名稱為3,5的值<br>
這是因為用列名稱取值方式跟Python系統的取值方式發生了衝突</p>
<pre><code>ds[1:3]
Out[26]: 
3       cat
5    monkey
</code></pre>
<p>這時就要使用<code>loc</code>,<code>iloc</code>或<code>ix</code>方式來對列名稱精確取值.</p>
<pre><code>ds.loc[1:3]
Out[27]: 
1    dog
3    cat
</code></pre>
<p>這時取出的就是列名稱對應1,3的值了</p>
<h3 id="建立dataframe">建立DataFrame</h3>
<p>建立DataFrame有2種方式</p>
<ol>
<li>從pd.Series資料轉成DataFrame</li>
</ol>
<pre><code>#建立Series資料
salary=pd.Series([100,200,300,400])
salary
Out[35]: 
0    100
1    200
2    300
3    400

建立DataFrame時,可以藉由column對行標籤命名.
df_salary=pd.DataFrame(salary,columns=['SALARY'])
df_salary
Out[39]: 
   SALARY
0     100
1     200
2     300
3     400
</code></pre>
<ol start="2">
<li>由Numpy資料轉成DataFrame</li>
</ol>
<pre><code>pd.DataFrame(np.random.rand(3, 2), 
            columns=['foo', 'bar'], 
            index=['a', 'b', 'c']) 
Out[69]: 
        foo       bar
a  0.705701  0.863022
b  0.417669  0.431585
c  0.311138  0.555763```
</code></pre>
<p><strong>選取資料值</strong><br>
從DataFrame中取值也很簡單,使用行名稱加上<code>loc</code>精確取值方式</p>
<pre><code>df_salary['SALARY'].loc[2]
Out[47]: 300
df_salary['SALARY'].loc[0]
Out[48]: 100
</code></pre>
<p><strong>邏輯取值</strong><br>
如果你想要取薪水大於200的數值</p>
<pre><code>df_salary[df_salary['SALARY']&gt;200]
Out[57]: 
   SALARY
2     300
3     400
</code></pre>
<p>如果你想要取薪水大於等於100但小於300的數值</p>
<pre><code>df_salary[(df_salary['SALARY']&gt;=100)&amp;(df_salary['SALARY']&lt;300)]
Out[58]: 
   SALARY
0     100
1     200
</code></pre>
<p><strong>增加資料</strong><br>
增加資料到DataFrame中,使用以下方式.譬如加入獎金資料</p>
<pre><code>df_salary['BONUS']=[20,30,40,20]
df_salary
Out[50]: 
   SALARY  BONUS
0     100     20
1     200     30
2     300     40
3     400     20
</code></pre>
<p>如果需要計算資料後,增加到DataFrame中,使用以下方式.譬如加入總收入</p>
<pre><code>df_salary['Total']=df_salary['SALARY']+df_salary['BONUS']
df_salary
Out[62]: 
   SALARY  BONUS  Total
0     100     20    120
1     200     30    230
2     300     40    340
3     400     20    420
</code></pre>
<h1 id="計算">計算</h1>
<p>Pandas計算上, 跟NumPy相同. 可以直接使用常見的四則運算符號. 或對應的運算函數.<br>
使用運算函數時, 可以增加一下額外的設定; 例如: 變換NaN值</p>
<ul>
<li>加: +  &lt;=&gt; add()</li>
<li>減: - &lt;=&gt; sub() ,  subtract()</li>
<li>乘: * &lt;=&gt; mul() , multiply()</li>
<li>除: / &lt;=&gt; truediv(), div(), divide()</li>
<li>餘數: % &lt;=&gt; mod()</li>
<li>次方: ** &lt;=&gt; pow()</li>
</ul>
<h3 id="series-計算">Series 計算</h3>
<p><strong>產生兩個Series</strong></p>
<pre><code>a=pd.Series([2,4,6])
b=pd.Series([7,8])
a
Out[11]: 
0    2
1    4
2    6
dtype: int64

b
Out[12]: 
0    7
1    8
</code></pre>
<ul>
<li>常數運算</li>
</ul>
<pre><code>加法
a+1
Out[14]: 
0    3
1    5
2    7
dtype: int64
乘法
a*2
Out[15]: 
0     4
1     8
2    12
dtype: int64
</code></pre>
<ul>
<li>2個Series運算</li>
</ul>
<pre><code>a+b
Out[17]: 
0     9.0
1    12.0
2     NaN
dtype: float64
</code></pre>
<p>當Series的長度不同時, 以最長的為主. 並在缺少的部份以NaN(Not a number)顯示.<br>
NaN也稱為缺少值(missing value)</p>
<h3 id="dataframe計算">DataFrame計算</h3>
<p><strong>產生兩個DataFrame</strong></p>
<pre><code>D1=pd.DataFrame({'N1':[1,2],
                 'N2':[3,4]})

D2=pd.DataFrame({'N1':[1,2,3],
                 'N2':[3,4,5],
                 'N3':[7,8,9]})

D3=pd.DataFrame({'N1':[0,1,2],
                 'N2':[0,3,4]})
D1
Out[71]: 
   N1  N2
0   1   3
1   2   4

D2
Out[72]: 
   N1  N2  N3
0   1   3   7
1   2   4   8
2   3   5   9

D3
Out[73]: 
   N1  N2
0   0   0
1   1   3
2   2   4

相加
D1+D2
Out[75]: 
    N1   N2  N3
0  2.0  6.0 NaN
1  4.0  8.0 NaN
2  NaN  NaN NaN

D1+D2+D3
Out[76]: 
    N1    N2  N3
0  2.0   6.0 NaN
1  5.0  11.0 NaN
2  NaN   NaN NaN

相乘
D1*D2
Out[78]: 
    N1    N2  N3
0  1.0   9.0 NaN
1  4.0  16.0 NaN
2  NaN   NaN NaN
</code></pre>
<h3 id="進階計算處理">進階計算處理</h3>
<p>有時候,我們需要對不同的群體去做分別計算. 例如: 男女, 水果種類, 地區<br>
就需要使用到GroupBy跟Pivot_table兩種方法. 可以想成Excel的Pivot的功能</p>
<p><strong>先介紹幾種常使用的函數</strong></p>
<ul>
<li>describe(): 做敘述統計</li>
<li>count(): 記數</li>
<li>mean() ,  median(): 平均數, 中位數</li>
<li>min() ,  max(): 最大最小值</li>
<li>std() ,  var(): 標準差與變異數</li>
<li>sum(): 總合</li>
</ul>
<p>建立DataFrame, 包含性別,身高,體重,種族</p>
<pre><code>d=pd.DataFrame({'gender':['M','M','F','F','F'],
                 'height':[130,112,108,110,103],
                 'weight':[50,46,41,43,38],
                 'ethnic':['A','B','C','A','B']
                 })
d
Out[85]: 
  ethnic gender  height  weight
0      A      M     130      50
1      B      M     112      46
2      C      F     108      41
3      A      F     110      43
4      B      F     103      38
</code></pre>
<h3 id="groupby">GroupBy</h3>
<p>使用goupby函數去將資料分群,只要在group中填入要分群行名稱<br>
例如: 如果我们想知道不同性别的平均身高,体重</p>
<pre><code>d.groupby('gender').mean()
Out[88]: 
        height     weight
gender                   
F        107.0  40.666667
M        121.0  48.000000
</code></pre>
<p>如果我们想知道不同性别的人数</p>
<pre><code>d.groupby('gender').count()
Out[89]: 
        ethnic  height  weight
gender                        
F            3       3       3
M            2       2       2
</code></pre>
<p>如果我们想知道不同种族的平均身高,体重</p>
<pre><code>d.groupby('ethnic').mean()
Out[90]: 
        height  weight
ethnic                
A        120.0    46.5
B        107.5    42.0
C        108.0    41.0
</code></pre>
<p>也可以使用兩個行名稱去分群, 例如不同种族與性別的平均身高,体重</p>
<pre><code>d.groupby(['gender','ethnic']).mean()
Out[91]: 
               height  weight
gender ethnic                
F      A          110      43
       B          103      38
       C          108      41
M      A          130      50
       B          112      46
</code></pre>
<p>接下來介紹一些額外的功能.<br>
<strong>Aggregate函數</strong><br>
如果我們同時想知道平均身高跟標準差.<br>
就可以使用aggregate函數來幫忙</p>
<pre><code>d.groupby('gender').aggregate(['mean','std'])
Out[99]: 
       height                weight          
         mean        std       mean       std
gender                                       
F         107   3.605551  40.666667  2.516611
M         121  12.727922  48.000000  2.828427
</code></pre>
<p>如果我們同時想知道最大身高跟最小體重.</p>
<pre><code>d.groupby('gender').aggregate({'height':'min','weight':'min'})
Out[102]: 
        height  weight
gender                
F          103      38
M          112      46
</code></pre>
<h3 id="缺少值-missing-value">缺少值 (missing value)</h3>
<p>在Python中有幾種缺少值, 依據Python中對不同缺少值的定義. 使用方式會有不同的結果.</p>
<ol>
<li>None: 資料型別(dtype)被定義為object<br>
如果缺少值資料型別定義為object, 則無法使用sum, min或者排序<br>
舉例:</li>
</ol>
<pre><code>a=np.array([7,None,8])
a
Out[28]: array([7, None, 8], dtype=object)
np.sum(a)
TypeError: unsupported operand type(s) for +: 'int' and 'NoneType'
</code></pre>
<ol start="2">
<li>NaN: 資料型別(dtype)被定義為float-point type<br>
如果缺少值資料型別定義為float-point type, 則可以使用sum, min或者排序.<br>
但是會得到NaN的結果<br>
舉例:</li>
</ol>
<pre><code>a=np.array([7,np.nan,8])
a
Out[57]: array([ 7., nan,  8.])

np.sort(a)
Out[52]: array([ 7.,  8., nan])

a.sum()
Out[53]: nan
</code></pre>
<p>了解了兩種缺少值後, 大部分情況在Pandas中都會將之轉換為NaN形態的缺少值</p>
<h3 id="操作缺少值">操作缺少值</h3>
<p>那以下介紹3種操作缺少值的方式. 在處理資料時也是很重要的一個技能. 這在做EDA(Explore data analysis)前是很常使用的清理資料方法.</p>
<ol>
<li>isnull()、notnull(): isnull()判斷缺少值在資料中哪個位置、notnull()則是判斷非缺少值位置</li>
</ol>
<pre><code>建立Series, 第二個數值為NaN
a=pd.Series([7,np.nan,8])
a
Out[63]: 
0    7.0
1    NaN
2    8.0
dtype: float64

使用isnull
a.isnull()
Out[64]: 
0    False
1     True
2    False
dtype: bool
可以看出第二個數值為缺少值

使用notnull
a.notnull()
Out[66]: 
0     True
1    False
2     True
dtype: bool
可以看出第一跟第三個數值非缺少值

知道非缺失值位置後, 就可以用來操作資料
a[a.notnull()]
Out[67]: 
0    7.0
2    8.0
dtype: float64
</code></pre>
<ol start="2">
<li>dropna(): dropna()是用來移除資料缺少值. 有how,thresh跟axis參數可以進行更多的操作方式</li>
</ol>
<pre><code>建立1維Series, 第二個數值為NaN
a=pd.Series([7,np.nan,8])
a
Out[63]: 
0    7.0
1    NaN
2    8.0
dtype: float64

使用dropna,將第二個NaN數值移除
a.dropna(how="any",axis=0) 或 a.dropna()
Out[69]: 
0    7.0
2    8.0
dtype: float64

建立2維DataFrame資料
a=pd.DataFrame([[7,np.nan,8],
                [1,2,3],
                [np.nan,10,np.nan]])
a
Out[74]: 
     0     1    2
0  7.0   NaN  8.0
1  1.0   2.0  3.0
2  NaN  10.0  NaN

直接使用dropna(),可以看到有缺少值的資料都被移除了
b.dropna(how="any",axis=0) 或 a.dropna()
Out[75]: 
     0    1    2
1  1.0  2.0  3.0

如果要延著行去除缺少值,整個資料都刪除了,因為每一行都有缺少值
a.dropna(how="any",axis=1)
Out[76]: 
Empty DataFrame
Columns: []
Index: [0, 1, 2]

但這樣有時候會刪除許多資料, 造成資料集過少或將有用的數據刪除了
則可以將how="any"改為how="all"表示全為缺少值的資料才刪除
增加一筆全為缺少值的資料
a['3']=[np.nan,np.nan,np.nan]
a
Out[84]: 
     0     1    2   3
0  7.0   NaN  8.0 NaN
1  1.0   2.0  3.0 NaN
2  NaN  10.0  NaN NaN

延著列去除,沒有全為NaN的值,故沒有刪除任何列
a.dropna(how="all",axis=0)
Out[85]: 
     0     1    2   3
0  7.0   NaN  8.0 NaN
1  1.0   2.0  3.0 NaN
2  NaN  10.0  NaN NaN

延著行去除,第三列全為NaN的值,故刪除第三列
a.dropna(how="all",axis=1)
Out[86]: 
     0     1    2
0  7.0   NaN  8.0
1  1.0   2.0  3.0
2  NaN  10.0  NaN
</code></pre>
<ol start="3">
<li>fillna(): 替換缺少值. 有時候我們不需要刪除缺少值, 而是將缺少值更換成某些符號</li>
</ol>
<pre><code>b=pd.Series([7,np.nan,8])
b
Out[94]: 
0    7.0
1    NaN
2    8.0
dtype: float64

更換缺少值為-9999
b.fillna(-9999)
Out[96]: 
0       7.0
1   -9999.0
2       8.0
dtype: float64

更換缺少值為符號$, 但注意dtype改變了
b.fillna('$')
Out[97]: 
0    7
1    $
2    8
dtype: object
</code></pre>
<h1 id="資料合併">資料合併</h1>
<p>將兩個資料集合併, 是個很重要的技巧. 使用concat或merge來達成. 可以使整理資料的過程變得精減. Pandas的concat函數有需多參數設定可以利用.</p>
<h3 id="concat函數">Concat函數</h3>
<pre><code># Signature in Pandas v0.18 
pd.concat(objs, axis=0, join='outer', join_axes=None, ignore_index=False, 
          keys=None, levels=None, names=None, verify_integrity=False, 
          copy=True) 
</code></pre>
<ul>
<li>Concat: 可以將Series跟Series, Series跟DataFrame或DataFrame與DataFrame<br>
<strong>Series跟Series</strong></li>
</ul>
<pre><code>產生3個Series
S1=pd.Series([1,2,3])
S2=pd.Series([0,1,2,3,4])
S3=pd.Series([2,3])

使用concat,行合併
pd.concat([S1,S2,S3])
Out[10]: 
0    1
1    2
2    3
0    0
1    1
2    2
3    3
4    4
0    2
1    3
dtype: int64

使用concat,列合併(axis=1).若資料長度不同,缺少的部份會以缺失值NaN補足
pd.concat([S1,S2,S3],axis=1)
Out[11]: 
     0  1    2
0  1.0  0  2.0
1  2.0  1  3.0
2  3.0  2  NaN
3  NaN  3  NaN
4  NaN  4  NaN
</code></pre>
<p><strong>DataFrame與DataFrame</strong></p>
<pre><code>產生3個DataFrame
D1=pd.DataFrame({'N1':[1,2],
                 'N2':[3,4]})

D2=pd.DataFrame({'N1':[1,2,3],
                 'N2':[3,4,5],
                 'N3':[7,8,9]})

D3=pd.DataFrame({'N1':[0,1,2],
                 'N2':[0,3,4]})
D1
Out[32]: 
   N1  N2
0   1   3
1   2   4

D2
Out[33]: 
   N1  N2  N3
0   1   3   7
1   2   4   8
2   3   5   9

D3
Out[34]: 
   N1  N2
0   0   0
1   1   3
2   2   4

使用concat,行合併.若資料長度不同,缺少的部份會以缺失值NaN補足
pd.concat([D1,D2,D3])
Out[36]: 
   N1  N2   N3
0   1   3  NaN
1   2   4  NaN
0   1   3  7.0
1   2   4  8.0
2   3   5  9.0
0   0   0  NaN
1   1   3  NaN
2   2   4  NaN

使用concat,列合併(axis=1).若資料長度不同,缺少的部份會以缺失值NaN補足
pd.concat([D1,D2,D3],axis=1)
Out[37]: 
    N1   N2  N1  N2  N3  N1  N2
0  1.0  3.0   1   3   7   0   0
1  2.0  4.0   2   4   8   1   3
2  NaN  NaN   3   5   9   2   4
</code></pre>
<h3 id="merge函數">Merge函數</h3>
<p>Merge函數的方式, 類似SQL語言操作資料表. 在結合資料表上有更多工具可以使用.<br>
相同的, 我們使用例子來舉例.</p>
<pre><code>建立DataFrame
d1 = pd.DataFrame({'employee': ['Bob', 'Jake', 'Lisa', 'Sue'], 
                   'group': ['Accounting', 'Engineering', 'Engineering', 'HR']}) 
d2 = pd.DataFrame({'employee': ['Lisa', 'Bob', 'Jake', 'Sue'], 
                   'hire_date': [2004, 2008, 2012, 2014]}) 
d3 = pd.DataFrame({'group': ['Accounting', 'Engineering', 'HR'], 
                   'supervisor': ['Carly', 'Guido', 'Steve']}) 
d4 = pd.DataFrame({'group': ['Accounting', 'Accounting', 
                             'Engineering', 'Engineering', 'HR', 'HR'], 
                   'skills': ['math', 'spreadsheets', 'coding', 'linux', 
                              'spreadsheets', 'organization']}) 
先看一下資料, 資料有許多共同的訊息. 例如: employee.
操作這種類型的資料表,就是要使用merge的好時機
d1
Out[41]: 
  employee        group
0      Bob   Accounting
1     Jake  Engineering
2     Lisa  Engineering
3      Sue           HR

d2
Out[42]: 
  employee  hire_date
0     Lisa       2004
1      Bob       2008
2     Jake       2012
3      Sue       2014

d3
Out[43]: 
         group supervisor
0   Accounting      Carly
1  Engineering      Guido
2           HR      Steve

d4
Out[44]: 
         group        skills
0   Accounting          math
1   Accounting  spreadsheets
2  Engineering        coding
3  Engineering         linux
4           HR  spreadsheets
5           HR  organization                              

結合d1,d2.得到一個簡潔的資料表
pd.merge(d1,d2)
Out[46]: 
  employee        group  hire_date
0      Bob   Accounting       2008
1     Jake  Engineering       2012
2     Lisa  Engineering       2004
3      Sue           HR       2014

結合d1,d2,d3.得到一個簡潔的資料表
pd.merge(pd.merge(d1,d2),d3)
Out[51]: 
  employee        group  hire_date supervisor
0      Bob   Accounting       2008      Carly
1     Jake  Engineering       2012      Guido
2     Lisa  Engineering       2004      Guido
3      Sue           HR       2014      Steve

結合d1,d4.注意這是個多項目資料表的合併
pd.merge(d1,d4)
Out[52]: 
  employee        group        skills
0      Bob   Accounting          math
1      Bob   Accounting  spreadsheets
2     Jake  Engineering        coding
3     Jake  Engineering         linux
4     Lisa  Engineering        coding
5     Lisa  Engineering         linux
6      Sue           HR  spreadsheets
7      Sue           HR  organization
</code></pre>
<p>以下介紹一些使用merge的特殊操作方式<br>
<strong>left_on,right_on參數</strong><br>
當兩個資料集有不同的行名稱但內容定義是相同時, 可以用left_on,right_on參數<br>
這個方式會有重複的行資料, 只要再加上使用drop()函數可以將多餘的資料行移除.<br>
舉例如下</p>
<pre><code>建立DataFrame, 可以看出name的內容跟d1中的employee相同.只是此資料表的行名稱不同
d5 = pd.DataFrame({'name': ['Bob', 'Jake', 'Lisa', 'Sue'], 
                   'salary': [70000, 80000, 120000, 90000]}) 
d5
Out[55]: 
   name  salary
0   Bob   70000
1  Jake   80000
2  Lisa  120000
3   Sue   90000

使用left_on,right_on參數合併資料表, 加上drop去除重複的name資料
pd.merge(d1, d5, left_on="employee", right_on="name").drop('name', axis=1)
Out[56]: 
  employee        group  salary
0      Bob   Accounting   70000
1     Jake  Engineering   80000
2     Lisa  Engineering  120000
3      Sue           HR   90000
</code></pre>
<p><strong>how參數</strong><br>
how參數在merge中預設是inner. 這是什麼意思? 請看例子.</p>
<pre><code>建立DataFrame, 可以只有Mary在d1中的employee
d6 = pd.DataFrame({'employee': ['Bob'], 
                   'age': [37]}) 
d6
Out[59]: 
   age employee
0   37      Bob

將d1,d6合併
pd.merge(d1,d6)
Out[60]: 
  employee       group  age
0      Bob  Accounting   37
</code></pre>
<p>發現inner是什麼意思了嗎? inner就是取兩資料表的交集.<br>
因此我們也可以設定how="outter"就是取兩資料表的聯集, 缺少的部份就是補缺少值NaN</p>
<pre><code>pd.merge(d1,d6,how="outer")
Out[62]: 
  employee        group   age
0      Bob   Accounting  37.0
1     Jake  Engineering   NaN
2     Lisa  Engineering   NaN
3      Sue           HR   NaN
</code></pre>
<h3 id="文字格式資料">文字格式資料</h3>
<p>處理文字格式資料也是一個很重要的技巧. 這個可以使用在很多方面. 例如: 文字採礦, 網路爬蟲等<br>
以下是Python中處理字串的函數.<br>
<code>len() lower() translate() islower() ljust() upper() startswith() isupper() rjust() find() endswith() isnumeric() center() rfind() isalnum() isdecimal() zfill() index() isalpha() split() strip() rindex() isdigit() rsplit() rstrip() capitalize() isspace() partition() lstrip() swapcase() istitle() rpartition()</code><br>
一些常見的用法,我就不介紹了. 如長度, 大小寫轉換等<br>
我這裡舉例如何在文字海中,找到包含關鍵用字的資料, 並對其進行文字清理與更換<br>
例如: 你想在一堆文字中, 找出含有apple這個詞的句子. 再取出其中的販售價格</p>
<pre><code>建立文字資料
s = pd.Series(
        ['Galy apple price: 30 per KG',
         'Jobs has a new dog',
         'Apple cop. release new iphone',
         'Airlift is not a good ideal',
         'Farm apple retailer: 22 per KG',
         'Banana and apple waste 30 KG per year'
        ])
Out[125]: 
0              Galy apple price: 30 per KG
1                       Jobs has a new dog
2            Apple cop. release new iphone
3              Airlift is not a good ideal
4           Farm apple retailer: 22 per KG
5    Banana and apple waste 30 KG per year
dtype: object
</code></pre>
<p>現在我們感興趣的是蘋果apple的銷售價格. 如何在其中找到含有apple的資料呢?<br>
使用contains函數</p>
<pre><code>s.str.contains('apple')
Out[126]: 
0     True
1    False
2    False
3    False
4     True
5     True
dtype: bool

現在我們知道位置0,4,5有包含apple的字眼. 我們可以直接取值

s[s.str.contains('apple')]
Out[127]: 
0              Galy apple price: 30 per KG
4           Farm apple retailer: 22 per KG
5    Banana and apple waste 30 KG per year
dtype: object
接下來我們想要含有apple字眼句子中的數字.這裡需要使用replace與正規標示法
s[s.str.contains('apple')].str.replace('[A-Za-z:]',"")
Out[133]: 
0         30  
4         22  
5        30
</code></pre>
<p>以上, 我們將含有apple字眼句子中的數字找出. 不過注意到, 第三個數字跟價格並不相關<br>
這是做文字採礦需要注意的, 有時候需要多用些關鍵字篩選句子, 才能提升精準度<br>
<strong>ps: 正規標示法在處理文字資料時, 也是很重要的技巧.</strong></p>
<h3 id="時間格式資料">時間格式資料</h3>
<p>時間格式的資料, 也是常會遇見的資料. 例如: 網路交易時間, 氣象資料, 運輸通勤時間等<br>
以下舉例如何使用Pandas中的to_datetime函數去處理這類的時間資料</p>
<pre><code>建立時間資料
date = pd.to_datetime("2018-06-01")
date
Out[135]: Timestamp('2018-06-01 00:00:00')

建立6/1號往後10天的日期
date+pd.to_timedelta(np.arange(10),'D')
Out[138]: 
DatetimeIndex(['2018-06-01', '2018-06-02', '2018-06-03', '2018-06-04',
               '2018-06-05', '2018-06-06', '2018-06-07', '2018-06-08',
               '2018-06-09', '2018-06-10'],
              dtype='datetime64[ns]', freq=None)

以星期表示日期strftime('%A')
(date+pd.to_timedelta(np.arange(10),'D')).strftime('%A')
Out[141]: 
array(['Friday', 'Saturday', 'Sunday', 'Monday', 'Tuesday', 'Wednesday',
       'Thursday', 'Friday', 'Saturday', 'Sunday'], dtype='&lt;U9')              
</code></pre>
<p>建立從每日到每日的時間序列, 使用pd.date_range</p>
<pre><code>pd.date_range('2018-06-02','2018-06-09')
Out[145]: 
DatetimeIndex(['2018-06-02', '2018-06-03', '2018-06-04', '2018-06-05',
               '2018-06-06', '2018-06-07', '2018-06-08', '2018-06-09'],
              dtype='datetime64[ns]', freq='D')
</code></pre>
<p>建立從某天開始往後3天的時間序列, 使用pd.date_range加上periods參數</p>
<pre><code>pd.date_range('2018-06-02',periods=3)
Out[147]: 
DatetimeIndex(['2018-06-02', '2018-06-03', '2018-06-04'], dtype='datetime64[ns]', freq='D')
</code></pre>
<p>建立從某月開始往後6個月的時間序列, 使用pd.date_range加上periods參數與freq參數</p>
<pre><code>pd.period_range('2015-07', periods=6, freq='M')
Out[149]: 
PeriodIndex(['2015-07', '2015-08', '2015-09', '2015-10', '2015-11', '2015-12'], dtype='period[M]', freq='M')
</code></pre>
<h3 id="補充">補充</h3>
<ol>
<li>在讀pd.merge時, 讓我想起R中也有一個merge函數來合併data.frame.</li>
<li>我在學習的過程, 書中的例子不夠簡單. 我使用的例子是跟書中不同.</li>
<li>書中有些特別的技巧, 我沒有介紹. 因為我處理資料的經驗中, 很少使用到.</li>
<li>對於處理非常大數據(GB以上)的朋友, 我建議你去看書中的High-Performance Pandas_ eval() and query()章節.</li>
</ol>

