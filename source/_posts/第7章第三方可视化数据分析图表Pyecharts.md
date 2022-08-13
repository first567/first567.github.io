---
layout:
  - page
title:  第三方可视化数据分析图表Pyecharts
date: 2020-05-15 16:16:53
tags: 
   - [python]
   - [数据分析]
---
<br>
<!--more-->
# 第七章 第三方可视化数据分析图表Pyecharts

Echarts是一个由百度开源的数据可视化工具，而Python是一门适用于数据处理和数据分析的语言，为了适应Python的需求，Pyecharts诞生了。
本章以Pyecharts 1.7.1版本为主，介绍Pyecharts的安装、链式调用、Pyecharts图表的组成，以及如何绘制柱状图、折线图、面积图、饼形图、箱形图、散点图、词云图、热力图、水球图和日历图。此外，本章还通过综合应用介绍南丁格尔玫瑰图、双y轴可视化数据分析图表的实现，以及饼形图与环形图组合图表的实现。接下来，就让我们开启Pyecharts的旅程。

# 7.1　Pyecharts概述

## 7.1.1　Pyecharts简介

Pyecharts是一个用于生成Echarts图表的类库。Echarts是百度开源的一个数据可视化JS库。用Echarts生成的图可视化效果非常好，而Pyecharts则是专门为了与Python衔接，方便在Python中直接使用的可视化数据分析图表。使用Pyecharts可以生成独立的网页格式的图表，还可以在flask、django中直接使用，非常方便。
Pyecharts的图表类型非常多且效果非常漂亮，例如图7.1、图7.2和图7.3所示的线性闪烁图、仪表盘图和水球图。
Pyecharts的图表类型主要包括Bar（柱状图／条形图）、Boxplot（箱形图）、Funnel（漏斗图）、Gauge（仪表盘）、HeatMap（热力图）、Line（折线／面积图）、Line3D（3D折线图）、Liquid（水球图）、Map（地图）、Parallel（平行坐标系）、Pie（饼图）、Polar（极坐标系）、Radar（雷达图）、Scatter（散点图）和WordCloud（词云图）等。

![image-20211025093507338](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093507338.png)

​                                                                              图7.1　线性闪烁图

![image-20211025093610269](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093610269.png)

​                                                                                           图7.2　仪表盘图

![image-20211025093631679](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093631679.png)

​                                                                                                       图7.3　水球图

## 7.1.2　安装Pyecharts

在anaconda命令提示符窗口中安装Pyecharts库。在系统搜索框中输入anaconda prompt，单击Anaconda Prompt打开Anaconda Prompt命令提示符窗口，使用pip工具安装，命令如下：

pip install pyecharts==1.7.1
安装成功后，将提示安装成功的字样，如“Successfully installed pyecharts-1.7.1”。说明
由于Pyecharts各个版本的相关代码有一些区别，因此这里建议安装与笔者相同的版本，以免造成不必要的麻烦。那么，对于已经安装完成的Pyecharts，可以使用如下方法查看Pyecharts的版本，代码如下：

import pyecharts
print(pyecharts.__version__)
运行程序，控制台输出结果如下：

1.7.1

如果安装版本与笔者不同，建议卸载重新安装Pyecharts 1.7.1版本。

## 7.1.3　绘制第一张图表

【示例01】　绘制简单的柱状图。（示例位置：资源包\MR\Code\07\01）
下面使用Pyecharts绘制一张简单的柱状图，具体步骤如下。
（1）从pyecharts.charts库中导入Bar模块，代码如下：

from pyecharts.charts import Bar  #从pyecharts.charts库中导入Bar模块

（2）创建一个空的Bar()对象，代码如下：

bar = Bar()
（3）定义x轴和y轴数据，其中x轴为月份，y轴为销量。代码如下：

01 bar.add_xaxis(["1月", "2月", "3月", "4月", "5月", "6月"])
02 bar.add_yaxis("零基础学Python", [2567, 1888, 1359, 3400, 4050, 5500])
03 bar.add_yaxis("Python趣味案例编程", [1567, 988, 2270,3900, 2750, 3600])
（4）渲染图表到HTML文件中，并存放在程序所在目录下，代码如下：

bar.render("mycharts.html")
运行程序，在程序所在路径下生成一个名为mycharts.html的HTML文件，打开该文件，效果如图7.4所示。

![image-20211025093733763](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093733763.png)

