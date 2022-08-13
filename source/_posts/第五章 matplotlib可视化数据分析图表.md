---
layout:
  - page
title:  第五章 matplotlib可视化数据分析图表
date: 2020-05-16 16:16:53
tags: 
   - [python]
   - [数据分析]
---
<br>
<!--more-->

​                                                                                                    图5.3　图表分类框架图

### 5.3　图表

数据分析图表有很多种，但每一种图表的绝大组成部分是基本相同的，一张完整的图表一般包括画布、图表标题、绘图区、数据系列、坐标轴、坐标轴标题、图例、文本标签、网格线等，如图5.4所示。







01 import matplotlib.pyplot as plt
02 plt.plot([1, 2, 3, 4,5])



01 import matplotlib.pyplot as plt
02 plt.plot([1, 2, 3, 4,5], [2, 5, 8, 12,18], 'ro')

### 5.5　图表的常用设置

本节主要介绍图表的常用设置，主要包括颜色设置、线条样式、标记样式、设置画布、坐标轴、添加文本标签、设置标题和图例、添加注释文本、调整图表与画布边缘间距，以及其他相关设置等。

### 5.5.1　基本绘图plot()函数

Matplotlib基本绘图主要使用plot()函数，语法如下：

matplotlib.pyplot.plot(x,y,format_string,**kwargs)
参数说明：　**

x：x轴数据。　

y：y轴数据。　

format_string：控制曲线格式的字符串，包括颜色、线条样式和标记样式。　

kwargs：键值参数，相当于一个字典，比如输入参数为(1,2,3,4,k,a=1,b=2,c=3)，*args=(1,2,3,4,k)，**kwargs={'a':'1,'b':2,'c':3}。





0～1的小数作为灰度值，例如0.5。　

{'b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'}，其中的一个颜色值。　

X11/CSS4规定中的颜色名称。　

Xkcd中指定的颜色名称，例如xkcd:sky blue。　

Tableau调色板中的颜色，例如{'tab:blue', 'tab:orange', 'tab:green', 'tab:red', 'tab:purple', 'tab:brown','tab:pink', 'tab:gray', 'tab:olive', 'tab:cyan'}。　

CN格式的颜色循环，对应的颜色设置代码如下：

01  from cycler import cycler
02  colors=['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd', '#8c564b', '#e377c2','#7f7f7f', '#bcbd22', '#17becf']
03  plt.rcParams['axes.prop_cycle'] = cycler(color=colors)




1	plt.rcParams[’axes.unicode_minus’] = False	字符显示
2	plt.rcParams[’font.sans-serif’] = ‘SimHei’	设置字体
线条样式：lines	
3	plt.rcParams[’lines.linestyle’] = ‘-.’	线条样式
4	plt.rcParams[’lines.linewidth’] = 3	线条宽度
5	plt.rcParams[’lines.color’] = ‘blue’	线条颜色
6	plt.rcParams[’lines.marker’] = None	默认标记
7	plt.rcParams[’lines.markersize’] = 6	标记大小
8	plt.rcParams[’lines.markeredgewidth’] = 0.5	标记附近的线宽
横、纵轴：xtick、ytick	
9	plt.rcParams[’xtick.labelsize’]	横轴字体大小
10	plt.rcParams[’ytick.labelsize’]	纵轴字体大小
11	plt.rcParams[’xtick.major.size’]	x轴最大刻度
12	plt.rcParams[’ytick.major.size’]	y轴最大刻度
figure中的子图：axes	
13	plt.rcParams[’axes.titlesize’]	子图的标题大小
14	plt.rcParams[’axes.labelsize’]	子图的标签大小
图像、图片：figure、savefig	
15	plt.rcParams[’figure.dpi’]	图像分辨率
16	plt.rcParams[’figure.figsize’]	图像显示大小
17	plt.rcParams[’savefig.dpi’]	图片像素





#### 2．线条样式

linestyle可选参数可以设置线条的样式，设置值如下，设置后的效果如图5.23所示。　“-”：实线，默认值。　“--”：双画线　“-.”：点画线。　“:”：虚线。



| 属性                         |                                                         描述 |
| ---------------------------- | -----------------------------------------------------------: |
| agg_filter                   | a filter function, which takes a (m, n, 3) float array and a dpi value, and returns a (m, n, 3) array |
| alpha                        |                                                float or None |
| animated                     |                                                         bool |
| antialiased or aa            |                                                         bool |
| clip_box                     |                                                         Bbox |
| clip_on                      |                                                         bool |
| clip_path                    |                           Patch or (Path, Transform) or None |
| color or c                   |                                                        color |
| contains                     |                                                      unknown |
| dash_capstyle                |                              {‘butt’, ‘round’, ‘projecting’} |
| dash_joinstyle               |                                  {‘miter’, ‘round’, ‘bevel’} |
| dashes                       |    sequence of floats (on/off ink in points) or (None, None) |
| data                         |                                (2, N) array or two 1D arrays |
| drawstyle or ds              | {‘default’, ‘steps’, ‘steps-pre’, ‘steps-mid’, ‘steps-post’}, default: ‘default’ |
| figure                       |                                                       Figure |
| fillstyle                    |           {‘full’, ‘left’, ‘right’, ‘bottom’, ‘top’, ‘none’} |
| gid                          |                                                          str |
| in_layout                    |                                                         bool |
| label                        |                                                       object |
| linestyle or ls              |           {’-’, ‘–’, ‘-.’, ‘:’, ‘’, (offset, on-off-seq), …} |
| linewidth or lw              |                                                        float |
| marker                       |                     marker style string, Path or MarkerStyle |
| markeredgecolor or mec       |                                                        color |
| markeredgewidth or mew       |                                                        float |
| markerfacecolor or mfc       |                                                        color |
| markerfacecoloralt or mfcalt |                                                        color |
| markersize or ms             |                                                        float |
| markevery                    | None or int or (int, int) or slice or List[int] or float or (float, float) or List[bool] |
| path_effects                 |                                           AbstractPathEffect |
| picker                       |                                                      unknown |
| pickradius                   |                                                        float |
| rasterized                   |                                                 bool or None |
| sketch_params                |             (scale: float, length: float, randomness: float) |
| snap                         |                                                 bool or None |
| solid_capstyle               |                              {‘butt’, ‘round’, ‘projecting’} |
| solid_joinstyle              |                                  {‘miter’, ‘round’, ‘bevel’} |
| transform                    |                              matplotlib.transforms.Transform |
| url                          |                                                          str |
| visible                      |                                                         bool |
| xdata                        |                                                     1D array |
| ydata                        |                                                     1D array |
| zorder                       |                                                        float |

#### 3．标记样式

marker可选参数可以设置标记样式，设置值如表5.2所示。

plt.plot(x,y,color='m',linestyle='-',marker='o',mfc='w')

markerfacecolor or mfc：填充颜色



### 

matpoltlib.pyplot.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None, frameon=True)
参数说明：　

