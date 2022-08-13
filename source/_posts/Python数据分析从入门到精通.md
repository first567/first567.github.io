---
layout:
  - page
title:  Python数据分析从入门到精通
date: 2020-04-20 19:16:53
tags: 
   - [python]
   - [数据分析]
---
<br>
<!--more-->




一. 数据分析

熟悉工具-明确目的-获取数据-数据处理-数据分析-验证结果-结果呈现-数据应用

​                                                                                          表3.1　数据类型对应表　





### 3.3 DataFrame重要属性和函数

DataFrame是Pandas一个重要的对象，它的属性和函数很多，下面先简单了解DataFrame的几个重要属性和函数。重要属性介绍如表3.2所示，重要函数介绍如表3.3所示。

​                                                                                               表3.2　重要属性

​                                                                                                  表3.3　重要函数

### 3.4 导入外部数据

#### 3.4.1　导入.xls或.xlsx文件

导入.xls或.xlsx文件主要使用Pandas的read_excel()方法，语法如下：

pandas.read_excel(io,sheet_name=0,header=0,names=None,index_col=None,usecols=None,squeeze=False,
dtype=None,engine=None,converters=None,true_values=None,false_values=None,skiprows=None,nrow=None,
na_values=None,keep_default_na=True,verbose=False,parse_dates=False,date_parser=None,thousands=None,
comment=None,skipfooter=0,conver_float=True,mangle_dupe_cols=True,**kwds)
常用参数说明：　

io：字符串，.xls或.xlsx文件路径或类文件对象。　

sheet_name：None、字符串、整数、字符串列表或整数列表，默认值为0。字符串用于工作表名称，整数为索引表示工作表位置，字符串列表或整数列表用于请求多个工作表，为None时获取所有工作表。参数值如表3.4所示。

​                                                                                     表3.4　sheet_name参数值　

header：指定作为列名的行，默认值为0，即取第一行的值为列名。数据为除列名以外的数据；若数据不包含列名，则设置header=None。　

names：默认值为None，要使用的列名列表。　

index_col：指定列为行索引，默认值为None，索引0是DataFrame的行标签。

usecols：int、list列表或字符串，默认值为None。　如果为None，则解析所有列。　如果为int，则解析最后一列。　如果为list列表，则解析列号列表的列。　如果为字符串，则表示以逗号分隔的Excel列字母和列范围列表（例如“A:E”或“A,C,E:F”）。范围包括双方。　squeeze：布尔值，默认值为False，如果解析的数据只包含一列，则返回一个Series。　

dtype：列的数据类型名称或字典，默认值为None。例如{'a':np.float64,'b':np.int32}。　

skiprows：省略指定行数的数据，从第一行开始。　

skipfooter：省略指定行数的数据，从尾部数的行开始。

下面通过示例，详细介绍如何导入.xlsx文件。

知识胶囊
导入外部数据，必然要涉及路径问题，下面来了解一下相对路径和绝对路径。　

**相对路径**：相对路径就是以当前文件为基准进行一级级目录指向被引用的资源文件。以下是常用的表示当前目录和当前目录的父级目录的标识符。　../：表示当前文件所在目录的上一级目录。　./：表示当前文件所在的目录（可以省略）。　/：表示当前文件的根目录（域名映射或硬盘目录）。　如果使用系统默认文件路径\，那么，在Python中则需要在路径最前面加一个r，以避免路径里面的\被转义。　

**绝对路径**：绝对路径是文件真正存在的路径，是指从硬盘的根目录（盘符）开始，进行一级级目录指向文件。

##### 2．导入指定的Sheet页

一个Excel文件包含多个Sheet页，通过设置sheet_name参数就可以导入指定Sheet页的数据。

【示例13】　导入指定Sheet页的数据。 \03\13）一个Excel文件包含多家店铺的销售数据，导入其中一家店铺（莫寒）的销售数据，如图3.14所示。
图3.14　原始数据

程序代码如下：

01 import pandas as pd
02 df=pd.read_excel('1 月.xlsx',sheet_name='莫寒')
03 df1=df.head()          #输出前5条数据
运行程序，输出前5条数据，结果如图3.15所示。
除了指定Sheet页的名字，还可以指定Sheet页的顺序，从0开始。例如，sheet_name=0表示导入第一个Sheet页的数据，sheet_name=1表示导入第二个Sheet页的数据，以此类推。
如果不指定sheet_name参数，则默认导入第一个Sheet页的数据。

##### 3．通过行、列索引导入指定行、列数据

DataFrame是二维数据结构，因此它既有行索引又有列索引。当导入Excel数据时，行索引会自动生成，如0、1、2；而列索引则默认将第0行作为列索引（如A,B,…,J）。DataFrame行、列索引的示意图如图3.16所示。

​                                                  

​                                                                            图3.15　导入指定的Sheet页（前5条数据） 



​                                                                                图3.16　DataFrame行、列索引示意图

【示例14】　指定行索引导入Excel数据。 \03\14）
如果通过指定行索引导入Excel数据，则需要设置index_col参数。下面将“买家会员名”作为行索引（位于第0列），导入Excel数据，程序代码如下：

01 import pandas as pd
02 df1=pd.read_excel('1 月.xlsx',index_col=0)     #“买家会员名”为行索引
03 df1=df1.head()                                 #输出前5条数据
运行程序，输出结果如图3.17所示。

图3.17　通过指定行索引导入Excel数据
如果通过指定列索引导入Excel数据，则需要设置header参数，主要代码如下：

df2=pd.read_excel('1月.xlsx',header=1)        #设置第1行为列索引

运行程序，输出结果如图3.18所示。
如果将数字作为列索引，可以设置header参数为None，主要代码如下：

df3=pd.read_excel('1月.xlsx',header=None)    #列索引为数字

运行程序，输出结果如图3.19所示。

图3.19　指定列索引
那么，为什么要指定索引呢？因为通过索引可以快速地检索数据，例如df3[0]，就可以快速检索到“买家会员名”这一列数据。

##### 4.导入指定列数据

一个Excel往往包含多列数据，如果只需要其中的几列，可以通过usecols参数指定需要的列，从0开始（表示第1列，以此类推）。

【示例15】　导入第1列数据。 \03\15）下面导入第1列数据（索引为0），程序代码如下：

01 import pandas as pd
02 df1=pd.read_excel('1 月.xlsx',usecols=[0])       #导入第1列
03 df1.head()
运行程序，输出结果如图3.20所示。
如果导入多列，可以在列表中指定多个值。例如，导入第1列和第4列，主要代码如下：

df2=pd.read_excel('1月.xlsx',usecols=[0,3])
也可以指定列名称，主要代码如下：

df3=pd.read_excel('1月.xlsx',usecols=['买家会员名','宝贝标题'])
运行程序，输出结果如图3.21所示。

​                                                                                     图3.21　导入第1列和第4列数据

#### 3.4.2　导入.csv文件

导入.csv文件主要使用Pandas的read_csv()方法，语法如下：

常用参数说明：　

filepath_or_buffer：字符串，文件路径，也可以是URL链接。　

sep、delimiter：字符串，分隔符。

header：指定作为列名的行，默认值为0，即取第1行的值为列名。数据为除列名以外的数据；若数据不包含列名，则设置header=None。　

names：默认值为None，要使用的列名列表。　

index_col：指定列为索引列，默认值为None，索引0是DataFrame的行标签。　

usecols：int、list列表或字符串，默认值为None。　如果为None，则解析所有列。　如果为int，则解析最后一列。　如果为list列表，则解析列号列表的列。　如果为字符串，则表示以逗号分隔的Excel列字母和列范围列表（例如“A:E”或“A,C,E:F”）。范围包括双方。　dtype：列的数据类型名称或字典，默认值为None。例如{'a':np.float64,'b':np.int32}。　

parse_dates：布尔类型值、int类型值的列表、列表或字典，默认值为False。可以通过parse_dates参数直接将某列转换成datetime64日期类型。例如，df1=pd.read_csv('1月.csv', parse_dates=['订单付款时间'])。　

​		parse_dates为True时，尝试解析索引。　

​		parse_dates为int类型值组成的列表时，如[1,2,3]，则解析1、2、3列的值作为独立的日期列。　

​		parse_date为列表组成的列表，如[[1,3]]，则将1、3列合并，作为一个日期列使用。　

​		parse_date为字典时，如{'总计'：[1, 3]}，则将1、3列合并，合并后的列名为“总计”。　

encoding：字符串，默认值为None，文件的编码格式。Python常用的编码格式是UTF-8。　返回值：返回一个DataFrame。



【示例16】　导入.csv文件。 \03\16）导入.csv文件，程序代码如下：

01 import pandas as pd
02 df1=pd.read_csv('1月.csv'**,encoding=**'gbk')        #导入.csv文件，并指定编码格式
03 df1=df1.head()                                   #输出前5条数据
运行程序，输出结果如图3.22所示。                                                  

​                                                                                            图3.22　导入.csv文件

注意
上述代码中指定了编码格式，即encoding='gbk'。Python常用的编码格式是UTF-8和gbk，默认编码格式为UTF-8。导入.csv文件时，需要通过encoding参数指定编码格式。当将Excel文件另存为.csv文件时，默认编码格式为gbk，此时当编写代码导入.csv文件时，就需要设置编码格式为gbk，与源文件编码格式保持一致；否则会提示错误。

#### 3.4.3　导入.txt文本文件

导入.txt文件同样使用Pandas的read_csv()方法，不同的是需要指定sep参数（如制表符\t）。read_csv()方法读取.txt文件返回一个DataFrame，像表格一样的二维数据结构，如图3.23所示。

【示例17】　导入.txt文件。 \03\17）
下面使用read_csv()方法导入1月.txt文件，主要代码如下：

01 import pandas as pd
02 df1=pd.read_csv('1月.txt',sep='\t',encoding='gbk')
03 print(df1.head())
运行程序，输出结果如图3.24所示。

​                                                                                                         图3.24　导入.txt文本

#### 3.4.4　导入HTML网页

导入HTML网页数据主要使用Pandas的read_html()方法，该方法用于导入带有table标签的网页表格数据，语法如下：

pandas.read_html(io,match='.+',flavor=None,header=None,index_col=None,skiprows=None,attrs=None,parse_
dates=False,thousands=',',encoding=None,decimal='.',converters=None,na_values=None,keep_default_na=True,
displayed_only=True)
常用参数说明：　

io：字符串，文件路径，也可以是URL链接。网址不接受https，可以尝试去掉https中的s后爬取，如http://www.mingribook.com。