​                                                                                                图7.4　绘制第一张图表
以上就是我们绘制的第一张Pyecharts图表。实用技巧Pyecharts 1.0以上版本对方法的链式调用
对于方法的调用可分为**单独调用和链式调用**。单独调用就是常规的一个方法一个方法的调用。而链式调用的关键在于方法化，现在很多开源库或者代码都使用链式调用。链式调用将所有需要调用的方法写在一个方法里，这样使得我们的代码看上去更加简洁易懂。
下面以本节的“第一张图表”为例，在调用Bar模块的各个方法时，将单独调用与链式调用进行简单对比，效果如图7.5所示。



![image-20211025093824559](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093824559.png)

​                                                                                 图7.5　单独调用与链式调用对比
从图7.5中可以看出，链式调用将所有需要调用的方法写在了一个方法里，这样的代码看上去更加简洁易懂。当然，如果不习惯使用链式调用，单独调用也可以。

# 7.2　Pyecharts图表的组成

Pyecharts不仅具备Matplotlib图表的一些常用功能，而且还提供了独有的、别具特色的功能。**主要包括主题风格的设置、提示框、视觉映射、工具箱和区域缩放**等，如图7.6所示。这些功能使得Pyecharts能够绘制出各种各样、超乎想象的图表。

![image-20211025093932297](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025093932297.png)

​                                                                                                    图7.6　Pyecharts图表的组成

## 7.2.1　主题风格

Pyecharts内置提供了15种不同的主题风格，并提供了便捷的定制主题的方法。主要使用Pyecharts库的options模块，通过该模块的InitOpts()方法设置图表的主题风格。下面介绍InitOpts()方法的几个关键参数。


参数说明：　

width：字符型，图表画布宽度，以像素为单位，例如width='500px'。　

height：字符型，图表画布高度，以像素为单位，例如height='300px'。　

chart_id：图表的ID，图表的唯一标识，主要用于多张图表时以区分每张图表。　

page_title：字符型，网页标题。　

theme：图表主题，其参数值主要由ThemeType模块提供。　

bg_color：字符型，图表背景颜色，例如bg_color='black'或bg_color='#fff'。

下面详细介绍一下ThemeType模块提供的15种图表主题风格，如表7.1所示。

​                                                                               表7.1　theme参数设置值

![image-20211025094017187](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094017187.png)

【示例02】　为图表更换主题。（示例位置：资源包\MR\Code\07\02）
下面为“第一张图表”更换主题，具体步骤如下所示。
（1）从pyecharts.charts库中导入Bar模块，代码如下：

from pyecharts.charts import Bar
（2）从pyecharts库中导入options模块，代码如下：

from pyecharts import options as opts
（3）从pyecharts.globals库中导入主题类型模块ThemeType，代码如下：

from pyecharts.globals import ThemeType
（4）设置画布大小、图表主题和图表背景颜色，代码如下：

![image-20211025094339610](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094339610.png)

（5）渲染图表到HTML文件中，并存放在程序所在目录下，代码如下：

bar.render("mycharts1.html")
运行程序，在程序所在路径下生成一个名为mycharts1.html的HTML文件，打开该文件，效果如图7.7所示。

![image-20211025094359953](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094359953.png)

​                                                                                                 图7.7　主题风格

## 7.2.2　图表标题

图表标题主要通过set_global_options()方法的title_opts参数进行设置，该参数值参考options模块的TitleOpts()方法，该方法可以实现主标题、副标题、距离设置以及文字样式等。TitleOpts()方法主要参数说明如下。　

title：字符型，默认值为None。主标题文本，支持换行符“\n”。　

title_link：字符型，默认值为None。主标题跳转URL链接。　

title_target：字符型，默认值为None。主标题跳转链接的方式，默认值为blank，表示在新窗口打开。可选参数self，表示在当前窗口打开。　

subtitle：字符型，默认值为None。副标题文本，支持换行符“\n”。　

subtitle_link：字符型，默认值为None。副标题跳转URL链接。　

subtitle_target：字符型，默认值为None。副标题跳转链接的方式，默认值为blank，表示在新窗口打开。可选参数self，表示在当前窗口打开。　

pos_left：字符型，默认值为None。标题距左侧的距离，其值可以是像10这样的具体像素值，也可以是像10%这样的相对于容器的高宽的百分比，还可以是left、center或right，标题将根据相应的位置自动对齐。　

pos_right：字符型，默认值为None。标题距右侧的距离，其值可以是像10这样的具体像素值，也可以是像10%这样的相对于容器的高宽的百分比。　

pos_top：字符型，默认值为None。标题距顶端的距离，其值可以是像10这样的具体像素值，也可以是像10%这样的相对于容器的高宽的百分比，还可以是top、middle或bottom，标题将根据相应的位置自动对齐。　