num：图像编号或名称，数字为编号，字符串为名称，可以通过该参数激活不同的画布。　

figsize：指定画布的宽和高，单位为英寸。　

dpi：指定绘图对象的分辨率，即每英寸多少个像素，默认值为80。像素越大画布越大。　

facecolor：背景颜色。　

edgecolor：边框颜色。

frameon：是否显示边框，默认值为True，绘制边框；如果为False，则不绘制边框。

【示例05】　自定义画布。（示例位置：资源包\MR\Code\05\05）
自定义一个5×3的黄色画布，主要代码如下：

01 import matplotlib.pyplot as plt
02 fig=plt.figure(figsize=(5,3),facecolor='yellow')
运行程序，输出结果如图5.25所示。



figsize=(5,3)，因为实际画布大小是500×300，所以这里不要输入太大的数字。



#### 1．x轴、y轴标题

设置x轴和y轴标题主要使用xlabel()函数和ylabel()函数。


（1）解决中文乱码问题，代码如下：

plt.rcParams['font.sans-serif']=['SimHei']        #解决中文乱码

（2）解决负号不显示问题，代码如下：

plt.rcParams['axes.unicode_minus'] = False       #解决负号不显示

#### 2．坐标轴刻度

用matplotlib画二维图像时，默认情况下的横坐标（x轴）和纵坐标（y轴）显示的值有时可能达不到我们的需求，需要借助xticks()函数和yticks()函数分别对x轴和y轴的值进行设置。
xticks()函数的语法如下：

xticks(locs, [labels], **kwargs)
参数说明：　

locs：数组，表示x轴上的刻度。例如，在“学生英语成绩分布图”中，x轴的刻度是2～14的偶数，如果想改变这个值，就可以通过locs参数设置。　

labels：也是数组，默认值和locs相同。locs表示位置，而labels则决定该位置上的标签，如果赋予labels空值，则x轴将只有刻度而不显示任何值。



plt.xticks(range(1,15,1))



运行程序，对比效果如图5.27和图5.28所示。
接下来，设置y轴刻度，主要使用yticks()函数。例如，设置体温为35.4～38，主要代码如下：

plt.yticks([35.4,35.6,35.8,36,36.2,36.4,36.6,36.8,37,37.2,37.4,37.6,37.8,38])

#### 3．坐标轴范围