match：正则表达式，返回与正则表达式匹配的表格。　

flavor：解析器默认为lxml。　

header：指定列标题所在的行，列表list为多重索引。　

index_col：指定行标题对应的列，列表list为多重索引。　

encoding：字符串，默认为None，文件的编码格式。　

返回值：返回一个DataFrame。
使用read_html()方法前，首先要确定网页表格是否为table类型。例如，NBA球员薪资网页（http://www.espn.com/nba/salaries），右击该网页中的表格，在弹出的快捷菜单中选择“检查元素”命令，查看代码中是否含有表格标签<table>…</table>的字样，如图3.25所示。确定后才可以使用read_html()方法。

​                                                                            图3.25　<table>…</table>表格标签

【示例18】　导入NBA球员薪资数据。 \03\18）
下面使用read_html()方法导入NBA球员薪资数据，程序代码如下：



运行程序，输出结果如图3.26所示。

​                                                                                              图3.26　导入网页数据注意
运行程序，如果出现ImportError: lxml not found, please install it错误提示信息，则需要安装lxml模块。

### 3.5　数据抽取

数据分析过程中，并不是所有的数据都是我们想要的，此时可以抽取部分数据，主要使用DataFrame对**象的loc属性和iloc属性**，示意图如图3.27所示。          

                                                                                         图3.27　loc属性和iloc属性示意图
对象的loc属性和iloc属性都可以抽取数据，区别如下。　

loc属性：以列名（columns）和行名（index）作为参数，当只有一个参数时，默认是行名，即抽取整行数据，包括所有列，如df.loc['A']。　

iloc属性：以行和列位置索引（即0，1，2，…)作为参数，0表示第1行，1表示第2行，以此类推。当只有一个参数时，默认是行索引，即抽取整行数据，包括所有列。如抽取第1行数据，df.iloc[0]。

#### 3.5.1　抽取一行数据

抽取一行数据主要使用loc属性。【

示例19】　抽取一行考试成绩数据。 \03\19）抽取一行名为“明日”的考试成绩数据（包括所有列），程序代码如下：运行程序，输出结果如图3.28所示。
使用iloc属性抽取第1行数据，指定行索引即可，如df.iloc[0]，输出结果同图3.28一样。

[1,2,2,3]

[[1,2,3,4]]

​                                                                                                                图3.28　抽取一行数据

#### 3.5.2　抽取多行数据

1．抽取任意多行数据
**通过loc属性和iloc属性指定行名和行索引即可实现抽取任意多行数据。**

【示例20】　抽取多行考试成绩数据。 \03\20）抽取行名为“明日”和“高袁圆”（即第1行和第3行数据）的考试成绩数据，可以使用loc属性，也可以使用iloc属性，其输出结果都是一样的，主要代码如下：

01 df1=df.loc[['明日','高袁圆']]
02 df1=df.iloc[[0,2]]
运行程序，输出结果如图3.29所示。

​                                                                                                图3.29　抽取多行数据
2．抽取连续任意多行数据
在loc属性和iloc属性中合理地使用冒号（:），即可抽取连续任意多行数据。

【示例21】　抽取连续几个学生的考试成绩。 \03\21）抽取连续几个学生的考试成绩，主要代码如下：

运行程序，控制台输出结果如图3.30所示。

​                                                                                 图3.30　抽取连续任意多行数据

#### 3.5.3　抽取指定列数据

抽取指定列数据，可以直接使用列名，也可以使用loc属性和iloc属性。
1．直接使用列名【示例22】　抽取“语文”和“数学”的考试成绩。 \03\22）
抽取列名为“语文”和“数学”的考试成绩数据，程序代码如下：

运行程序，输出结果如图3.31所示。

2．使用loc属性和iloc属性
前面介绍loc属性和iloc属性均有两个参数：第一个参数代表行；第二个参数代表列。那么这里抽取指定列数据时，行参数不能省略。

【示例23】　抽取指定学科的考试成绩。 \03\23）
下面使用loc属性和iloc属性抽取指定列数据，主要代码如下：



​                         

​                                                                                          图3.32　loc属性和iloc属性

#### 3.5.4　抽取指定行、列数据

抽取指定行、列数据主要使用loc属性和iloc属性，这两个方法的两个参数都指定就可以实现指定行、列数据的抽取。

【示例24】　抽取指定学科和指定学生的考试成绩。 \03\24）使用loc属性和iloc属性抽取指定行、列数据，程序代码如下：

运行程序，控制台输出结果如图3.33所示。

                                                                                   图3.33　抽取指定行、列数据
在上述结果中，第一个输出结果是一个数，不是数据，是由于“df.loc['七月流火','英语']”没有使用方括号[]，导致输出的数据不是DataFrame类型。

#### 3.5.5　按指定条件抽取数据

DataFrame对象实现数据查询有以下3种方式。　取其中的一个元素.iat[x,x]。　基于位置的查询，如.iloc[]、iloc[2,1]。　基于行、列名称的查询，如.loc[x]。

【示例25】　抽取指定学科和指定分数的数据。 \03\25）抽取语文成绩大于105，数学成绩大于88的数据，程序代码如下：



​                                                                                             图3.34　按指定条件抽取数据

### 3.6　数据的增加、修改和删除

#### 3.6.1　增加数据

图3.35　原始数据

##### 1．按列增加数据

按列增加数据，可以通过以下3种方式实现。
（1）直接为DataFrame对象赋值

【示例26】　增加一列“物理”成绩。 \03\26）
增加一列“物理”成绩，程序代码如下：

运行程序，输出结果如图3.36所示。

​                                                                                   图3.36　按列增加数据
（2）使用loc属性在DataFrame对象的最后增加一列

【示例27】　使用loc属性增加一列“物理”成绩。 \03\27）使用loc属性在DataFrame对象的最后增加一列。例如，增加“物理”一列，主要代码如下：

df.loc[:,'物理'] = [88,79,60,50]
在DataFrame对象最后增加一列“物理”，其值为等号右边数据。

（3）在指定位置插入一列
在指定位置插入一列，主要使用insert()方法。

【示例28】　在第1列后面插入“物理”成绩。 \03\28）
例如，在第1列后面插入“物理”，其值为wl的数值，主要代码如下：

01 wl =[88,79,60,50]
02 df.insert(1,'物理',wl)
运行程序，输出结果如图3.37所示。



##### 2．按行增加数据

按行增加数据，可以通过以下两种方式实现。
（1）增加一行数据
增加一行数据主要使用loc属性实现。

【示例29】　在成绩表中增加一行数据。 \03\29）在成绩表中增加一行数据，即“钱多多”同学的成绩，主要代码如下：

df.loc['钱多多'] = [100,120,99]
（2）增加多行数据

增加多行数据主要使用**字典**结合**append()**方法实现。

【示例30】　在原有数据中增加几名同学的考试成绩。 \03\30）在原有数据中增加“钱多多”“童年”“无名”同学的考试成绩，主要代码如下：

01 df_insert=pd.DataFrame({'语文':[100,123,138],'数学':[99,142,60],'英语':[98,139,99]},index = ['钱多多','童年','无名'])
02 df1 = df.append(df_insert)

​                                              



​                                                    

##### 1．修改列标题

修改列标题主要使用DataFrame对象的cloumns属性，直接赋值即可。

【示例31】　修改“数学”的列名。 \03\31）将“数学”修改为“数学（上）”，主要代码如下：

df.columns=['语文','数学（上）','英语']

上述代码中，即使只修改“数学”为“数学（上）”，但是也**要将所有列的标题全部写上；**否则将报错。
下面再介绍一种方法，使用DataFrame对象的rename()方法修改列标题。

【示例32】　修改多个学科的列名。 \03\32）将“语文”修改为“语文（上）”、“数学”修改为“数学（上）”、“英语”修改为“英语（上）”，主要代码如下：

df1=df.rename(columns = {'语文':'语文（上）','数学':'数学（上）','英语':'英语（上）'},inplace = True)

上述代码中，参数inplace为True，表示直接修改df；否则，不修改df，只返回修改后的数据。
运行程序，输出结果分别如图3.41和图3.42所示。

##### 2．修改行标题

修改行标题主要使用DataFrame对象的index属性，直接赋值即可。

【示例33】　将行标题统一修改为数字编号。 \03\33）
将行标题统一修改为数字编号，主要代码如下：

df.index=list('1234')



使用DataFrame对象的rename()方法也可以修改行标题。例如，将行标题统一修改为数字编号，主要代码如下：

df.rename({'明日':1,'七月流火':2,'高袁圆':3,'二月二':4},axis=0,inplace = True)

##### 3．修改数据

修改数据主要使用DataFrame对象的loc属性和iloc属性。

【示例34】　修改学生成绩数据。 \03\34）
（1）修改整行数据
例如，修改“明日”同学的各科成绩，主要代码如下：

df.loc['明日']=[120,115,109]
如果各科成绩均加10分，可以直接在原有值上加10，主要代码如下：

df.loc['明日']=df.loc['明日']+10
（2）修改整列数据
例如，修改所有同学的“语文”成绩，主要代码如下：

df.loc[:,'语文']=[115,108,112,118]
（3）修改某一数据

例如，修改“明日”同学的“语文”成绩，主要代码如下：

df.loc['明日','语文']=115
（4）使用iloc属性修改数据
通过iloc属性指定行、列位置实现修改数据，主要代码如下：

01 df.iloc[0,0]=115                        #修改某一数据
02 df.iloc[:,0]=[115,108,112,118]          #修改整列数据
03 df.iloc[0,:]=[120,115,109]              #修改整行数据

#### 3.6.3　删除数据

删除数据主要使用DataFrame对象的drop()方法。语法如下：

DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')
参数说明：　

labels：表示行标签或列标签。　

axis：axis = 0，表示按行删除；

​			axis = 1，表示按列删除。默认值为0，即按行删除。　

index：删除行，默认值为None。　

columns：删除列，默认值为None。

level：针对有两级索引的数据。level = 0，表示按第1级索引删除整行；level = 1表示按第2级索引删除整行，默认值为None。　inplace：可选参数，对原数组做出修改并返回一个新数组。默认值为False，如果值为True，那么原数组直接就被替换。　

errors：参数值为ignore或raise，默认值为raise，如果值为ignore（忽略），则取消错误。

##### 1．删除行、列数据

【示例35】　删除学生成绩数据。 \03\35）
删除指定的学生成绩数据，主要代码如下：

##### 2．删除特定条件的行