pos_bottom：字符型，默认值为None。标题距底端的距离，其值可以是像10这样的具体像素值，也可以是像10%这样的相对于容器的高宽的百分比。　

padding：标题内边距，单位为像素。默认值为各方向（上右下左）内边距为5，接受数组分别设定上右下左边距，例如padding=[10,4,5,90]。　

item_gap：数值型，主标题与副标题之间的间距，例如item_gap=3.5。　

title_textstyle_opts：主标题文字样式配置项，参考options模块的TextStyleOpts()方法。主要包括颜色、字体样式、字体的粗细、字体的大小以及对齐方式等。例如，设置标题颜色为红色，字体大小为16，代码如下：

title_textstyle_opts=opts.TextStyleOpts(color='red',font_size=18)　

subtitle_textstyle_opts：副标题文字样式配置项。同上。

【示例03】　为图表设置标题。（示例位置：资源包\MR\Code\07\03）
下面为“第一张图表”设置标题，具体步骤如下所示。
（1）从pyecharts.charts库中导入Bar模块，代码如下：

from pyecharts.charts import Bar
（2）从pyecharts库中导入options模块，代码如下：

from pyecharts import options as opts
（3）从pyecharts.globals库中导入主题类型模块ThemeType，代码如下：

from pyecharts.globals import ThemeType
（4）生成图表，设置图表标题，包括主标题、主标题字体颜色和大小、副标题、标题内边距，以及主标题与副标题之间的间距。代码如下：

![image-20211025094612795](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094612795.png)

（5）渲染图表到HTML文件中，并存放在程序所在目录下，代码如下：

bar.render("mycharts2.html")
运行程序，在程序所在路径下生成一个名为mycharts2.html的HTML文件，打开该文件，效果如图7.8所示。

![image-20211025094645524](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094645524.png)

​                                                                                                        图7.8　图表标题

## 7.2.3　图例

设置图例主要通过set_global_opts()方法的legend_opts参数进行设置，该参数值参考options模块的LegendOpts()方法。LegendOpts()方法主要参数说明如下。　

is_show：布尔值，是否显示图例，值为True显示图例，值为False则不显示图例。　

pos_left：字符串或数字，默认值为None。图例离容器左侧的距离，其值可以是像10这样的具体像素值，也可以是10%，表示相对于容器高宽的百分比，还可以是left、center或right，图例将根据相应的位置自动对齐。　

pos_right：字符串或数字，默认值为None。图例离容器右侧的距离，其值可以是像10这样的具体像素值，也可以是10%，表示相对于容器高宽的百分比。　

pos_top：字符串或数字，默认值为None。图例离容器顶端的距离，其值可以是像10这样的具体像素值，也可以是10%，表示相对于容器高宽的百分比，还可以是top、middle或bottom，图例将根据相应的位置自动对齐。　

pos_bottom：字符串或数字，默认值为None。图例离容器底端的距离，其值可以是像10这样的具体像素值，也可以是10%，表示相对于容器高宽的百分比。　

orient：字符串，默认值为None。图例列表的布局朝向，其值为horizontal（横向）或vertical（纵向）。

align：字符串。图例标记和文本的对齐，其值为auto、left或right，默认值为auto（自动）。根据图表的位置和orient参数（图例列表的朝向）决定。　padding：整型，图例内边距，单位为像素（px），默认值为各方向内边距为5。　

item_gap：图例之间的间隔。横向布局时为水平间隔，纵向布局时为纵向间隔。默认间隔为10。　

item_width：图例标记的宽度。默认宽度为25。　

item_height：图例标记的高度。默认高度为14。　

textstyle_opts：图例的字体样式。参考options模块的TextStyleOpts()方法。主要包括颜色、字体样式、字体的粗细、字体的大小以及对齐方式等。　

legend_icon：图例标记的样式。其值为circle（圆形）、rect（矩形）、roundRect（圆角矩形）、triangle（三角形）、diamond（菱形）、pin（大头针）、arrow（箭头）或none（无），也可以设置为图片。

【示例04】　为图表设置图例。（示例位置：资源包\MR\Code\07\04）
下面为“第一张图表”设置图例，具体步骤如下所示。
（1）从pyecharts.charts库中导入Bar模块，代码如下：

from pyecharts.charts import Bar
（2）从pyecharts库中导入options模块，代码如下：

from pyecharts import options as opts
（3）生成图表，设置图表标题和图例。其中图例主要包括图例离容器右侧的距离、图例标记的宽度和图例标记的样式，代码如下：