坐标轴范围是指x轴和y轴的取值范围。设置坐标轴范围主要使用xlim()函数和ylim()函数。

【示例09】　为折线图设置坐标范围。（示例位置：资源包\MR\Code\05\09）
设置x轴（日期）范围为1～14，y轴（基础体温）范围为35～45，主要代码如下：

01  plt.xlim(1,14)
02  plt.ylim(35,45)

#### 4．网格线



plt.grid(color='0.5',linestyle='--',linewidth=1)




### 5.5.4　添加文本标签

绘图过程中，为了能够更清晰、直观地看到数据，有时需要给图表中指定的数据点添加文本标签。下面介绍细节之二——文本标签，主要使用**text()**函数，语法如下：

matplotlib.pyplot.text(x, y, s, fontdict=None, withdash=False, **kwargs)
参数说明：　**

x：x坐标轴的值。　

y：y坐标轴的值。　

s：字符串，注释内容。　

fontdict：字典，可选参数，默认值为None。用于重写默认文本属性。　

withdash：布尔型，默认值为False，创建一个TexWithDash实例，而不是Text实例。　

kwargs：关键字参数。这里指通用的绘图参数，如字体大小fontsize=12、垂直对齐方式horizontalalignment='center'（或简写为ha='center'）、水平对齐方式verticalalignment='center'（或简写为va='center'）。



01  for a,b  in zip(x,y):
02      plt.text(a,b+3,'%.1f'%b,ha = 'center',va = 'bottom',fontsize=9)

​                                                                                     图5.31　带文本标签的折线图
在本示例代码中，首先，x、y是x轴和y轴的值，它代表了折线图在坐标中的位置，通过for循环找到每一个x、y值相对应的坐标赋值给a、b，再使用plt.text在对应的数据点上添加文本标签，而for循环也保证了折线图中每一个数据点都有文本标签。其中，a,b+3表示每一个数据点（x值对应y值加3）的位置处添加文本标签；%.1f'%b是对y值进行的格式化处理，保留小数点1位；ha='center'、va='bottom'代表水平对齐、垂直对齐的方式，fontsize则是字体大小。

### 5.5.5　设置标题和图例

#### 1．图表标题

为图表设置标题主要使用title()函数，语法如下：

matplotlib.pyplot.title(label, fontdict=None, loc='center', pad=None, **kwargs)
参数说明：　

label：字符串，表示图表标题文本。　

fontdict：字典，用来设置标题字体的样式。如{'fontsize': 20,'fontweight':20,'va': 'bottom','ha':'center'}。　

loc：字符串，表示标题水平位置，参数值为center、left或right，分别表示水平居中、水平居左和水平居右，默认为水平居中。　

pad：浮点型，表示标题离图表顶部的距离，默认值为None。

**kwargs：关键字参数，可以设置一些其他文本属性。
例如，设置图表标题为“14天基础体温曲线图”，主要代码如下：

plt.title('14天基础体温曲线图',fontsize='18')

#### 2．图表图例

##### （1）自动显示图例

plt.legend()
（2）手动添加图例

plt.legend('基础体温')

注意
当手动添加图例时，有时会出现文本显示不全，解决方法是在文本后面加一个逗号（,），主要代码如下：

**plt.legend(('基础体温',))**
（3）设置图例显示位置
通过loc参数可以设置图例的显示位置，如在左下方显示，主要代码如下：

plt.legend(('基础体温',),loc='upper right',fontsize=10)
具体图例显示位置的设置如表5.3所示。



plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0)
下面来看下设置标题和图例后的“14天基础体温曲线图”，效果如图5.32所示。

### 5.5.6　添加注释




01 plt.annotate('最高体温', xy=(9,37.1), xytext=(10.5,37.1),

02               xycoords='data',
03               arrowprops=dict(facecolor='r', shrink=0.05))
下面介绍一下本示例中用到的几个主要参数。　

xy：被注释的坐标点，二维元组，如(x,y)。　

xytext：注释文本的坐标点（也就是本示例中箭头的位置），也是二维元组，默认与xy相同。　

xycoords：是被注释点的坐标系属性，设置值如表5.4所示。





### 5.5.8　其他设置

#### 1．坐标轴的刻度线

（1）设置4个方向的坐标轴上的刻度线是否显示，主要代码如下：

plt.tick_params(bottom=False,left=True,right=True,top=True)
（2）设置x轴和y轴的刻度线显示方向，其中in表示向内，out表示向外，inout表示在中间，默认刻度线向外，主要代码如下：

plt.rcParams['xtick.direction'] = 'in'         #x轴的刻度线向内显示
plt.rcParams['ytick.direction'] = 'in'         #y轴的刻度线向内显示

#### 2．坐标轴相关属性设置　