删除满足特定条件的行，首先找到满足该条件的行索引，然后再使用drop()方法将其删除。

【示例36】　删除符合条件的学生成绩数据。 \03\36）
删除“数学”成绩中包含88的行、“语文”成绩中小于110的行，主要代码如下：

01 df.drop(index=df[df['数学'].**isin**([88])].index[0],inplace=True)      #删除“数学”成绩中包含88的行
02 df.drop(index=df[df['语文']<110].index[0],inplace=True)             #删除“语文”成绩中小于110的行说明
以上代码中的方法都可以实现删除指定的行、列数据，读者选择一种即可。

### 3.7　数据清洗

#### 3.7.1　缺失值查看与处理

缺失值是指由于某种原因导致数据为空，这种情况一般有不处理、删除、填充／替换、插值（以均值／中位数／众数等填补）这4种处理方式。

##### 1．缺失值查看

首先需要找到缺失值，主要使用DataFrame对象的info()方法。

【示例37】　查看数据概况。 \03\37）以淘宝销售数据为例，首先输出数据，然后使用info()方法查看数据，程序代码如下：

01 import pandas as pd
02 df=pd.read_excel('TB2018.xls')
03 print(df)
04 print(df.info())

运行程序，控制台输出结果如图3.43所示。

图3.43　缺失值查看
在Python中，缺失值一般用NaN表示，如图3.43所示。通过info()方法可看到“买家会员名”“买家实际支付金额”“宝贝标题”“订单付款时间”的非空数量是10，而“宝贝总数量”和“类别”的非空数量是8，那么说明这两项存在空值。

【示例38】　判断数据是否存在缺失值。 \03\38）
接下来，判断数据是否存在缺失值还可以使用isnull()方法和notnull()方法，主要代码如下： 

01  print(df.isnull())
02  print(df.notnull())

​                                                                                              图3.44　判断缺失值
使用isnull()方法缺失值返回True，非缺失值返回False；而notnull()方法与isnull()方法正好相反，缺失值返回False，非缺失值返回True。
如果使用df[df.isnull() == False]，

则会将所有非缺失值的数据找出来，只针对Series对象。

##### 2．缺失值删除处理

通过前面的判断得知数据缺失情况，下面将缺失值删除，主要使用dropna()方法，该方法用于删除含有缺失值的行，主要代码如下：

df1=df.dropna()
运行程序，输出结果如图3.45所示。说明
有些时候数据可能存在整行为空的情况，此时可以在dropna()方法中指定参数how='all'，删除所有空行。



​                                                                                   图3.45　缺失值删除处理1
从运行结果得知：dropna()方法将所有包含缺失值的数据全部删除了。那么，此时如果我们认为有些数据虽然存在缺失值，但是不影响数据分析，那么可以使用以下方法处理。例如，上述数据中只保留“宝贝总数量”不存在缺失值的数据，而类别是否缺失不关注，则可以使用notnull()方法判断，主要代码如下：

df2=df[df['宝贝总数量'].notnull()]
运行程序，输出结果如图3.46所示。

图3.46　缺失值删除处理2

##### 3．缺失值填充处理

对于缺失数据，如果比例高于30%可以选择放弃这个指标，做删除处理；低于30%尽量不要删除，而是选择将这部分数据填充，一般以0、均值、众数（大多数）填充。DataFrame对象中的fillna()函数可以实现填充缺失数据，pad/ffill表示用前一个非缺失值去填充该缺失值；backfill/bfill表示用下一个非缺失值填充该缺失值；None用于指定一个值去替换缺失值。

【示例39】　将NaN填充为0。 \03\39）对于用于计算的数值型数据如果为空，可以选择用0填充。例如，将“宝贝总数量”为空的数据填充为0，主要代码如下：


运行程序，输出结果如图3.47所示。

​                                                                                                图3.47　缺失值填充处理

#### 3.7.2　重复值处理

对于数据中存在的重复数据，包括重复的行或者几行中某几列的值重复一般做删除处理，主要使用DataFrame对象的drop_duplicates()方法。

【示例40】　处理淘宝电商销售数据中的重复数据。 \03\40）下面以“1月.xlsx”淘宝销售数据为例，对其中的重复数据进行处理。
（1）判断每一行数据是否重复（完全相同），主要代码如下：

df1.duplicated()
如果返回值为False表示不重复，返回值为True表示重复。
（2）去除全部的重复数据，主要代码如下：

df1.drop_duplicates()#默认保留一行
（3）去除指定列的重复数据，主要代码如下：

df1.drop_duplicates(['买家会员名'])
（4）保留重复行中的最后一行，主要代码如下：

df1.drop_duplicates(['买家会员名'],keep='last')

说明
以上代码中参数keep的值有3个。当keep='first'表示保留第一次出现的重复行，**是默认值**；当keep为另外两个取值，即last和False时，分别表示保留最后一次出现的重复行和去除所有重复行。
（5）直接删除，保留一个副本，主要代码如下：

df1.drop_duplicates(['买家会员名','买家支付宝账号'],inplace=Fasle)
inplace=True表示直接在原来的DataFrame上删除重复项，而默认值False表示删除重复项后生成一个副本。

#### 3.7.3　异常值的检测与处理

首先了解一下什么是异常值。在数据分析中异常值是指超出或低于正常范围的值，如年龄大于200、身高大于3米、宝贝总数量为负数等类似数据。那么这些数据如何检测呢？主要有以下几种方法。
（1）根据给定的数据范围进行判断，不在范围内的数据视为异常值。
（2）均方差。
在统计学中，如果一个数据分布近似正态分布（数据分布的一种形式，正态分布的概率密度函数曲线呈钟形，两头低、中间高、左右对称，因此人们又经常称之为钟形曲线），那么大约68%的数据值会在均值的一个标准差范围内，大约95%会在两个标准差范围内，大约99.7%会在3个标准差范围内。
（3）箱形图。
箱形图是显示一组数据分散情况资料的统计图。它可以将数据通过四分位数的形式进行图形化描述。箱形图通过上限和下限作为数据分布的边界。任何高于上限或低于下限的数据都可以认为是异常值，如图3.48所示。

​                                                                                            图3.48　箱形图说明
有关箱形图的介绍以及如何通过箱形图识别异常值可参见第6章。
了解了异常值的检测，接下来介绍如何处理异常值，主要包括以下几种处理方式。
（1）最常用的方式是删除。
（2）将异常值当缺失值处理，以某个值填充。
（3）将异常值当特殊情况进行分析，研究异常值出现的原因。

缺失值替换

replace(to_repalce=None,value=None,inplace=False,limit=None,regex=False,method='pad')

to_repalce:指定需要替换的原值，可以是字符型，正则表达式，列表，series，整数，浮点数或None，例如{‘V1’:n1,'v2':n2}表示使用n1,n2替换掉原来的v1,v2,这时的value必须为None

value：指定用于替换的新值

inplace：True修改原始数据，False仅修改视图

limit：限制向前，向后填充的最大个数

regex：默认False，若为True则to_palce必须为一个字符串。



pd.where(cond,value)

满足条件的保留，不满足条件的修改为value

### 3.8 索引设置

索引能够快速查询数据，本节主要介绍索引的作用以及索引的应用。

#### 3.8.1　索引的作用

索引的作用相当于图书的目录，可以根据目录中的页码快速找到所需的内容。Pandas索引的作用如下。　

更方便查询数据。　

使用索引可以提升查询性能。　

如果索引是唯一的，Pandas会使用哈希表优化，查找数据的时间复杂度为O(1)。　

如果索引不是唯一的，但是有序，Pandas会使用二分查找算法，查找数据的时间复杂度为O(logN)。　

如果索引是完全随机的，那么每次查询都要扫描数据表，查找数据的时间复杂度为O(N)。　自动的数据对齐功能，示意图如图3.49所示。

​                                                                                    图3.49　自动数据对齐示意图
实现上述效果，程序代码如下：

01 import pandas as pd
02 s1 = pd.Series([10,20,30],index= list("abc"))
03 s2 = pd.Series([2,3,4],index=list("bcd"))
04 print(s1 + s2)　

强大的数据结构。　

基于分类数的索引，提升性能。　

多维索引，用于groupby多维聚合结果等。　

时间类型索引，强大的日期和时间的方法支持。

#### 3.8.2　重新设置索引

Pandas有一个很重要的方法是reindex()，它的作用是创建一个适应新索引的新对象。语法如下：

DataFrame.reindex(labels = None,index = None,columns = None,axis = None,method = None,copy = True,level =
None,fill_value = nan,limit = None,tolerance = None)
常用参数说明：　

labels：标签，可以是数组，默认值为None（无）。　

index：行索引，默认值为None。　

columns：列索引，默认值为None。

axis：轴，axis=0表示行，axis=1表示列。默认值为None。　

method：默认值为None，重新设置索引时，选择插值（一种填充缺失数据的方法）方法，其值可以是None、bfill/backfill（向后填充）、ffill/pad（向前填充）等。　

fill_value：缺失值要填充的数据。如缺失值不用NaN填充，而用0填充，则设置fill_value=0即可。



##### 1．对Series对象重新设置索引

【示例41】　重新设置物理成绩的索引。 \03\41）
在3.2.3节已经建立了一组学生的物理成绩，下面重新设置索引，程序代码如下：

01 import pandas as pd
02 s1=pd.Series([88,60,75],index=[1,2,3])
03 print(s1)
04 print(s1.reindex([1,2,3,4,5]))

​                                                                                                 图3.51　重新设置索引
从运行结果得知：reindex()方法根据新索引进行了重新排序，并且对缺失值自动填充NaN。如果不想用NaN填充，则可以为fill_value参数指定值，如0，主要代码如下：

s1.reindex([1,2,3,4,5],fill_value=0)
而对于一些有一定顺序的数据，我们可能需要插值（插值是一种填充缺失数据的方法）来填充缺失的数据，可以使用method参数。

【示例42】　向前和向后填充数据。 \03\42）

向前填充（和前面数据一样）、向后填充（和后面数据一样），主要代码如下：

01 print(s1.reindex([1,2,3,4,5],method='ffill'))   #向前填充
02 print(s1.reindex([1,2,3,4,5],method='bfill'))   #向后填充

##### 2．对DataFrame对象重新设置索引

对于DataFrame对象，reindex()方法用于修改行索引和列索引。

【示例43】　创建成绩表并重新设置索引。 \03\43）通过二维数组创建成绩表，程序代码如下：



df.reindex(['mr001','mr002','mr003','mr004','mr005'])
通过reindex()方法重新设置列索引，主要代码如下：