![image-20211025094813219](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094813219.png)

运行程序，在程序所在路径下生成一个名为mycharts3.html的HTML文件，打开该文件，效果如图7.9所示。

![image-20211025094912334](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025094912334.png)

​                                                                                                  图7.9　图例

## 7.2.4　提示框

提示框的设置主要通过set_global_opts()方法的tooltip_opts参数进行设置，该参数值参考options模块的TooltipOpts()方法。TooltipOpts()方法主要参数说明如下。　

is_show：布尔值，是否显示提示框。　

trigger：提示框触发的类型，可选参数。item数据项图形触发，主要在散点图和饼图等无类目轴的图表中使用。axis坐标轴触发，主要在柱状图和折线图等使用类目轴的图表中使用。None不触发，无提示框。　

trigger_on：提示框触发的条件，可选参数。mousemove鼠标移动时触发，click鼠标单击时触发，mousemove|click鼠标移动和单击的同时触发，none鼠标不移动或不单击时触发。　

axis_pointer_type：指示器类型，可选参数。其值如下。　

line：直线指示器。　

shadow：阴影指示器。

cross：十字线指示器。　

none：无指示器。　

background_color：提示框的背景颜色。　

border_color：提示框边框的颜色。　

border_width：提示框边框的宽度。　

textstyle_opts：提示框中文字的样式。参考options模块的TextStyleOpts()方法。主要包括颜色、字体样式、字体的粗细、字体的大小以及对齐方式等。

【示例05】　为图表设置提示框。（示例位置：资源包\MR\Code\07\05）
下面设置提示框的样式，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  from pyecharts import options as opts
02  from pyecharts.charts import Bar
03  from pyecharts.globals import ThemeType
（2）设置图表标题和图例。其中图例主要包括图例离容器右侧的距离、图例标记的宽度和图例标记的样式，代码如下：

![image-20211025095151357](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025095151357.png)

（3）生成图表，设置提示框。鼠标单击时触发提示框，设置提示框为十字线指示器，设置背景色、边框宽度和边框颜色，代码如下：

![image-20211025095209115](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025095209115.png)



运行程序，在程序所在路径下生成一个名为mycharts5.html的HTML文件，打开该文件，效果如图7.10所示。

![image-20211025095249239](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025095249239.png)

​                                                                                              图7.10　提示框

## 7.2.5　视觉映射

视觉映射主要通过set_global_opts()方法的title_opts参数进行设置，该参数值参考options模块的VisualMapOpts()方法。VisualMapOpts()方法主要参数说明如下。　

is_show：布尔型，是否显示视觉映射配置。　

type_：映射过渡类型，可选参数，其值为color或size。　_

_min_：整型或浮点型，颜色条的最小值。　

max_：整型或浮点型，颜色条的最大值。　

range_text：颜色条两端的文本，例如，High或Low。　range_color：序列。颜色范围（过渡颜色），例如range_color=["#FFF0F5", "#8B008B"]。　orient：颜色条放置方式，水平（horizontal）或者竖直（vertical）。　pos_left：颜色条离左侧的距离。　dimension：颜色条映射的维度。　is_piecewise：布尔型，是否分段显示数据。【示例06】　为图表添加视觉映射。（示例位置：资源包\MR\Code\07\06）
下面为图表添加视觉映射，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  from pyecharts import options as opts

02  from pyecharts.charts import Bar
（2）为柱状图添加数据，代码如下：

![image-20211025101615302](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025101615302.png)

（3）设置图表标题和视觉映射，并生成图表，代码如下：

![image-20211025101634254](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025101634254.png)

运行程序，在程序所在路径下生成一个名为mycharts6.html的HTML文件，打开该文件，效果如图7.11所示。

![image-20211025101655610](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025101655610.png)

​                                                                                                 图7.11　视觉映射

## 7.2.6　工具箱

工具箱主要通过set_global_opts()方法的title_opts参数进行设置，该参数值参考options模块的ToolboxOpts()方法。ToolboxOpts()方法主要参数说明如下。　

is_show：布尔值，是否显示工具箱。　

orient：工具箱的布局朝向。可选参数，默认值为None，其值为horizontal（水平）或vertical（竖直）。　

pos_left：工具箱离容器左侧的距离。　

pos_right：工具箱离容器右侧的距离。　

pos_top：工具箱离容器顶端的距离。　

pos_bottom：工具箱离容器底端的距离。　

feature：工具箱中每个工具的配置项。