axis()：返回当前axes范围。　

axis(v)：通过输入v = [xmin, xmax, ymin, ymax]，设置x、y轴的取值范围。　

axis('off')：关闭坐标轴轴线及坐标轴标签。　

axis('equal')：使x、y轴长度一致。　

axis('scaled')：调整图框的尺寸（而不是改变坐标轴取值范围），使x、y轴长度一致。　

axis('tight')：改变x轴和y轴的限制，使所有数据被展示。如果所有的数据已经显示，它将移动到图形的中心而不修改（xmax～xmin）或（ymax～ymin）。　

axis('image')：缩放axis范围（limits），等同于对data缩放范围。　

axis('auto')：自动缩放。　

axis('normal')：不推荐使用。恢复默认状态，轴限的自动缩放以使数据显示在图表中。







​                                                                                               图5.36　多折线图
上述举例，用到了几个参数，下面进行说明。

mfc：标记的颜色。　

ms：标记的大小。　

mec：标记边框的颜色。　

alpha：透明度，设置该参数可以改变颜色的深浅。

### 5.6.2　绘制柱形图

matplotlib.pyplot.bar(x,height,width,bottom=None,*,align='center',data=None,**kwargs)
参数说明：　**

x：x轴数据。　

height：柱子的高度，也就是y轴数据。　

width：浮点型，柱子的宽度，默认值为0.8，可以指定固定值。　

bottom：标量或数组，可选参数，柱形图的y坐标，默认值为None。　

*：星号本身不是参数。星号表示其后面的参数为命名关键字参数，命名关键字参数必须传入参数名；否则程序会出现错误。　

align：对齐方式，如center（居中）和edge（边缘），默认值为center。　

data：data关键字参数。如果给定一个数据参数，所有位置和关键字参数将被替换。　

kwargs：关键字参数，其他可选参数，如color（颜色）、alpha（透明度）、label（每个柱子显示的标签）等。



01 import matplotlib.pyplot as plt
02 x=[1,2,3,4,5,6]

03 height=[10,20,30,40,50,60]
04 plt.bar(x,height)
运行程序，输出结果如图5.37所示。


bar()函数可以绘制出各种类型的柱形图，如基本柱形图、多柱形图、堆叠柱形图，只要将bar()函数的主要参数理解透彻，就会达到意想不到的效果。下面介绍几种常见的柱形图。





### 5.6.3　绘制直方图

直方图，又称质量分布图，由一系列高度不等的纵向条纹或线段表示数据分布的情况。一般用横轴表示数据类型，纵轴表示分布情况。直方图是数值数据分布的精确图形表示，是一个连续变量（定量变量）的概率分布的估计。
绘制直方图主要使用hist()函数，语法如下：

matplotlib.pyplot.hist(x,bins=None,range=None, density=None, bottom=None, histtype='bar', align='mid', log=
False, color=None, label=None, stacked=False, normed=None)
参数说明：　

x：数据集，最终的直方图将对数据集进行统计。　

bins：统计数据的区间分布。　

range：元组类型，显示的区间。　

density：布尔型，显示频率统计结果，默认值为None。设置值为False，不显示频率统计结果；设置值为True，则显示频率统计结果。需要注意，频率统计结果=区间数目/(总数×区间宽度)。　

histtype：可选参数，设置值为bar、barstacked、step或stepfilled，默认值为bar，推荐使用默认配置，其中step使用的是梯状，stepfilled则会对梯状内部进行填充，效果与bar类似。　

align：可选参数，控制柱状图的水平分布，设置值为left、mid或right，默认值为mid，其中，left或者right会有部分空白区域，推荐使用默认值。　

log：布尔型，默认值为False，即y坐标轴是否选择指数刻度。

stacked：布尔型，默认值为False，是否为堆积柱状图。

【示例16】　绘制简单直方图。（示例位置：资源包\MR\Code\05\16）
绘制简单直方图，程序代码如下：

01 import matplotlib.pyplot as plt
02 x=[22,87,5,43,56,73,55,54,11,20,51,5,79,31,27]
03 plt.hist(x, bins = [0,25,50,75,100])
运行程序，输出结果如图5.40所示。





### 5.6.4　绘制饼形图

饼形图常用来显示各个部分在整体中所占的比例。例如，在工作中如果遇到需要计算总费用或金额的各个部分构成比例的情况，一般通过各个部分与总额相除来计算，而且这种比例表示方法很抽象，而通过饼形图将直接显示各个组成部分所占比例，一目了然。
Matplotlib绘制饼形图主要使用pie()函数，语法如下：