df.reindex(columns=['语文','物理','数学','英语'])
通过reindex()方法重新设置行索引和列索引，主要代码如下：

df.reindex(index=['mr001','mr002','mr003','mr004','mr005'],columns=['语文','物理','数学','英语'])
运行程序，控制台输出结果分别为原始数据（见图3.52）、重新设置行索引（见图3.53）、重新设置列索引（见图3.54）、重新设置行、列索引（见图3.55）。

​                                                                                              

#### 3.8.3　设置某列为行索引

设置某列为行索引主要使用set_index()方法。

【示例44】　设置“买家会员名”为行索引。 \03\44）
首先，导入“1月.xlsx”Excel文件，程序代码如下：

运行程序，输出结果如图3.56所示。
此时默认行索引为0、1、2、3、4，下面将“买家会员名”作为行索引，主要代码如下：

df2=df.set_index(['买家会员名'])
运行程序，输出结果如图3.57所示。

​                                                                                                图3.56　1月淘宝销售数据（部分数据）

​                                                                                                       图3.57　设置“买家会员名”为索引
如果在set_index()方法中传入参数drop=True，则会删除“买家会员名”；如果传入drop=False，则会保留“买家会员名”。默认为False。

#### 3.8.4　数据清洗后重新设置连续的行索引

在对Dataframe对象进行数据清洗后，例如去掉含NaN的行之后，发现行索引还是原来的行索引，对比效果如图3.58和图3.59所示。

​                                                                                            图3.58　原数据

​                                                                           图3.59　数据清洗后还是原来的索引

【示例45】　删除数据后重新设置索引。 \03\45）

如果要重新设置索引可以使用reset_index()方法，在删除缺失数据后重新设置索引，主要代码如下：

df2=df.dropna().reset_index(drop=True)
运行程序，输出结果如图3.60所示。


另外，对于分组统计后的数据，有时也需要重新设置连续的行索引，方法同上。

### 3.9　数据排序与排名

本节主要介绍数据的各种排序和排名方法。

#### 3.9.1　数据排序

DataFrame数据排序主要使用sort_values()方法，该方法类似于SQL中的ORDER BY。sort_values()方法可以根据指定行／列进行排序，语法如下：

DataFrame.sort_values(by,axis=0,ascending=True,inplace=False,kind='quicksort',na_position='last',ignore_
index=False)
参数说明：　

by：要排序的名称列表。

axis：轴，axis=0表示行，axis=1表示列。默认值为0，即按行排序。　

ascending：升序或降序排序，布尔值，指定多个排序可以使用布尔值列表。默认值为True。　

inplace：布尔值，默认值为False，如果值为True，则就地排序。　

kind：指定排序算法，值为quicksort（快速排序）、mergesort（混合排序）或heapsort（堆排），默认值为quicksort。　

na_position：空值（NaN）的位置，值为first空值在数据开头，值为last空值在数据最后，默认值为last。　

ignore_index：布尔值，是否忽略索引，值为True标记索引（从0开始按顺序的整数值），值为False则忽略索引。

##### 1．按一列数据排序



Spyder变量浏览窗口本身也支持数据排序，单击需要排序的列即可实现升序或降序排序。
程序代码如下：

##### 2．按多列数据排序


主要代码如下：

df1=df.sort_values(by=['图书名称','销量'])

##### 3．对统计结果排序



按“类别”分组统计销量并进行降序排序，统计排序后的效果如图3.64所示。



​                                                                                 图3.64　按“类别”分组统计销量并降序排序
主要代码如下：

01 df1=df.groupby(["类别"])["销量"].sum().reset_index()

2 df2=df1.sort_values(by='销量',ascending=False)

##### 4．按行数据排序

【示例49】　按行数据排序。 \03\49）
按行排序，主要代码如下：

df=dfrow.sort_values(by=0,ascending=True,axis=1)

注意
**按行排序的数据类型要一致**，否则会出现错误提示。

#### 3.9.2　数据排名

排名是根据Series对象或DataFrame的某几列的值进行排名的，主要使用rank()方法，语法如下：

DataFrame.rank(axis=0,method='average',numeric_only=None,na_option='keep',ascending=True,pct=False)
参数说明：　

axis：轴，axis=0表示行，axis=1表示列。默认值为0，即按行排序。　

method：表示在具有相同值的情况下所使用的排序方法。设置值如下。　

​	average：默认值，平均排名。

​	min：最小值排名。　

​	max：最大值排名。　

​	first：按值在原始数据中的出现顺序分配排名。　

​	dense：密集排名，类似最小值排名，但是排名每次只增加1，即排名相同的数据只占一个名次。　

numeric_only：对于DataFrame对象，如果设置值为True，则只对数字列进行排序。　

na_option：空值的排序方式，设置值如下。　

​	keep：保留，将空值等级赋值给NaN值。　

​	top：如果按升序排序，则将最小排名赋值给NaN值。　

​	bottom：如果按升序排序，则将最大排名赋值给NaN值。　

ascending：升序或降序排序，布尔值，指定多个排序可以使用布尔值列表。默认值为True。　

pct：布尔值，是否以百分比形式返回排名。默认值为False。

1．顺序排名



01 df['平均排名']=df['销量'].rank(ascending=False)

02 df1=df[['图书名称','销量','平均排名']]
程序运行结果如图3.66所示。
3．最小值排名
排名相同的，按顺序排名取最小值作为排名，主要代码如下：

df['最小值排名']=df['销量'].rank(method="min",ascending=False)
4．最大值排名
排名相同的，按顺序排名取最大值作为排名，主要代码如下：

df['最大值排名']=df['销量']

rank(method="max",ascending=False)





### sum()

DataFrame.sum(axis=None, skipna=None, level=None, numeric_only=None, min_count=0, **kwargs)
参数说明：　

axis：axis=1表示行，axis=0表示列，默认值为None（无）。　skipna：布尔型，表示计算结果是否排除NaN/Null值，默认值为None。

level：表示索引层级，默认值为None。　

numeric_only：仅数字，布尔型，默认值为None。　

min_count：表示执行操作所需的数目，整型，默认值为0。　**kwargs：要传递给函数的附加关键字参数。　

返回值：返回Series对象或DataFrame对象。行或列求和数据。

【示例01】　计算语文、数学和英语三科的总成绩。 \04\01）
首先，创建一组DataFrame类型的数据，包括语文、数学和英语三科的成绩，如图4.1所示。
程序代码如下：

df['总成绩']=df.sum(axis=1)



### mean()

DataFrame.mean(axis=None, skipna=None, level=None, numeric_only=None, kwargs)
参数说明：　

axis：axis=1表示行，axis=0表示列，默认值为None（无）。　

skipna：布尔型，表示计算结果是否排除NaN/Null值，默认值为None。　

level：表示索引层级，默认值为None。　

numeric_only：仅数字，布尔型，默认值为None。　

kwargs：要传递给函数的附加关键字参数。　

返回值：返回Series对象或DataFrame对象。行或列平均值数据。

### max()

DataFrame.max(axis=None, skipna=None, level=None, numeric_only=None, **kwargs)
参数说明：　**

**axis：axis=1表示行，axis=0表示列，默认值为None（无）。　skipna：布尔型，表示计算结果是否排除NaN/Null值，默认值为None。　

**level：表示索引层级，默认值为None。　

**numeric_only：仅数字，布尔型，默认值为None。　

kwargs：要传递给函数的附加关键字参数。　

返回值：返回Series对象或DataFrame对象。行或列最大值数据。

### median()



中位数又称中值，是统计学专有名词，是指按顺序排列的一组数据中位于中间位置的数，其不受异常值的影响。例如，年龄23、45、35、25、22、34、28这7个数，中位数就是排序后位于中间的数字，即28；而年龄23、45、35、25、22、34、28、27这8个数，中位数则是排序后位于中间两个数的平均值，即27.5。在Python中直接调用DataFrame对象的median()函数就可以轻松实现中位数的运算，语法如下：

DataFrame.median(axis=None,skipna=None,level=None,numeric_only=None,**kwargs)
参数说明：　**

**axis：axis=1表示行，axis=0表示列，默认值为None（无）。　skipna：布尔型，表示计算结果是否排除NaN/Null值，默认值为None。　

**level：表示索引层级，默认值为None。　

**numeric_only：仅数字，布尔型，默认值为None。　

kwargs：要传递给函数的附加关键字参数。　

返回值：返回Series对象或DataFrame对象。



### mode()

什么是众数？众数的众字有多的意思，顾名思义，众数就是一组数据中出现最多的数称为众数，它代表了数据的一般水平。
在Python中通过调用DataFrame对象的mode()函数可以实现众数运算，语法如下：

DataFrame.mode(axis=0,numeric_only=False,dropna=True)
参数说明：　

axis：axis=1表示行，axis=0表示列，默认值为0。　

numeric_only：仅数字，布尔型，默认值为False。如果值为True，则仅适用于数字列。　

dropna：是否删除缺失值，布尔型，默认值为True。　

返回值：返回Series对象或DataFrame对象。

### var()

方差
接着来看一下总体波动（方差和），“小黑”的数据是73.2，“小白”的数据是949.2，很明显“小黑”的物理成绩波动较小，发挥更稳定，所以应该选“小黑”参加物理竞赛。
以上举例就是方差的意义。大数据时代，它能够帮助我们解决很多身边的问题、协助我们做出合理的决策。
在Python中通过调用DataFrame对象的var()函数可以实现方差运算，语法如下：

**DataFrame.var(axis=None,skipna=None,level=None,ddof=1,numeric_only=None,kwargs)**
参数说明：　

axis：axis=1表示行，axis=0表示列，默认值为None（无）。　skipna：布尔型，表示计算结果是否排除NaN/Null值，默认值为None。　

level：表示索引层级，默认值为None。　

ddof：整型，默认值为1。自由度，计算中使用的除数是N-ddof，其中N表示元素的数量。　

numeric_only：仅数字，布尔型，默认值为None。　

kwargs：要传递给函数的附加关键字参数。　

返回值：返回Series对象或DataFrame对象。

### std()

标准差又称均方差，是方差的平方根，用来表示数据的离散程度。
在Python中通过调用DataFrame对象的std()函数求标准差，语法如下：

DataFrame.std(axis=None,skipna=None,level=None,ddof=1,numeric_only=None,**kwargs)
std()函数的参数与var()函数一样，这里不再赘述。



### 4.1.9　求分位数（quantile()函数）