【示例07】　为图表添加工具箱。（示例位置：资源包\MR\Code\07\07）
下面为图表添加工具箱，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  from pyecharts import options as opts
02  from pyecharts.charts import Bar
（2）绘制柱状图，代码如下：

![image-20211025102300265](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102300265.png)

（3）添加工具箱，并生成图表，代码如下：

![image-20211025102427248](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102427248.png)运行程序，在程序所在路径下生成一个名为mycharts7.html的HTML文件，打开该文件，效果如图7.12所示。

![image-20211025102448491](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102448491.png)

​                                                                                         图7.12　工具箱

## 7.2.7　区域缩放

区域缩放工具条主要通过set_global_opts()方法的datazoom_opts参数进行设置，该参数值参考options模块的DataZoomOpts()方法。DataZooDataZoomOpts()方法主要参数说明如下。　

is_show：布尔值，是否显示区域缩放工具条。　

type_：区域缩放工具条的类型，可选参数，其值为slider或inside。　

is_realtime：布尔值，是否实时更新图表。　

range_start：数据窗口范围的起始百分比，其值为0～100，表示0%～100%。　

range_end：数据窗口范围的结束百分比，其值为0～100，表示0%～100%。　

start_value：数据窗口的起始数值。　

end_value：数据窗口范围的结束数值。　

orient：区域缩放工具条的布局方式。可选参数，默认值为None，其值为horizontal（水平）或vertical（竖直）。　

pos_left：工具箱离容器左侧的距离。　

pos_right：工具箱离容器右侧的距离。　

pos_top：工具箱离容器顶端的距离。　

pos_bottom：工具箱离容器底端的距离。

【示例08】　为图表添加区域缩放。（示例位置：资源包\MR\Code\07\08）
下面为图表添加区域缩放工具条，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  from pyecharts import options as opts
02  from pyecharts.charts import Bar
（2）绘制柱状图，代码如下：

![image-20211025102558340](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102558340.png)



（3）添加区域缩放工具条，并生成图表，代码如下：

![image-20211025102644997](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102644997.png)

运行程序，在程序所在路径下生成一个名为mycharts8.html的HTML文件，打开该文件，效果如图7.13所示。

![image-20211025102719440](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102719440.png)

​                                                                                                       图7.13　区域缩放

# 7.3　Pyecharts图表的绘制

## 7.3.1　柱状图——Bar模块

绘制柱状图／条形图主要使用Bar模块实现，主要方法介绍如下。

add_xaxis()：x轴数据。　

add_yaxis()：y轴数据。　

reversal_axis()：翻转x、y轴数据。　

add_dataset()：原始数据。一般来说，原始数据表达的是二维表。

【示例09】　绘制多柱状图。（示例位置：资源包\MR\Code\07\09）
上述内容简单介绍了柱状图的绘制，下面通过Pandas导入Excel文件中的数据，然后绘制多柱状图，分析近7年各个电商平台的销量情况，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  import pandas as pd
02  from pyecharts.charts import Bar
03  from pyecharts import options as opts
04  from pyecharts.globals import ThemeType
（2）导入Excel文件，代码如下：

01  #导入Excel文件
02  df = pd.read_excel('books.xlsx',sheet_name='Sheet2')
03  #x轴和y轴数据
04  x=list(df['年份'])
05  y1=list(df['京东'])
06 y2=list(df['天猫'])
07 y3=list(df['自营'])
（3）绘制多柱状图，代码如下：



运行程序，对比效果如图7.14和图7.15所示。

![image-20211025102857406](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102857406.png)

​                                                                                                     图7.14　数据展示

![image-20211025102918759](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025102918759.png)

​                                                                                             图7.15　多柱状图展示

## 7.3.2　折线／面积图——Line模块

绘制折线／面积图主要使用Line模块的add_xaxis()方法和add_yaxis()方法实现。下面介绍add_yaxis()方法的几个主要参数。　series_name：系列名称。用于提示文本和图例标签。　

y_axis：y轴数据。　

color：标签文本的颜色。　

symbol：标记。包括circle、rect、roundRect、triangle、diamond、pin、arrow或none，也可以设置为图片。　

symbol_size：标记大小。　

is_smooth：布尔值，是否为平滑曲线。　

is_step：布尔值，是否显示为阶梯图。　

linestyle_opts：线条样式。参考series_options.LineStyleOpts。　

areastyle_opts：填充区域配置项，主要用于绘制面积图。该参数值须参考options模块的AreaStyleOpts()方法，例如areastyle_opts=opts.AreaStyleOpts(opacity=1)。