matplotlib.pyplot.pie(x,explode=None,labels=None,colors=None,autopct=None,pctdistance=0.6,shadow=False,
labeldistance=1.1,startangle=None,radius=None,counterclock=True,wedgeprops=None,textprops=None,center=
(0, 0), frame=False, rotatelabels=False, hold=None, data=None)
参数说明：　

x：每一块饼图的比例，如果sum(x)>1会使用sum(x)归一化。　

explode：每一块饼图离中心的距离。　

labels：每一块饼图外侧显示的说明文字。　

autopct：设置饼图百分比，可以使用格式化字符串或format()函数。如'%1.1f '保留小数点前后1位。　

pctdistance：类似于labeldistance参数，指定百分比的位置刻度，默认值为0.6。　

shadow：在饼图下面画一个阴影，默认值为False，即不画阴影。　

labeldistance：标记的绘制位置，相对于半径的比例，默认值为1.1，如<1则绘制在饼图内侧。　

startangle：起始绘制角度，默认是从x轴正方向逆时针画起，如设置值为90则从y轴正方向画起。　

radius：饼图半径，默认值为1。　

counterclock：指定指针方向，布尔型，可选参数。默认值为True，表示逆时针；如果值为False，则表示顺时针。　

wedgeprops：字典类型，可选参数，默认值为None。字典传递给wedge对象，用来画一个饼图。例如wedgeprops={'linewidth':2}设置wedge线宽为2。　

textprops：设置标签和比例文字的格式，字典类型，可选参数，默认值为None。传递给text对象的字典参数。　

center：浮点类型的列表，可选参数，默认值为(0,0)，表示图表中心位置。　

frame：布尔型，可选参数，默认值为False，不显示轴框架（也就是网格）；如果值为True，则显示轴框架，与grid()函数配合使用。实际应用中建议使用默认设置，因为显示轴框架会干扰饼形图效果。　

rotatelabels：布尔型，可选参数，默认值为False；如果值为True，则旋转每个标签到指定的角度。



01 import matplotlib.pyplot as plt
02 x = [2,5,12,70,2,9]
03 plt.pie(x,autopct='%1.1f%%')
运行程序，输出结果如图5.42所示。

#### 



​                                                                                               图5.44　分裂饼形图
分裂饼形图主要通过设置explode参数实现，该参数用于设置饼图距中心的距离，我们需要将哪块饼图分裂出来，就设置它与中心的距离即可。例如，图5.43中有10块饼图，我们将占比最多的“广东省”分裂出来，如图5.44（a）所示。广东省在第一位，那么就设置第一位距中心的距离为0.1，其他为0，关键代码如下：

explode = (0.1,0,0,0,0,0,0,0,0,0)

#### 3．立体感带阴影的饼形图

立体感带阴影的饼形图看起来更美观，效果如图5.45所示。
立体感带阴影的饼形图主要通过shadow参数实现，设置该参数值为True即可，主要代码如下：

shadow=True

#### 4．环形图



​                                                                                                              图5.46　环形图
这里还是通过pie()函数实现，一个关键参数wedgeprops，字典类型，用于设置饼形图内、外边界的属性，如环的宽度，环边界颜色和宽度，主要代码如下：

wedgeprops = {'width': 0.4, 'edgecolor': 'k'}

#### 5．内嵌

​                                                                                             图5.47　内嵌环形图
绘制内嵌环形图需要注意以下3点。
（1）连续使用两次pie()函数。
（2）通过wedgeprops参数设置环形边界。
（3）通过radius参数设置不同的半径。
另外，由于图例内容比较长，为了使图例能够正常显示，图例代码中引入了两个主要参数，即frameon和bbox_to_anchor。其中，frameon参数设置图例有无边框；bbox_to_anchor参数设置图例位置，主要代码如下：

![image-20211022044933255](111111111111111111/image-20211022044933255.png)

### 5.6.5　散点图

散点图主要用来查看数据的分布情况或相关性，一般用在线性回归分析中，查看数据点在坐标系平面上的分布情况。散点图表示因变量随自变量而变化的大致趋势，据此可以选择合适的函数对数据点进行拟合。
散点图与折线图类似，也是一个个点构成的。但不同之处在于，散点图的各点之间不会按照前后关系以线条连接起来。
Matplotlib绘制散点图使用plot()函数和scatter()函数都可以实现，本节使用scatter()函数绘制散点图，scatter()函数专门用于绘制散点图，使用方式和plot()函数类似，区别在于前者具有更高的灵活性，可以单独控制每个散点与数据匹配，并让每个散点具有不同的属性。scatter()函数的语法如下：

matplotlib.pyplot.scatter(x,y,s=None,c=None,marker=None,cmap=None,norm=None,vmin=None,vmax=None,
alpha=None,linewidths=None,verts=None,edgecolors=None,data=None, **kwargs)
参数说明：　