分位数也称分位点，它以概率依据将数据分割为几个等份，常用的有中位数（即二分位数）、四分位数、百分位数等。分位数是数据分析中常用的一个统计量，经过抽样得到一个样本值。例如，经常会听老师说：“这次考试竟然有20%的同学不及格！”，那么这句话就体现了分位数的应用。在Python中通过调用DataFrame对象的quantile()函数求分位数，语法如下：

**DataFrame.quantile(q=0.5,axis=0,numeric_only=True, interpolation='linear')**
参数说明：　

q：浮点型或数组，默认为0.5（50%分位数），其值为0～1。　

axis：axis=1表示行，axis=0表示列。默认值为0。　

numeric_only：仅数字，布尔型，默认值为True。　

interpolation：内插值，可选参数[{‘linear’,‘lower’,‘higher’,‘midpoint’,‘nearest’}]用于指定要使用的插值方法，当期望的分位数为数据点i～j时。　

​	linear’：i+(j-i)×分数，其中分数是指数被i和j包围的小数部分。　

​	lower：i。　

​	higher：j。　 

​	nearest：i或j二者以最近者为准。　

​	midpoint：(i+j)/2。　

返回值：返回Series或DataFrame对象。

【示例10】　通过分位数确定被淘汰的35%的学生。 \04\10）
以学生成绩为例，数学成绩分别为120、89、98、78、65、102、112、56、79、45的10名同学，现根据分数淘汰35%的学生，该如何处理？首先使用quantile()函数计算35%的分位数，然后将学生成绩与分位数比较，筛选小于等于分位数的学生，程序代码如下：





### 4.2.1　设置小数位数

设置小数位数主要使用DataFrame对象的round()函数，该函数可以实现四舍五入，而它的decimals参数则用于设置保留小数的位数，设置后数据类型不会发生变化，依然是浮点型。语法如下：

DataFrame.round(decimals=0, *args, **kwargs)　**

decimals：每一列四舍五入的小数位数，整型、字典或Series对象。如果是整数，则将每一列四舍五入到相同的位置。否则，将字典和Series舍入到可变数目的位置；如果小数是类似于字典的，那么列名应该在键中；如果小数是级数，列名应该在索引中。没有包含在小数中的任何列都将保持原样。非输入列的小数元素将被忽略。　

args：附加的关键字参数。　

kwargs：附加的关键字参数。　

返回值：返回DataFrame对象。

当然，保留小数位数也可以用自定义函数，例如，为DataFrame对象中的各个浮点值保留两位小数，主要代码如下：

df.applymap(lambda x: '%.2f'%x)



### 4.2.2　设置百分比

在数据分析过程中，有时需要百分比数据。那么，利用自定义函数将数据进行格式化处理，处理后的数据就可以从浮点型转换成带指定小数位数的百分比数据，主要使用apply()函数与format()函数。

【示例13】　将指定数据格式化为百分比数据。 \04\13）
将A1列的数据格式化为百分比数据，程序代码如下：



### 4.2.3　设置千位分隔符

由于业务需要，有时需要将数据格式化为带千位分隔符的数据。那么，处理后的数据将不再是浮点型而是对象型。

df['麻阳']=df['妈呀']。apply(lambda x:format(int(x),','))





### 4.3.1　分组groupby()



**DataFrame.groupby(by=None,axis=0,level=None,as_index=True,sort=True,group_keys=True,squeeze=False,observed=False)**

参数说明：　

by：映射、字典或Series对象、数组、标签或标签列表。如果by是一个函数，则对象索引的每个值都调用它；如果传递了一个字典或Series对象，则使用该字典或Series对象值来确定组；如果传递了数组ndarray，则按原样使用这些值来确定组。　

axis：axis=1表示行，axis=0表示列。默认值为0。　

level：表示索引层级，默认值为None（无）。　

as_index：布尔型，默认值为True，返回以组标签为索引的对象。　sort：对组进行排序，布尔型，默认值为True。　

group_keys：布尔型，默认值为True，调用apply()函数时，将分组的键添加到索引以标识片段。　

squeeze：布尔型，默认值为False。如果可能，减少返回类型的维度；否则返回一致类型。　

observed： *bool, default False* 布尔型, 观察者, 默认为False。当以石斑鱼为分类时，才会使用该参数。如果参数值为True，则仅显示分类石斑鱼的观测值；如果参数值为False，则显示分类石斑鱼的所有值。

返回值：返回DataFrameGroupBy，返回包含有关组的信息的groupby对象。

#### 1．按照一列分组统计	

【示例15】　根据“一级分类”统计订单数据。 \04\15）
按照图书“一级分类”对订单数据进行分组统计求和，程序代码如下：



​                                 图4.10　按照一列分组统计

#### 2．按照多列分组统计

多列分组统计，以列表形式指定列。

【示例16】　根据两级分类统计订单数据。 \04\16）
按照图书“一级分类”和“二级分类”对订单数据进行分组统计求和，主要代码如下：

01 #抽取数据
02 df1=df[['一级分类','二级分类','7天点击量','订单预定']]
03 df1=df1.groupby(['一级分类','二级分类']).sum()    #分组统计求和







#### 3．分组并按指定列进行数据计算

前面介绍的分组统计是按照所有列进行汇总计算的，那么如何按照指定列汇总计算呢？

【示例17】　统计各编程语言的7天点击量。 \04\17）
统计各编程语言的7天点击量，首先按“二级分类”分组，然后抽取“7天点击量”列并对该列进行求和运算，主要代码如下：

df1=df1.groupby('二级分类')['7天点击量'].sum()




### 4.3.3　对分组的某列或多列使用聚合函数（agg()函数）

Python也可以实现像SQL中的分组聚合运算操作，主要通过groupby()函数与agg()函数实现。【示例20】　对分组统计结果使用聚合函数。 \04\20）
按“一级分类”分组统计“7天点击量”“订单预定”的平均值和总和，主要代码如下：

print(df1.groupby('一级分类').agg(['mean','sum']))
运行程序，控制台输出结果如图4.14所示。





【示例21】　针对不同的列使用不同的聚合函数。 \04\21）
在上述示例中，还可以针对不同的列使用不同的聚合函数。例如，按“一级分类”分组统计“7天点击量”的平均值和总和、“订单预定”的总和，主要代码如下：

print(df1.groupby('一级分类').agg({'7天点击量':['mean','sum'], '订单预定':['sum']}))


​           图4.15　分组统计“7天点击量”的平均值和总和、“订单预定”的总和

【示例22】　通过自定义函数实现分组统计。 \04\22）
通过自定义函数也可以实现数据分组统计。例如，统计1月份销售数据中，购买次数最多的产品，主要代码如下：







## 4.4　数据移位

什么是数据移位？例如，分析数据时需要上一条数据怎么办？当然是移动至上一条，从而得到该条数据，这就是数据移位。在Pandas中，使用shift()方法可以获得上一条数据，该方法返回向下移位后的结果，从而得到上一条数据。例如，获取某学生上一次英语成绩，如图4.21所示。

DataFrame.shift(periods=1, freq=None, axis=0)
参数说明：　

periods：表示移动的幅度，可以是正数，也可以是负数，默认值是1，1表示移动一次。注意这里移动的都是数据，而索引是不移动的，移动之后是没有对应值的，赋值为NaN。　

freq：可选参数，默认值为None，只适用于时间序列，如果这个参数存在，那么会按照参数值移动时间索引，而数据值没有发生变化。　

axis：axis=1表示行，axis=0表示列。默认值为0。



### 4.5.1　一列数据转换为多列数据

一列数据转换为多列数据的情况在日常工作中经常会用到，从各种系统中导出的订单号、名称、地址很多都是复合组成的（即由多项内容组成），那么，这些列在查找、统计、合并时就没办法使用，需要将它们拆分开。例如，地址信息由省市区街道门牌号等信息组成，如果按省、市或区统计数据，就需要将地址信息中的“省”“市”“区”拆分开，此时就应用到了一列数据转多列数据，通常使用以下方法。

#### 1．split()方法

Pandas的DataFrame对象中的str.split()内置方法可以实现分割字符串，语法如下：

Series.str.split(pat=None, n=-1, expand=False)
参数说明：　

pat：字符串、符号或正则表达式，字符串分割的依据，默认以空格分割字符串。　

n：整型，分割次数，默认值是-1，0或-1都将返回所有拆分。　expand：布尔型，分割后的结果是否转换为DataFrame，默认值是False。　

返回值：系列、索引、DataFrame或多重索引。




#### 2．join()方法与split()方法结合



df = df.join(df['宝贝标题'].str.split(', ', expand=True))







【示例28】　对元组数据进行分隔。 \04\28）
首先，创建一组包含元组的数据，程序代码如下：

01  import pandas as pd
02  df = pd.DataFrame({'a':[1,2,3,4,5], 'b':[(1,2), (3,4),(5,6),(7,8),(9,10)]})
03  print(df)

然后，使用apply()函数对元组进行分隔，主要代码如下：

df[['b1', 'b2']] = df['b'].apply(pd.Series)
或者使用join()方法结合apply()函数，主要代码如下：

df= df.join(df['b'].apply(pd.Series))















#### 3．pivot()方法

pivot()方法针对列的值，即指定某列的值作为行索引，指定某列的值作为列索引，然后再指定哪些列作为索引对应的值。unstack()方法针对索引进行操作，pivot()方法针对值进行操作。但实际上，二者的功能往往可以互相实现。
pivot()方法的语法如下：

DataFrame.pivot(index=None, columns=None, values=None)
参数说明：　

index：字符串或对象，可选参数。列用于创建新DataFrame数据的索引。如果没有，则使用现有索引。　

columns：字符串或对象，列用于创建新DataFrame的列。　

values：列用于填充新DataFrame的值，如果未指定，则将使用所有剩余的列，结果将具有分层索引列。　

返回值：DataFrame对象或Series对象。


使用pivot()方法转换学生成绩表，主要代码如下：

01 df=pd.read_excel('grade.xls',sheet_name='英语3')         #导入Excel文件
02 df1=df.pivot(index='序号',columns='班级',values='得分')

图4.33　使用pivot()方法转换学生成绩表

### 4.5.3　DataFrame转换为字典

DataFrame转换为字典主要使用DataFrame对象的to_dict()方法，以索引作为字典的键（key），以列作为字典的值（value）。例如，有一个DataFrame对象（索引为“类别”、列为“数量”），通过to_dict()方法就会生成一个字典，示意图如图4.34所示。如果DataFrame对象包含两列，那么to_dict()方法就会生成一个两层的字典（dict），第一层是列名作为字典的键（key），第二层以索引列的值作为字典的键（key），以列值作为字典的值（value）。