【示例10】　绘制折线图。（示例位置：资源包\MR\Code\07\10）
下面绘制折线图，分析近7年各个电商平台的销量情况，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  import pandas as pd
02  from pyecharts.charts import Line
（2）绘制折线图，代码如下：

运行程序，在程序所在路径下生成myline1.html的HTML文件，打开该文件，效果如图7.16所示。

![image-20211025103019599](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103019599.png)

​                                                                                                         图7.16　折线图

注意

x轴数据必须为字符串，否则图表不显示。如果数据为其他类型，需要使用str()函数转换为字符串，如x_data=[str(i) for i in x]。

【示例11】　绘制面积图。（示例位置：资源包\MR\Code\07\11）
使用Line模块还可以绘制面积图，主要通过在add_yaxis()方法中指定areastyle_opts参数，该参数值由options模块的AreaStyleOpts()方法提供。下面绘制面积图，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  import pandas as pd
02  from pyecharts.charts import Line
03  from pyecharts import options as opts
（2）绘制面积图，代码如下：

![image-20211025103120692](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103120692.png)

运行程序，在程序所在路径下生成myline2.html的HTML文件，打开该文件，效果如图7.17所示。

![image-20211025103137908](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103137908.png)

​                                                                                                  图7.17　面积图

## 7.3.3　饼形图——Pie模块

绘制饼形图主要使用Pie模块的add()方法实现。下面介绍add()方法的几个主要参数。　

series_name：系列名称。用于提示文本和图例标签。　

data_pair：数据项，格式为[(key1, value1), (key2, value2)]。可使用zip()函数将可迭代对象打包成元组，然后再转换为列表。　

color：系列标签的颜色。　

radius：饼图的半径，数组的第一项是内半径，第二项是外半径。默认设置为百分比，相对于容器高宽中较小的一项的一半。

rosetype：是否展开为南丁格尔玫瑰图（也称南丁格尔的玫瑰），通过半径区分数据大小。其值为radius或area，radius表示通过扇区圆心角展现数据的百分比，通过半径展现数据的大小；area表示所有扇区圆心角相同，仅通过半径展现数据的大小。知识胶囊
南丁格尔，英国护士和统计学家，出生于意大利的一个英国上流社会的家庭。南丁格尔被描述为“在统计的图形显示方法上，是一个真正的先驱”，她发展出极坐标图饼图的形式，或称为南丁格尔玫瑰图，相当于现代圆形直方图，以说明她在管理的野战医院内，病人死亡率在不同季节的变化。她使用极坐标图饼图，向不会阅读统计报告的国会议员，报告克里米亚战争的医疗条件。　

is_clockwise：饼图的扇区是否以顺时针显示。

【示例12】　饼形图分析各地区销量占比情况。（示例位置：资源包\MR\Code\07\12）
下面绘制饼形图，分析各地区销量占比情况，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  import pandas as pd
02  from pyecharts.charts import Pie
03  from pyecharts import options as opts
（2）导入Excel文件，并将数据处理为列表加元组的形式，代码如下：

![image-20211025103236326](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103236326.png)

（3）创建饼形图，代码如下：

![image-20211025103625577](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103625577.png)

运行程序，在程序所在路径下生成mypie1.html的HTML文件，打开该文件，效果如图7.18所示。

![image-20211025103706227](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103706227.png)

​                                                                                               图7.18　饼形图

## 7.3.4　箱形图——Boxplot模块

【示例13】　绘制简单的箱形图。（示例位置：资源包\MR\Code\07\13）
绘制箱形图主要使用Boxplot模块的add_xaxis()方法和add_yaxis()方法实现。下面绘制一个简单的箱形图，程序代码如下：

![image-20211025103730467](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103730467.png)

运行程序，在程序所在路径下生成myboxplot.html的HTML文件，打开该文件，效果如图7.19所示。

![image-20211025103753043](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103753043.png)

​                                                                                                 图7.19　箱形图

## 7.3.5　涟漪特效散点图——EffectScatter模块

【示例14】　绘制简单的散点图。（示例位置：资源包\MR\Code\07\14）
绘制涟漪特效散点图主要使用EffectScatter模块的add_xaxis()方法和add_yaxis()方法实现。下面绘制一个简单的涟漪特效散点图，程序代码如下：

![image-20211025103917833](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103917833.png)

运行程序，在程序所在路径下生成myscatter.html的HTML文件，打开该文件，效果如图7.20所示。

![image-20211025103937243](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025103937243.png)

​                                                                                    图7.20　涟漪特效散点图

## 7.3.6　词云图——WordCloud模块