x，y：数据。　

s：标记大小，以平方磅为单位的标记面积，设置值如下。　

​		数值标量：以相同的大小绘制所有标记。　

​		行或列向量：使每个标记具有不同的大小。x、y和sz中的相应元素确定每个标记的位置和面积。sz的长度必须等于x和y的长度。　

​		[]：使用36平方磅的默认面积。　

c：标记颜色，可选参数，默认标记颜色为蓝色。　

marker：标记样式，可选参数，默认值为'o'。　

cmap：颜色地图，可选参数，默认值为None。

norm：可选参数，默认值为None

vmin，vmax：标量，可选，默认值为None　

alpha：透明度，可选参数，0～1的数，表示透明度，默认值为None。　

linewidths：线宽，标记边缘的宽度，可选参数，默认值为None。　

verts：(x,y)的序列，可选参数，如果参数marker为None，这些顶点将用于构建标记。标记的中心位置为(0,0)。　

edgecolors：轮廓颜色，与参数c类似，可选参数，默认值为None。　

data：data关键字参数。如果给定一个数据参数，所有位置和关键字参数将被替换。　

**kwargs：关键字参数，其他可选参数。



01 import matplotlib.pyplot as plt
02 x=[1,2,3,4,5,6]
03 y=[19,24,37,43,55,68]
04 plt.scatter(x, y)
运行程序，输出结果如图5.48所示。



​                                                                              图5.49　销售收入与广告费散点图

### 5.6.6　绘制面积图

面积图用于体现数量随时间而变化的程度，也可用于引起人们对总值趋势的注意。例如，表示随时间而变化的利润的数据可以绘制在面积图中，以强调总利润。
Matplotlib绘制面积图主要使用stackplot()函数，语法如下：

matplotlib.pyplot.stackplot(x,*args,data=None,**kwargs)
参数说明：　**

x：x轴数据。　

*args：当传入的参数个数未知时使用*args。这里指y轴数据可以传入多个y轴。　

data：data关键字参数。如果给定一个数据参数，所有位置和关键字参数将被替换。　

kwargs：关键字参数，其他可选参数，如color（颜色）、alpha（透明度）等。







### 5.6.7　绘制热力图

热力图是通过密度函数进行可视化用于表示地图中点的密度的热图。它使人们能够独立于缩放因子感知点的密度。热力图可以显示不可点击区域发生的事情。利用热力图可以看数据表里多个特征两两的相似度。例如，以特殊高亮的形式显示访客热衷的页面区域和访客所在的地理区域的图示。热力图在网页分析、业务数据分析等其他领域也有较为广泛的应用。

【示例28】　绘制简单热力图。（示例位置：资源包\MR\Code\05\28）
热力图是数据分析的常用方法，通过色差、亮度来展示数据的差异，易于理解。下面绘制简单热力图，程序代码如下：

01 import matplotlib.pyplot as plt
02 X = [[1,2],[3,4],[5,6],[7,8],[9,10]]
03 plt.imshow(X)
运行程序，输出结果如图5.53所示。

​                                                                                              图5.53　简单热力图

上述代码中，plt.imshow(X)中传入的数组X=[[1,2],[3,4],[5,6],[7,8],[9,10]]为颜色的对应值，按照矩阵X进行颜色分布，如左上角颜色为深蓝，其对应值为1，右下角颜色为黄色，其对应值为10，具体如下：

[1,2]  [深蓝,蓝色]
[3,4]  [蓝绿,深绿]
[5,6]  [海藻绿,春绿色]
[7,8]  [绿色,浅绿色]
[9,10] [草绿色,黄色]







### 5.6.8　箱形图

箱形图又称箱线图、盒须图或盒式图，它是一种用作显示一组数据分散情况下的资料的统计图。因形状像箱子而得名。箱形图最大的优点**就是不受异常值的影响（异常值也称为离群值**），可以以一种相对稳定的方式描述数据的离散分布情况，因此在各种领域也经常被使用。另外，箱形图也常用于异常值的识别。Matplotlib绘制箱形图主要使用boxplot()函数，语法如下：

matplotlib.pyplot.boxplot(x,notch=None,sym=None,vert=None,whis=None,positions=None,widths=None,patch_
artist=None,meanline=None,showmeans=None,showcaps=None,showbox=None,showfliers=None,boxprops=None,
labels=None,flierprops=None,medianprops=None,meanprops=None,capprops=None,whiskerprops=None)
参数说明：　

x：指定要绘制箱形图的数据。　

notch：是否以凹口的形式展现箱形图，默认非凹口。　

sym：指定异常点的形状，默认为加号（+）显示。　