【示例32】　将Excel销售数据转换为字典。 \04\32）
使用to_dict()方法将按“宝贝标题”分组统计后的部分数据转换为字典，程序代码如下：







​                           图4.35　DataFrame转换为字典

### 4.5.4　DataFrame转换为列表

DataFrame转换为列表主要使用DataFrame对象的tolist()方法。

【示例33】　将电商数据转换为列表。 \04\33）






### 4.5.5　DataFrame转换为元组

DataFrame转换为元组，首先通过循环语句按行读取DataFrame数据，然后使用元组函数tuple()将其转换为元组。

【示例34】　将Excel数据转换为元组。 \04\34）
将Excel表中的人物关系部分数据转换成元组，程序代码如下：





​                            图4.37　DataFrame转换为元组

### 4.5.6　Excel转换为HTML网页格式

日常工作中，有时会涉及财务数据的处理，而Excel应用最为广泛，但是对于展示数据来说，Excel并不友好，如果你想用其他格式的文件来向用户展示，那么，HTML网页格式是不错的选择。首先使用read_excel()方法导入Excel文件，然后使用to_html()方法将DataFrame数据导出为HTML格式，这样便实现了Excel转换为HTML格式。


程序代码如下：

01 import pandas as pd
02 df=pd.read_excel('mrbooks.xls')
03 df.to_html('mrbook.html',header = True,index = False)

## 4.6　数据合并

DataFrame数据合并主要使用merge()方法和concat()方法。

### 4.6.1　数据合并（merge()方法）

Pandas模块的merge()方法是按照两个DataFrame对象列名相同的列进行连接合并，两个DataFrame对象必须具有同名的列。merge()方法的语法如下：

pandas.merge(right,how='inner',on=None,left_on=None,right_on=None,left_index=False,right_index=False,sort=
False,suffixes=('_x','_y'),copy=True,indicator=False,validate=None)
参数说明：　

right：合并对象，DataFrame对象或Series对象。　

how：合并类型，参数值可以是left（左合并）、right（右合并）、outer（外部合并）或inner（内部合并），默认值为inner。各个值的说明如下。　

​		left：只使用来自左数据集的键，类似于SQL左外部联接，保留键的顺序。　

​		right：只使用来自右数据集的键，类似于SQL右外部联接，保留键的顺序。　

​		outer：使用来自两个数据集的键，类似于SQL外部联接，按字典顺序对键进行排序。　

​		inner：使用来自两个数据集的键的交集，类似于SQL内部连接，保持左键的顺序。

on：标签、列表或数组，默认值为None。DataFrame对象连接的列或索引级别名称。也可以是DataFrame对象长度的数组或数组列表。

left_on：标签、列表或数组，默认值为None。要连接的左数据集的列或索引级名称，也可以是左数据集长度的数组或数组列表。　

right_on：标签、列表或数组，默认值为None。要连接的右数据集的列或索引级名称，也可以是右数据集长度的数组或数组列表。　left_index：布尔型，默认值为False。使用左数据集的索引作为连接键。如果是多重索引，则其他数据中的键数（索引或列数）必须匹配索引级别数。

right_index：布尔型，默认值为False，使用右数据集的索引作为连接键。　

sort：布尔型，默认值为False，在合并结果中按字典顺序对连接键进行排序。如果值为False，则连接键的顺序取决于连接类型how参数。　

suffixes：元组类型，默认值为('_x','_y')。当左侧数据集和右侧数据集的列名相同时，数据合并后列名将带上“_x”和“_y”后缀。　

copy：是否复制数据，默认值为True。如果值为False，则不复制数据。　

indicator：布尔型或字符串，默认值为False。如果值为True，则添加一个列以输出名为_Merge的DataFrame对象，其中包含每一行的信息。如果是字符串，将向输出的DataFrame对象中添加包含每一行信息的列，并将列命名为字符型的值。　

validate：字符串，检查合并数据是否为指定类型。可选参数，其值说明如下。　one_to_one或“1:1”：检查合并键在左、右数据集中是否都是唯一的。　one_to_many或“1:m”：检查合并键在左数据集中是否唯一。　many_to_one或“m:1”：检查合并键在右数据集中是否唯一。　many_to_many或“m:m”：允许，但不检查。　

返回值：DataFrame对象，两个合并对象的数据集。

#### 1．常规合并



运行程序，控制台输出结果如图4.40所示。

【示例37】　通过索引合并数据。 \04\37）
如果通过索引列合并，则需要设置right_index参数和left_index参数值为True。例如，上述举例，通过列索引合并，主要代码如下：

01 df_merge=pd.merge(df1,df2,right_index=True,left_index=True)
02 print(df_merge)
运行程序，控制台输出结果如图4.41所示。





【示例38】　对合并数据去重。 \04\38）
从图4.41中的运行结果得知：数据中存在重复列（如编号），如果不想要重复列，可以设置按指定列和列索引合并数据，主要代码如下：

df_merge=pd.merge(df1,df2,on='编号',left_index=True,right_index=True)

还可以通过how参数解决这一问题。例如，设置该参数值为left，就是让df1保留所有的行列数据，df2则根据df1的行列进行补全，主要代码如下：

df_merge=pd.merge(df1,df2,on='编号',how='left')
运行程序，控制台输出结果如图4.42所示。





#### 2．多对一的数据合并

多对一是指两个数据集（df1、df2）的共有列中的数据不是一对一的关系，例如，df1中的“编号”是唯一的，而df2中的“编号”有重复的编号，类似这种就是多对一的关系，示意图如图4.43所示。【示例39】　根据共有列进行合并数据。 \04\39）
根据共有列中的数据进行合并，df2根据df1的行列进行补全，程序代码如下：



### 4.6.2　数据合并（concat()方法）

concat()方法可以根据不同的方式将数据合并，语法如下：

pandas.concat(objs,axis=0,join='outer',ignore_index: bool = False, keys=None, levels=None, names=None,
verify_integrity: bool = False, sort: bool = False, copy: bool = True)
参数说明：　

objs：Series、DataFrame或Panel对象的序列或映射。如果传递一个字典，则排序的键将用作键参数。　

axis：axis=1表示行，axis=0表示列。默认值为0。　

join：值为inner（内连接）或outer（外连连接），处理其他轴上的索引方式。默认值为outer。　

ignore_index：布尔值，默认值为False，保留索引，索引值为0，…，n-1。如果值为True，则忽略索引。　

keys：序列，默认值为None。使用传递的键作为最外层构建层次索引。如果为多索引，应该使用元组。　

levels：序列列表，默认值为None。用于构建MultiIndex的特定级别（唯一值）；否则，它们将从键推断。　

names：list列表，默认值为None。结果层次索引中的级别的名称。　

verify_integrity：布尔值，默认值为False。检查新连接的轴是否包含重复项。　

sort：布尔值，默认值为True（1.0.0以后版本默认值为False，即不排序）。如果连接为外连接（join='outer'），则对未对齐的非连接轴进行排序；如果连接为内连接（join='inner'），则该参数不起作用。

copy：是否复制数据，默认值为True，如果值为False，则不复制数据。

下面介绍concat()方法不同的合并方式，其中dfs代表合并后的DataFrame对象，df1、df2等代表单个DataFrame对象，result代表合并后的结果（DataFrame对象）。

#### 1．相同字段的表首尾相接

表结构相同的数据将直接合并，表首尾相接，主要代码如下：

01  dfs= [df1, df2, df3]
02  result = pd.concat(dfs)
例如，表df1、df2和df3结构相同，如图4.47所示。合并后的效果如图4.48所示。如果想要在合并数据时标记源数据来自哪张表，则需要在代码中加入参数keys，例如表名分别为“1月”“2月”“3月”，合并后的效果如图4.49所示。





​                        图4.49　合并后带标记（月份）的效果
主要代码如下：

result = pd.concat(dfs, keys=['1月', '2月', '3月'])

#### 2．横向表合并（行对齐）

当合并的数据列名称不一致时，可以设置参数axis=1，concat()方法将按行对齐，然后将不同列名的两组数据进行合并，缺失的数据用NaN填充，df1和df4合并前后效果如图4.50和图4.51所示。



​                        图4.50　横向表合并前

​                            图4.51　横向表合并后
主要代码如下：

result = pd.concat([df1, df4], axis=1)

#### 3．交叉合并

交叉合并，需要在代码中加上join参数，如果值为inner，结果是两张表的交集；如果值为outer，结果是两张表的并集。例如两张表交集，表df1和df4合并前后的效果如图4.52和图4.53所示。



​                                       图4.53　交叉合并后
主要代码如下：

result = pd.concat([df1, df4], axis=1, join='inner')

#### 4．指定表对齐数据（行对齐）

如果指定参数join_axes，就可以指定根据哪张表来对齐数据。例如，根据df4对齐数据，就会保留表df4的数据，然后将表df1的数据与之合并，行数不变，合并前后的效果与如图4.54和图4.55所示。


主要代码如下：

result = pd.concat([df1, df4], axis=1, join_axes=[df4.index])

## 4.7　数据导出

### 4.7.1　导出为.xlsx文件

导出数据为Excel，主要使用DataFrame对象的to_excel()方法，语法如下：

DataFrame.to_excel(excel_writer,sheet_name='Sheet1',na_rep='',float_format=None,columns=None,header=True,
index=True,index_label=None,startrow=0,startcol=0,engine=None,merge_cells=True, encoding=None, inf_rep='inf',
verbose=True, freeze_panes=None)
参数说明：　

excel_writer：字符串或ExcelWriter对象。　

sheet_name：字符串，默认值为Sheet1，包含DataFrame的表的名称。　

na_rep：字符串，默认值为' '。缺失数据的表示方式。　

float_format：字符串，默认值为None，格式化浮点数的字符串。　

columns：序列，可选参数，要编辑的列。　

header：布尔型或字符串列表，默认值为True。列名称，如果给定字符串列表，则表示它是列名称的别名。　

index：布尔型，默认值为True，行名（索引）。　

index_label：字符串或序列，默认值为None。如果需要，可以使用索引列的列标签；如果没有给出，标题和索引为True，则使用索引名称；如果数据文件使用多索引，则需使用序列。

startrow：指定从哪一行开始写入数据。　

startcol：指定从哪一列开始写入数据。　

engine：字符串，默认值为None，指定要使用的写引擎，如openpyxl或xlsxwriter。也可以通过io.excel.xlsx.writer、io.excel.xls.writer和io.excel.xlsm.writer进行设置。　