绘制词云图主要使用WordCloud模块的add()方法实现。下面介绍add()方法的几个主要参数。　

series_name：系列名称。用于提示文本和图例标签。　

data_pair：数据项。格式为[(word1,count1), (word2, count2)]。可使用zip()函数将可迭代对象打包成元组，然后再转换为列表。　

shape：字符型，词云图的轮廓。其值为circle、cardioid、diamond、triangle-forward、triangle、pentagon或star。　

mask_image：自定义图片（支持的图片格式为jpg、jpeg、png和ico）。该参数支持base64（一种基于64个可打印字符来表示二进制数据的方法）和本地文件路径（相对或者绝对路径都可以）。　

word_gap：单词间隔。　

word_size_range：单词字体大小范围。　

rotate_step：旋转单词角度。　

pos_left：距离左侧的距离。　

pos_top：距离顶部的距离。　

pos_right：距离右侧的距离。　

pos_bottom：距离底部的距离。　

width：词云图的宽度。　

height：词云图的高度。
实现词云图首先需要通过jieba模块的TextRank算法从文本中提取关键词。TextRank是一种文本排序算法，是基于著名的网页排序算法PageRank改动而来。TextRank不仅能进行关键词提取，也能做自动文摘。
根据某个词所连接的所有词汇的权重（权重是指某一因素或指标相对于某一事物的重要程度，这里指某个词在整段文字中的重要程度），重新计算该词汇的权重，然后把重新计算的权重传递下去，直到这种变化达到均衡态，权重数值不再发生改变。根据最后的权重值，取其中排列靠前的词汇作为关键词。

【示例15】　绘制词云图分析用户评论内容。（示例位置：资源包\MR\Code\07\15）
接下来绘制词云图，分析用户的评论内容。具体步骤如下所示。
（1）安装jieba模块，运行anaconda prompt（Anaconda），通过pip命令安装jieba模块，安装命令如下：

pip install jieba
（2）导入相关模块，代码如下：

01  from pyecharts.charts import WordCloud
02  from jieba import analyse

（3）使用TextRank算法从文本中提取关键词，代码如下：

![image-20211025104200766](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104200766.png)

（4）关键词列表，代码如下：

![image-20211025104221304](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104221304.png)

（5）绘制词云图，代码如下：

01  mywordcloud=WordCloud()
02  mywordcloud.add('',list1,word_size_range=[20,100])
03  mywordcloud.render('wordclound.html')
运行程序，在程序所在路径下生成wordclound.html的HTML文件，打开该文件，效果如图7.21所示。

![image-20211025104247930](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104247930.png)

​                                                                                               图7.21　词云图

## 7.3.7　热力图——HeatMap模块

【示例16】　热力图统计双色球中奖号码出现的次数。（示例位置：资源包\MR\Code\07\16）

绘制热力图主要使用HeatMap模块的add_xaxis()方法和add_yaxis()方法。下面通过热力图统计2014—2019年双色球中奖号码出现的次数，具体步骤如下所示。
（1）导入相关模块，代码如下：

01  import pyecharts.options as opts
02  from pyecharts.charts import HeatMap
03  import pandas as pd
（2）导入Excel文件，并进行数据处理，代码如下：

![image-20211025104333637](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104333637.png)

（3）将数据转换为HeatMap支持的列表格式，代码如下：

![image-20211025104354300](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104354300.png)

（4）绘制热力图，代码如下：

![image-20211025104427190](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104427190.png)

运行程序，在程序所在路径下生成heatmap.html的HTML文件，打开该文件，效果如图7.22所示。

![image-20211025104521598](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025104521598.png)

图7.22　热力图

## 7.3.8　水球图——Liquid模块

【示例17】　绘制水球图。（示例位置：资源包\MR\Code\07\17）
绘制水球图主要使用Liquid模块的add()方法实现。下面绘制一个简单的涟漪特效散点图，程序代码如下：



运行程序，在程序所在路径下生成myliquid.html的HTML文件，打开该文件，效果如图7.23所示。

![image-20211025105150709](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105150709.png)

​                                                                                                            图7.23　水球图

## 7.3.9　日历图——Calendar模块

【示例18】　绘制加班日历图。（示例位置：资源包\MR\Code\07\18）
绘制日历图主要使用Calendar模块的add()方法实现。下面绘制一个简单日历图，通过该日历图分析6月份加班情况，程序代码如下：

![image-20211025105216401](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105216401.png)



运行程序，在程序所在路径下生成calendar.html的HTML文件，打开该文件，效果如图7.24所示。