vert：是否需要将箱形图垂直摆放，默认垂直摆放。　

whis：指定上下限与上下四分位的距离，默认为1.5倍的四分位差。　

positions：指定箱形图的位置，默认为[0,1,2,…]。　

widths：指定箱形图的宽度，默认为0.5。　

patch_artist：是否填充箱体的颜色。　

meanline：是否用线的形式表示均值，默认用点来表示。　

showmeans：是否显示均值，默认不显示。　

showcaps：是否显示箱形图顶端和末端的两条线，默认显示。　

showbox：是否显示箱形图的箱体，默认显示。　

showfliers：是否显示异常值，默认显示。　

boxprops：设置箱体的属性，如边框色、填充色等。　

labels：为箱形图添加标签，类似于图例的作用。　

filerprops：设置异常值的属性，如异常点的形状、大小、填充色等。　

medianprops：设置中位数的属性，如线的类型、粗细等。　meanprops：设置均值的属性，如点的大小、颜色等。

capprops：设置箱形图顶端和末端线条的属性，如颜色、粗细等。　

whiskerprops：设置须的属性，如颜色、粗细、线的类型等。

【示例30】　绘制简单箱形图。（示例位置：资源包\MR\Code\05\30）
绘制简单箱形图，程序代码如下：

01  import matplotlib.pyplot as plt
02  x=[1,2,3,5,7,9]
03  plt.boxplot(x)
运行程序，输出结果如图5.55所示。

01 import matplotlib.pyplot as plt
02 x1=[1,2,3,5,7,9]
03 x2=[10,22,13,15,8,19]
04 x3=[18,31,18,19,14,29]
05 plt.boxplot([x1,x2,x3])
运行程序，输出结果如图5.56所示。



下四分位
		图5.57中的下四分位数指的是数据的25%分位点所对应的值（Q1）。计算分位数可以使用Pandas的quantile()函数。例如，Q1 = df['总消费'].quantile(q = 0.25)。　

中位数
		中位数即为数据的50%分位点所对应的值（Q2）。　

上四分位数
		上四分位数则为数据的75%分位点所对应的值（Q3）。　

上限
		**上限的计算公式为Q3+1.5(Q3-Q1)。**　

下限
		下限的计算公式为Q1-1.5(Q3-Q1)。其中，Q3-Q1表示四分位差。如果使用箱形图识别异常值，其判断标准是，当变量的数据值大于箱形图的上限或者小于箱线图的下限时，就可以将这样的数据判定为异常值。

​                                                                                          图5.60　异常值



​                                              

### 

Matplotlib可以实现在一张图上绘制多个子图表。Matplotlib提供了3种方法：一是subplot()函数；二是subplots()函数；三是add_subplot()函数，下面分别介绍。

#### 1．subplot()函数

subplot()函数直接指定划分方式和位置，它可以将一个绘图区域划分为n个子图，每个subplot()函数只能绘制一个子图。语法如下：

matplotlib.pyplot.subplot(*args,**kwargs)
参数说明：　**

*args：当传入的参数个数未知时使用*args。　

kwargs：关键字参数，其他可选参数。
例如，绘制一个2×3的区域，subplot(2,3,3)，将画布分成2行3列在第3个区域中绘制，用坐标表示如下：

(1,1),(1,2),(1,3)

(2,1),(2,2),(2,3)
如果行列的值都小于10，那么可以把它们缩写为一个整数，如subplot(233)。
另外，subplot()函数在指定的区域中创建一个轴对象，如果新创建的轴和之前所创建的轴重叠，那么，之前的轴将被删除。



上述举例，以下两个关键点一定要掌握。
**（1）每绘制一个子图表都要调用一次subplot()函数。**
**（2）绘图区域位置编号**。
subplot()函数的前面两个参数指定的是一个画布被分割成的行数和列数，后面一个参数则指的是当前绘制区域位置编号，编号规则是行优先。
例如，图5.64中有3个子图表，第1个子图表subplot(2,2,1)，即将画布分成2行2列，在第1个子图中绘制折线图；第2个子图表subplot(2,2,2)，将画布分成2行2列，在第2个子图中绘制散点图；第3个子图表subplot(2,1,2)，将画布分成2行1列，由于第1行已经占用了，所以在第2行也就是第3个子图中绘制柱形图。示意图如图5.65所示。



​                                                                                               图5.65　多个子图示意图
subplot()函数在画布中绘图时，每次都要调用它指定绘图区域非常麻烦，而subplots()函数则更直接，它会事先把画布区域分割好。下面介绍subplots()函数。

#### 2．subplots()函数

subplots()函数用于创建画布和子图，语法如下：