merge_cells：布尔型，默认值为True。　

encoding：指定Excel文件的编码方式，默认值为None。　

inf_rep：字符串，默认值为“正”，表示无穷大。　

verbose：布尔型，默认值为True。在错误日志中显示更多信息。　freeze_panes：整数的元组，长度2，默认值为None。指定要冻结的行列。

【示例41】　将处理后的数据导出为Excel文件。 \04\41）
将数据合并后的结果导出为Excel文件，主要代码如下：

df_merge.to_excel('merge.xlsx')
运行程序，数据将导出为Excel文件，如图4.56所示。



df1.to_excel('df1.xlsx',sheet_name='df1')

### 4.7.2　导出为.csv文件

导出数据为.csv文件，主要使用DataFrame对象的to_csv()方法，语法如下：



path_or_buf：要保存的路径及文件名。　

sep：分隔符，默认值为","。　

na_rep：指定空值的输出方式，默认值为空字符串。　

float_format：浮点数的输出格式，要用双引号括起来。　

columns：指定要导出的列，用列名列表表示，默认值为None。　header：是否输出列名，默认值为True。　

index：是否输出索引，默认值为True。　

index_label：索引列的列名，默认值为None。　

mode：Python写入模式，默认值为w。　

encoding：编码方式，默认值为utf-8。　

compression：压缩模式，默认值为infer。　

quoting：导出.csv文件是否用引号，默认值为0，表示不加双引号；如果值为1，则每个字段都会加上引号，数值也会被当作字符串看待。

quotechar：引用字符，当quoting=1时可以指定引号字符为双引号（" "）或单引号（' '）。　

line_terminator：换行符，默认值为\n。

chunksize：一次写入.csv文件的行数，当DataFrame对象数据特别大时需要分批写入。　

date_format：日期输出格式。　

doublequote：是否添加双引用符，默认值为True。　

escapechar：设置转义字符。　

decimal：可识别十进制分隔符的字符。　

errors：指定如何处理编码和解码错误，默认值为strict（严格的）。

【示例42】　将处理后的数据导出为.csv文件。 \04\42）
下面介绍to_csv()方法常用功能，举例如下，df为DataFrame对象。
（1）相对位置，保存在程序所在路径下，代码如下：

df.to_csv('Result.csv')
（2）绝对位置，代码如下：

df.to_csv('d:\Result.csv')
（3）分隔符。使用问号（？）分隔符分隔需要保存的数据，代码如下：

df.to_csv('Result.csv',sep='?')``
（4）替换空值，缺失值保存为NA，代码如下：

df.to_csv('Result1.csv',na_rep='NA')
（5）格式化数据，保留两位小数，代码如下：

df.to_csv('Result1.csv',float_format='%.2f')
（6）保留某列数据，保存索引列和name列，代码如下：

df.to_csv('Result.csv',columns=['name'])
（7）是否保留列名，不保留列名，代码如下：

df.to_csv('Result.csv',header=False)
（8）是否保留行索引，不保留行索引，代码如下：

df.to_csv('Result.csv',index=False)

### 4.7.3　导出多个Sheet

导出多个Sheet，应首先使用pd.ExcelWriter()方法打开一个Excel文件，然后再使用to_excel()方法导出指定的Sheet。



## 

### 4.8.1　DataFrame的日期数据转换

日常工作中，有一个非常麻烦的事情就是日期的格式可以有很多种表达，我们看到同样是2020年2月14日，可以有很多种格式，如图4.57所示。那么，我们需要先将这些格式统一后才能进行后续的工作。Pandas提供了to_datetime()方法可以帮助我们解决这一问题。
to_datetime()方法可以用来批量处理日期数据转换，对于处理大数据非常实用和方便，它可以将日期数据转换成你需要的各种格式。例如，将2/14/20和14-2-2020转换为日期格式2020-02-14。to_datetime()方法的语法如下：

pandas.to_datetime(arg,errors='ignore',dayfirst=False,yearfirst=False,utc=None,box=True,format=None,exact=
True,unit=None,infer_datetime_format=False,origin='unix',cache=False)
参数说明：　

arg：字符串、日期时间、字符串数组。　

errors：值为ignore、raise或coerce，具体说明如下，默认值为ignore，即忽略错误。　

ignore：无效的解析将返回原值。　

raise：无效的解析将引发异常。　

coerce：无效的解析将被设置为NaT，即无法转换为日期的数据将被转换为NaT。　

dayfirst：第一个为天，布尔型，默认值为False。例如02/09/2020，如果值为True，则解析日期的第一个为天，即2020-09-02；如果值为False，则解析日期与原日期一致，即2020-02-09。　

yearfirst：第一个为年，布尔型，默认值为False。例如14-Feb-20，如果值为True，则解析日期的第一个为年，即2014-02-20；如果值为False，则解析日期与原日期一致，即2020-02-14。　

utc：默认值为None。返回utc即协调世界时间。　

box：布尔值，默认值为True，如果值为True，则返回DatetimeIndex；如果值为False，则返回ndarray。　

format：格式化显示时间的格式。字符串，默认值为None。　

exact：布尔值，默认值为True。如果为True，则要求格式完全匹配；如果为False，则允许格式与目标字符串中的任何位置匹配。　

unit：默认值为None，参数的单位（D、s、、ms、μs、ns）表示时间的单位。　

infer_datetime_format：默认值为False。如果没有格式，则尝试根据第一个日期时间字符串推断格式。　

origin：默认值为unix。定义参考日期。数值将被解析为单位数。　

cache：默认值为False。如果值为True，则使用唯一、转换日期的缓存应用日期时间转换。在解析重复日期字符串，特别是带有时区偏移的字符串时，可能会产生明显的加速。只有在至少有50个值时才使用缓存。越界值的存在将使缓存不可用，并可能减慢解析速度。　

返回值：日期时间。







​                                        图4.59　日期组合

### 4.8.2　dt对象

dt对象是Series对象中用于获取日期属性的一个访问器对象，通过它可以获取日期中的年、月、日、星期数、季节等，还可以判断日期是否处在年底。语法如下：

  Series.dt()
参数说明：　

返回值：返回与原始系列相同的索引系列。如果Series不包含类日期值，则引发错误。　

dt对象提供了year、month、day、dayofweek、dayofyear、is_leap_year、quarter、weekday_name等属性和方法。

例如，year可以获取“年”、month可以获取“月”、quarter可以直接得到每个日期分别是第几个季度，weekday_name可以直接得到每个日期对应的是周几。

【示例46】　获取日期中的年、月、日、星期数等。 \04\46）
使用dt对象获取日期中的年、月、日、星期数、季节等。
（1）获取年、月、日，代码如下：

df['年'],df['月'],df['日']=df['日期'].dt.year,df['日期'].dt.month,df['日期'].dt.day
（2）从日期判断出所处星期数，代码如下：

df['星期几']=df['日期'].dt.day_name()
（3）从日期判断所处季度，代码如下：

df['季度']=df['日期'].dt.quarter
（4）从日期判断是否为年底最后一天，代码如下：

df['是否年底']=df['日期'].dt.is_year_end
运行程序，控制台输出结果如图4.60所示。

​                               图4.60　dt对象日期转换

### 4.8.3　获取日期区间的数据

获取日期区间的数据的方法是直接在DataFrame对象中输入日期或日期区间，但前提必须设置日期为索引，举例如下。　

获取2018年的数据。

df1['2018']　

获取2017—2018年的数据。

df1['2017':'2018']　

获取某月（2018年7月）的数据。

df1['2018-07']　

获取具体某天（2018年5月6日）的数据。

df1['2018-05-06':'2018-05-06']

### 4.8.4　按不同时期统计并显示数据

#### 1．按时期统计数据

按时期统计数据主要通过DataFrame对象的resample()方法结合数据计算函数实现。resample()方法主要应用于时间序列频率转换和重采样，它可以从日期中获取年、月、日、星期、季节等，结合数据计算函数就可以实现按年、月、日、星期或季度等不同时期统计数据。举例如下所示。
（1）按年统计数据，代码如下：

df1=df1.resample('AS').sum()
（2）按季度统计数据，代码如下：

df2.resample('Q').sum()
（3）按月度统计数据，代码如下：

df1.resample('M').sum()
（4）按星期统计数据，代码如下：

df1.resample('W').sum()
（5）按天统计数据，代码如下：

df1.resample('D').sum()





完整错误描述：
TypeError: Only valid with DatetimeIndex, TimedeltaIndex or PeriodIndex, but got an instance of'Index'
出现上述错误，是由于**resample()函数要求索引必须为日期型**。
解决方法：将数据的索引转换为datetime类型，主要代码如下：

df1.index = pd.to_datetime(df1.index)

#### 2．按时期显示数据

DataFrame对象的to_period()方法可以将时间戳转换为时期，从而实现按时期显示数据，前提是日期必须设置为索引。语法如下：

DataFrame.to_period(freq=None, axis=0, copy=True)
参数说明：　

freq：字符串，周期索引的频率，默认值为None。　

axis：行列索引，axis=0表示行索引，axis=1表示列索引。默认值为0，即表示行索引。　

copy：是否复制数据，默认值为True，如果值为False，则不复制数据。　返回值：带周期索引的时间序列。

【示例48】　从日期中获取不同的时期。 \04\48）
从日期中获取不同的时期，主要代码如下：

![image-20211020052452293](E:\文档\第四章-Pandas统计分析.assets\image-20211020052452293.png)

#### 3．按时期统计并显示数据

（1）按年统计并显示数据，代码如下：

df2.resample('AS').sum().to_period('A')
控制台输出结果如图4.63所示。
（2）按季度统计并显示数据，代码如下：

Q_df=df2.resample('Q').sum().to_period('Q')


（3）按月统计并显示数据，代码如下：

df2.resample('M').sum().to_period('M')
控制台输出结果如图4.65所示。
（4）按星期统计并显示数据（前5条数据），代码如下：

df2.resample('W').sum().to_period('W').head()

## 4.9　时间序列

### 4.9.1　重采样（Resample()方法）

通过前面的学习，我们学会了如何生成不同频率的时间索引，按小时、按天、按周、按月等，如果想对数据做不同频率的转换，该怎么办？在Pandas中对时间序列的频率的调整称为重新采样，即将时间序列从一个频率转换到另一个频率的处理过程。例如，每天一个频率转换为每5天一个频率，如图4.67所示。

​                                       图4.67　时间频率
重采样主要使用resample()方法，该方法用于对常规时间序列重新采样和频率转换，包括降采样和升采样两种。首先了解下resample()方法，语法如下：