![image-20211025105257503](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105257503.png)

​                                                                                                   图7.24　日历图

# 7.4　综合应用

## 7.4.1　案例1：南丁格尔玫瑰图

案例位置：资源包\MR\Code\07\example\01
下面使用Pie模块绘制南丁格尔玫瑰图，效果如图7.25所示。
南丁格尔玫瑰图主要通过绘制饼形图实现，其中一个关键点是设置rosetype参数为area，具体实现步骤如下所示。
（1）导入相关模块，代码如下：

01  import pandas as pd
02  from pyecharts.charts import Pie

03  from pyecharts import options as opts

![image-20211025105352924](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105352924.png)

​                                                                                图7.25　南丁格尔玫瑰图
（2）导入Excel文件，并对数据进行处理，代码如下：

![image-20211025105510687](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105510687.png)

（3）绘制南丁格尔玫瑰图，代码如下：

![image-20211025105530815](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105530815.png)

## 7.4.2　案例2：双y轴可视化数据分析图表的实现（柱形图+折线图）

案例位置：资源包\MR\Code\07\example\02

双y轴顾名思义就是两个y轴，下面实现柱形图+折线图双y轴图表的绘制，其中柱形图y轴表示月销量，折线图y轴表示3个平台的月平均销量，效果如图7.26所示。

![image-20211025105606632](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105606632.png)

​                                                              图7.26　双y轴可视化数据分析图表
实现双y轴可视化数据分析图表的两个关键点：一是使用Bar模块的extend_axis()方法扩展y轴；二是对add_yaxis()方法的yaxis_index参数进行设置，该参数用于指定y轴的索引值，从0开始。双y轴索引值分别为0和1。具体实现步骤如下所示。
（1）导入相关模块，代码如下：

01  import pyecharts.options as opts
02  from pyecharts.charts import Bar, Line
03  import pandas as pd
04  import numpy
（2）导入Excel文件，代码如下：

![image-20211025105630197](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105630197.png)

（3）创建颜色列表，代码如下：

colors = ["#5793f3", "#FFD700", "#675bba"]
（4）求平均值并保留整数位，代码如下：

y_average=list(((df['京东']+df['天猫']+df['自营'])/3).apply(numpy.round))

（5）绘制柱形图，代码如下：

![image-20211025105718321](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105718321.png)

（6）绘制折线图，代码如下：

![image-20211025105735016](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105735016.png)



## 7.4.3　案例3：饼形图与环形图组合图表的实现

案例位置：资源包\MR\Code\07\example\03
饼形图与环形图组合，其中饼形图展示“北上广”三大主要城市的销量情况，环形图展示其他省份的销量情况，效果如图7.27所示。

![image-20211025105757566](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105757566.png)

​                                                                              图7.27　饼形图与环形图组合图表
绘制饼形图与环形图组合图表的一个关键点是创建两个饼形图，并设置不同的半径（radius参数），具体实现步骤如下所示。
（1）导入相关模块，代码如下：

01  import pyecharts.options as opts

02  from pyecharts.charts import Pie
（2）为饼形图和环形图添加数据，代码如下：

![image-20211025105830032](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105830032.png)

（3）饼形图与环形图组合，代码如下：

![image-20211025105847941](第7章第三方可视化数据分析图表Pyecharts.assets/image-20211025105847941.png)

知识胶囊
下面介绍一下Pyecharts的文本标签配置项。　

字体基本样式：fontStyle、fontWeight、fontSize、fontFamily。　

文字颜色：color。　

文字描边：textBorderColor、textBorderWidth。　

文字阴影：textShadowColor、textShadowBlur、textShadowOffsetX、textShadowOffsetY。　

文本块或文本片段大小：lineHeight、width、height、padding。　

文本块或文本片段的对齐：align、verticalAlign。　

文本块或文本片段的边框、背景（颜色或图片）：backgroundColor、borderColor、borderWidth、borderRadius。　

文本块或文本片段的阴影：shadowColor、shadowBlur、shadowOffsetX、shadowOffsetY。　

文本块的位置和旋转：position、distance、rotate。

# 7.5　小结

相比Matplotlib和Searnborn，Pyecharts绘制出的图表更加令人惊叹，其动感效果更是Matplotlib和Searnborn无法比拟的，但也存在不足之处，其生成的图表为网页格式，不能够随时查看，需要打开文件进行浏览。Pyecharts更适合Web程序。
Pyecharts还有很多功能，由于篇幅有限不能一一进行介绍，希望读者在学习过程中能够举一反三，绘制出更多精彩的数据分析图表。