matplotlib.pyplot.subplots(nrows,ncols,sharex,sharey,squeeze,subplot_kw,gridspec_kw,**fig_kw)
参数说明：　

nrows和ncols：表示将画布分割成几行几列，例如，nrows=2、ncols=2表示将画布分割为2行2列，起始值均为0。当调用画布中的坐标轴时，ax[0,0]表示调用左上角的坐标，ax[1,1]表示调用右下角的坐标。　

sharex和sharey：布尔值或者值为“none”“all”“row”“col”，默认值为False。用于控制x或y轴之间的属性共享。具体参数值说明如下。　	

​		True或者“all”：表示x或y轴属性在所有子图中共享。　

​		False或者“none”：表示每个子图的x或y轴都是独立的部分。　

​		“row”：表示每个子图在一个x或y轴上共享行（row）。　

​		“col”：表示每个子图在一个x或y轴上共享列（column）　

squeeze：布尔值，默认值为True，额外的维度从返回的axes（轴）对象中挤出，对于n×1或1×n个子图，返回一个一维数组，对于n×m，n>1和m>1返回一个二维数组；如果值为False，则表示不进行挤压操作，返回一个元素为Axes实例的二维数组，即使它最终是1×1。　

subplot_kw：字典类型，可选参数。把字典的关键字传递给add_subplot()函数来创建每个子图。　

gridspec_kw：字典类型，可选参数。把字典的关键字传递给GridSpec()构造函数创建网格区域，然后将子图放在网格（grid）里。　**fig_kw：把所有详细的关键字参数传递给figure。

【示例37】　使用subplots()函数绘制多子图的空图表。（示例位置：资源包\MR\Code\05\37）
绘制一个2×3包含6个子图的空图表，使用subplots()函数只需3行代码。

01 import matplotlib.pyplot as plt
02 figure,axes=plt.subplots(2,3)
03 plt.show()
上述代码中，figure和axes是两个关键点。　

figure：绘制图表的画布。　

axes：坐标轴对象，可以理解为在figure（画布）上绘制坐标轴对象，它帮我们规划出了一个个科学作图的坐标轴系统。


#### 3．add_subplot()函数

【示例39】　使用add_subplot()函数绘制多子图图表。（示例位置：资源包\MR\Code\05\39）
add_subplot()函数也可以实现在一张图上绘制多个子图表，用法与subplot()函数基本相同，先来看下列一段代码：

01 import matplotlib.pyplot as plt
02 fig = plt.figure()

03 ax1 = fig.add_subplot(2,3,1)
04 ax2 = fig.add_subplot(2,3,2)
05 ax3 = fig.add_subplot(2,3,3)
06 ax4 = fig.add_subplot(2,3,4)
07 ax5 = fig.add_subplot(2,3,5)
08 ax6 = fig.add_subplot(2,3,6)
上述代码同样是绘制一个2×3包含6个子图的空图表。首先创建figure实例（画布），然后通过ax1 =fig.add_subplot(2,3,1)创建第1个子图表，返回Axes实例（坐标轴对象），第1个参数为行数，第2个参数为列数，第3个参数为子图表的位置。
以上用3种方法实现了在一张图上绘制多个子图表，3种方法各有所长。subplot()函数和add_subplot()函数比较灵活，定制化效果比较好，可以实现子图表在图中的各种布局（如一张图上可以随意摆放3个或5个图表）；而subplots()函数较为不灵活，但它可以用较少的代码实现绘制多个子图表。



### 5.6.11　图表的保存

实际工作中，有时需要将绘制的图表保存为图片放置到报告中。Matplotlib的savefig()函数可以实现这一功能，将图表保存为JPEG、TIFF或PNG格式的图片。
例如，保存之前绘制的折线图，主要代码如下：

plt.savefig('image.png')
需要注意的一个关键问题：保存代码必须在图表预览前，也就是plt.show()代码前；否则保存后的图片是白色，图表无法保存。
运行程序，图表被保存在程序所在路径下，名为image.png，如图5.68所示。

​                                                                                             图5.68　保存后的图表



## 5.7　综合应用

### 5.7.1　案例1：双y轴可视化数据分析图表的实现

案例位置：资源包\MR\Code\05\example\01
双y轴顾名思义就是两个y轴，其特点是通过双y轴可以看出发展情况的同时还可以看到其增长速度。对于产品而言，通过此图可以看到产品销量的同时还可以看到产品增长率，效果如图5.69所示。

​                                                                           图5.69　双y轴可视化数据分析图表
双y轴可视化数据分析图表的实现主要使用add_suplot()函数和twinx()函数。twinx()函数表示共享x轴，那么也就是一个x轴、两个y轴，程序代码如下：