DataFrame.resample(rule,how=None,axis=0,fill_method=None,closed=None,label=None,convention='start',kind=
None,loffset=None,limit=None,base=0,on=None,level=None)
参数说明：　

rule：字符串，偏移量表示目标字符串或对象转换。　

how：用于产生聚合值的函数名或数组函数。例如mean、ohlc和np.max等，默认值为mean，其他常用的值为first、last、median、max和min。　

axis：整型，表示行列，axis=0表示列，axis=1表示行。默认值为0，即表示列。　fill_method：升采样时所使用的填充方法，ffill()方法（用前值填充）或bfill()方法（用后值填充），默认值为None。　

closed：降采样时，时间区间的开和闭，与数学里区间的概念一样，其值为right或left，right表示左开右闭（即左边值不包括在内），left表示左闭右开（即右边值不包括在内），默认值为right左开右闭。　

label：降采样时，如何设置聚合值的标签。例如，10:30—10:35会被标记成10:30还是10:35，默认值为None。　

convention：当重采样时，将低频率转换到高频率所采用的约定，其值为start或end，默认值为start。　

kind：聚合到时期（period）或时间戳（timestamp），默认聚合到时间序列的索引类型，默认值为None。　

loffset：聚合标签的时间校正值，默认值为None。例如，-1s或Second(-1)用于将聚合标签调早1秒。　

limit：向前或向后填充时，允许填充的最大时期数，默认值为None。

　base：整型，默认值为0。对于均匀细分1天的频率，聚合间隔的“原点”。例如，对于5min频率，base的范围可以是0～4。　on：字符串，可选参数，默认值为None。对DataFrame对象使用列代替索引进行重新采样。列必须与日期时间类似。　

level：字符串或整型，可选参数，默认值为None。用于多索引，重新采样的级别名称或级别编号，级别必须与日期时间类似。　

返回值：重新采样对象。

​                          图4.68　时间序列转换程序代码如下：

01  import pandas as pd
02  index = pd.date_range('02/02/2020', periods=9, freq='T')

03  series = pd.Series(range(9), index=index)
04  print(series)
05  print(series.resample('3T').sum())

### 4.9.2　降采样处理

降采样是周期由高频率转向低频率。例如，将5min股票交易数据转换为日交易，按天统计的销售数据转换为按周统计。
数据降采样会涉及数据的聚合。例如，天数据变成周数据，那么就要对1周7天的数据进行聚合，聚合的方式主要包括求和、求均值等。例如，淘宝店铺每天销售数据（部分数据），如图4.69所示。

【示例50】　按周统计销售数据。 \04\50）
使用resample()方法来做降采样处理，频率为“周”，也就是将上述销售数据处理为每周（每7天）求和一次数据，程序代码如下：

01 import pandas as pd
02 df=pd.read_excel('time.xls')
03 df1 = df.set_index('订单付款时间')  #设置“订单付款时间”为索引
04 print(df1.resample('W').sum().head())
运行程序，控制台输出结果如图4.70所示。
在参数说明中，我们列出了closed参数的解释，如果把closed参数值设置为left，结果如图4.71所示。

​              图4.69　淘宝店铺每天销售数据（部分数据）

​                                       图4.70　周数据统计1



​                              图4.71　周数据统计2

### 4.9.3　升采样处理

​	升采样是周期由低频率转向高频率。将数据从低频率转换到高频率时，就不需要聚合了，将其重采样到日频率，默认会引入缺失值。
例如，原来是按周统计的数据，现在变成按天统计。升采样会涉及数据的填充，根据填充的方法不同，填充的数据也不同。下面介绍3种填充方法。　不填充。空值用NaN代替，使用asfreq()方法。　用前值填充。用前面的值填充空值，使用ffill()方法或者pad()方法。为了方便记忆，ffill()方法可以使用它的第一个字母“f”代替，代表forward，向前的意思。　用后值填充，使用bfill()方法，可以使用字母“b”代替，代表back，向后的意思。

【示例51】　每6小时统计一次数据。 \04\51）
下面创建一个时间序列，起始日期是2020-02-02，一共两天，每天对应的数值分别是1和2，通过升采样处理为每6小时统计一次数据，空值以不同的方式填充，程序代码如下：

01  import pandas as pd
02  import numpy as np
03  rng = pd.date_range('20200202', periods=2)
05  s1_6h_asfreq = s1.resample('6H').asfreq()

06  print(s1_6h_asfreq)
07  s1_6h_pad = s1.resample('6H').pad()
08  print(s1_6h_pad)
09  s1_6h_ffill = s1.resample('6H').ffill()
10  print(s1_6h_ffill)
11  s1_6h_bfill = s1.resample('6H').bfill()
12  print(s1_6h_bfill)
运行程序，控制台输出结果如图4.72所示。



​                          图4.72　6小时数据统计

### 4.9.4　时间序列数据汇总（ohlc()函数）

在金融领域，经常会看到开盘（open）、收盘（close）、最高价（high）和最低价（low）数据，而在Pandas中经过重新采样的数据也可以实现这样的结果，通过调用ohlc()函数得到数据汇总结果，即开始值（open）、结束值（close）、最高值（high）和最低值（low）。ohlc()函数的语法如下：

resample.ohlc()
ohlc()函数返回DataFrame对象，每组数据的open（开）、high（高）、low（低）和close（关）值。

【示例52】　统计数据的open、high、low和close值。 \04\52）
下面是一组5分钟的时间序列，通过ohlc()函数获取该时间序列中每组时间的开始值、最高值、最低值和结束值，程序代码如下：

01  import pandas as pd
02  import numpy as np
03  rng = pd.date_range('2/2/2020',periods=12,freq='T')
04  s1 = pd.Series(np.arange(12),index=rng)
05  print(s1.resample('5min').ohlc())
运行程序，控制台输出结果如图4.73所示。

​                          图4.73　时间序列数据汇总

### 4.9.5　移动窗口数据计算（rolling()函数）

通过重采样可以得到想要的任何频率的数据，但是这些数据也是一个时点的数据，那么就存在这样一个问题：时点的数据波动较大，某一点的数据就不能很好地表现它本身的特性，于是就有了“移动窗口”的概念，简单地说，为了提升数据的可靠性，将某个点的取值扩大到包含这个点的一段区间，用区间来进行判断，这个区间就是窗口。
下面举例说明，图4.74显示了移动窗口数据示意图，其中时间序列代表1号到15号每天的销量数据，接下来以3天为一个窗口，将该窗口从左至右依次移动，统计出3天的平均值作为这个点的值，如3号的销量是1号、2号和3号的平均值。



通过上述示意图相信您已经理解了移动窗口，在Pandas中可以通过rolling()函数实现移动窗口数据的计算，语法如下：

DataFrame.rolling(window, min_periods=None, center=False, win_type=None, on=None, axis=0, closed=None)

参数说明：　

window：时间窗口的大小，有两种形式，即int或offset。如果使用int，则数值表示计算统计量的观测值的数量，即向前几个数据；如果使用offset，则表示时间窗口的大小。　

min_periods：每个窗口最少包含的观测值数量，小于这个值的窗口结果为NA。值可以是int，默认值为None。offset情况下，默认值为1。

center：把窗口的标签设置为居中。布尔型，默认值为False，居右。

win_type：窗口的类型。截取窗的各种函数。字符串类型，默认值为None。　

on：可选参数。对于DataFrame对象，是指定要计算移动窗口的列，值为列名。　

axis：整型，axis=0表示列，axis=1表示行。默认值为0，即对列进行计算。　

closed：定义区间的开闭，支持int类型的窗口。对于offset类型默认是左开右闭（默认值为right）。可以根据情况指定left。　

返回值：为特定操作而生成的窗口或移动窗口子类。

【示例53】　创建淘宝每日销量数据。 \04\53）
首先创建一组淘宝每日销量数据，程序代码如下：

01  import pandas as pd
02  index=pd.date_range('20200201','20200215')
03  data=[3,6,7,4,2,1,3,8,9,10,12,15,13,22,14]
04  s1_data=pd.Series(data,index=index)
05  print(s1_data)
运行程序，控制台输出结果如图4.75所示。

【示例54】　使用rolling()函数计算3天的均值。 \04\54）

下面使用rolling()函数计算2020-02-01至2020-02-15中每3天的均值，窗口个数为3，代码如下：

s1_data.rolling(3).mean()
运行程序，看下rolling()函数是如何计算的？在图4.76中，当窗口开始移动时，第一个时间点2020-02-01和第二个时间点2020-02-02的数值为空，这是因为窗口个数为3，它们前面有空数据，所以均值为空；而到第三个时间点2020-02-03时，它前面的数据是2020-02-01至

​                       图4.76　2020-02-01至2020-02-15移动窗口均值1

【示例55】　用当天的数据代表窗口数据。 \04\55）
在计算第一个时间点2020-02-01的窗口数据时，虽然数据不够窗口长度3，但是至少有当天的数据，那么能否用当天的数据代表窗口数据呢？答案是肯定的，通过设置min_periods参数即可，它表示窗口最少包含的观测值，小于这个值的窗口长度显示为空，等于或大于时都有值，主要代码如下：

s1_data.rolling(3,min_periods=1).mean()

运行程序，对比效果如图4.77所示。
上述举例，我们再扩展下，通过图表观察原始数据与移动窗口数据的平稳性，如图4.78所示。其中实线代表移动窗口数据，其走向更平稳，这也是学习移动窗口rolling()函数的原因。






## 4.10　综合应用

### 4.10.1　案例1：Excel多表合并

案例位置：资源包\MR\Code\04\example\01
在日常工作中，几乎我们每天都有大量的数据需要处理，桌面上总是布满密密麻麻的Excel表，这样看上去非常凌乱，其实我们完全可以将其中类别相同的Excel表合并到一起，这样不但不会丢失数据，而且还可以有效地分析数据。下面使用concat()方法将指定文件夹内的所有Excel表合并，程序代码如下：



### 4.10.2　案例2：股票行情数据分析

案例位置：资源包\MR\Code\04\example\02
股票数据包括开盘价、收盘价、最高价、最低价、成交量等多个指标。其中，收盘价是当日行情的标准，也是下一个交易日开盘价的依据，可以预测未来证券市场行情，因此当投资者对行情分析时，一般采用收盘价作为计算依据。
下面使用rolling()函数计算某股票20天、50天和200天的收盘价均值并生成走势图（也称K线图），如图4.79所示。





