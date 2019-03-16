---
title: Matplotlib 学习笔记
date: 2019-03-13 21:23:56
tags:
    - python
    - Matplotlib
    - noteBook
toc: true
---

## Matplotlib

Matplotlib 是Python2D绘图领域使用最广泛的套件。能导出多种格式的图片。

### Matplotlib中文显示

Matplotlib默认是不支持中文的，如果出现中文会以方框代替。

![cn_error](http://poatdt87z.bkt.clouddn.com/cn_erro.png)

但是经过测试国外字体中部分可以支持。

```python
goodfont=[
 'Adobe Heiti Std',
 'Arial Unicode MS',
 'DengXian',
 'SimHei',
 'STKaiti',
 'STXihei',
]
```
<!-- more -->
使用fontproperties指定字体

```python
import numpy as np
from matplotlib import pyplot as plt
import matplotlib
zh_cn_font = matplotlib.font_manager.FontProperties(fname="F:\ProjectFiles\SimHei.ttf")
#第七行的作用是为了消除更换为unicode字体之后0、负数之类的显示异常。之后所有使用中文字体的地方只字符串都以u""的形式出现，并指定fontproperties属性为我们的指定的myfont就行了
matplotlib.rcParams['axes.unicode_minus'] = False
#matplotlib.rcParams['font.sans-serif'] = ['SimHei']
x = np.arange(0,9)
y = 2*x+1
plt.title(u"Matplotlib 标题",fontproperties = zh_cn_font)
plt.xlabel(u"x 轴:",fontproperties = zh_cn_font)
plt.ylabel(u"y 轴:",fontproperties = zh_cn_font)
plt.plot(x,y)
plt.show()
```

一劳永逸法

1. 找到matplotlib 配置文件：import matplotlib 
    print(matplotlib.matplotlib_fname()) 
#我自己的输出结果如下：
#D:\Program Files\Python36\Lib\site-packages\matplotlib\mpl-data
2. 编辑器打开此文件 matplotlibrc删除font.family和font.sans-serif两行前的#，并在font.sans-serif后添加微软雅黑字体Microsoft YaHei
3. 下载字体:msyh.ttf (微软雅黑)放在matplotlib 字体文件夹下:# D:\Program Files\Python36\Lib\site-packages\matplotlib\mpl-data\fonts\ttf
4. 删除.matplotlib/cache里面的两个缓存字体文件C:\Users\你的用户名\.matplotlib<img src="https://pic4.zhimg.com/50/v2-92f9f704ea4e9f440b57d3074da29db4_hd.jpg" data-rawwidth="254" data-rawheight="56" class="content_image" width="254"/>
5. 重启Python

![ch_pic](http://poatdt87z.bkt.clouddn.com/line_cn.png)

### 绘制一次方程

使用matplotlib中的pylot包进行简单绘图。

```python
import numpy as np
from matplotlib import pyplot as plt

x = np.arange(0,9)
y = 2*x+1
plt.title("Matplotlib Demo1")
plt.xlabel("x axis:")
plt.ylabel("y axis:")
plt.plot(x,y)
plt.show()
```

![demo1](http://poatdt87z.bkt.clouddn.com/line.png)

### 绘制离散图

向pyplot的plot()函数添加特殊的格式化字符串可以显示离散值。

| 字符       | 描述         |
| :--------- | :----------- |
| `'-'`      | 实线样式     |
| `'--'`     | 短横线样式   |
| `'-.'`     | 点划线样式   |
| `':'`      | 虚线样式     |
| `'.'`      | 点标记       |
| `','`      | 像素标记     |
| `'o'`      | 圆标记       |
| `'v'`      | 倒三角标记   |
| `'^'`      | 正三角标记   |
| `'&lt;'`   | 左三角标记   |
| `'&gt;'`   | 右三角标记   |
| `'1'`      | 下箭头标记   |
| `'2'`      | 上箭头标记   |
| `'3'`      | 左箭头标记   |
| `'4'`      | 右箭头标记   |
| `'s'`      | 正方形标记   |
| `'p'`      | 五边形标记   |
| `'*'`      | 星形标记     |
| `'h'`      | 六边形标记 1 |
| `'H'`      | 六边形标记 2 |
| `'+'`      | 加号标记     |
| `'x'`      | X 标记       |
| `'D'`      | 菱形标记     |
| `'d'`      | 窄菱形标记   |
| `'&#124;'` | 竖直线标记   |
| `'_'`      | 水平线标记   |

以下是颜色的缩写：

| 字符  | 颜色   |
| :---- | :----- |
| `'b'` | 蓝色   |
| `'g'` | 绿色   |
| `'r'` | 红色   |
| `'c'` | 青色   |
| `'m'` | 品红色 |
| `'y'` | 黄色   |
| `'k'` | 黑色   |
| `'w'` | 白色   |

例如：要显示圆来代表点，而不是上面示例中的线，请使用 ob 作为 plot() 函数中的格式字符串。

### 绘制正弦函数

```python
import numpy as np
from matplotlib import pyplot as plt
import matplotlib
m = np.arange(0,4,0.1)
n = np.sin(m*np.pi)
plt.title(u"Matplotlib 正弦函数")
plt.xlabel(u"x 轴:")
plt.ylabel(u"y 轴:")
plt.plot(m,n,'-')
plt.show()
```

![sin](http://poatdt87z.bkt.clouddn.com/sin.png)

### 绘制子图

`pyplot.subplot(nrows,ncols,index)`可以在一个figure中添加多个子图像。

使用`plt.subtiltle('')`给整个figure添加标题，使用plt.title('')给每个subplot添加子标题，修改x轴范围使用plt.xlim(min,max)，修改x轴刻度使用plt.xticks([numlist],[textlist])。

```python
import numpy as np
from matplotlib import pyplot as plt
import matplotlib
x = np.arange(0,3,0.05)
n = np.linspace(-np.pi/2,np.pi/2,50)
y = np.sin(x*np.pi)
z = np.cos(x*np.pi)
p = np.tan(n)
q = np.tan(np.pi/2-n)

plt.figure(figsize = (16,9),dpi = 80)

plt.suptitle('Matplotlib 绘制多图',fontsize = 40,weight = 40)

plt.subplot(2,2,1)
plt.title(u"正弦函数")
plt.xlabel(u"x 轴:")
plt.ylabel(u"y 轴:")
plt.plot(x,y,'-',label = 'sine')

plt.subplot(2, 2, 2)
plt.title(u"余弦函数")
plt.xlabel(u"x 轴:")
plt.ylabel(u"y 轴:")
plt.plot(x,z,'-',label = 'cosine')

plt.subplot(2, 2, 3)
plt.xlim(n.min()*1.1,n.max()*1.1)
plt.xticks([-np.pi/2,-np.pi/4,0,np.pi/4,np.pi/2],[r'$-\pi/2$',r'$-\pi/4$',r'$0$',r'$\pi/4$',r'$\pi/2$'])
plt.ylim(-10,10)
plt.title(u"正切函数")
plt.xlabel(u"x 轴:")
plt.ylabel(u"y 轴:")
plt.plot(n,p,'-',label = 'tan')

plt.subplot(2, 2, 4)
plt.xlim(n.min()*1.1,n.max()*1.1)
plt.xticks([-np.pi/2,-np.pi/4,0,np.pi/4,np.pi/2],[r'$-\pi/2$',r'$-\pi/4$',r'$0$',r'$\pi/4$',r'$\pi/2$'])
plt.ylim(-10,10)
plt.title(u"余弦函数")
plt.xlabel(u"x 轴:")
plt.ylabel(u"y 轴:")
plt.plot(n,q,'-',label = 'cotan')

plt.show()
```

![绘制子图](http://poatdt87z.bkt.clouddn.com/subplot.png)

### 绘制条形图

`plt,bar(x,y,width = 0.8, align = 'center',  color = 'r')`绘制垂直条形图

`plt.barh(x,y,width = 0.8, align = 'center', color = 'r')绘制水平条形图`

x 为x值的列表，y为y值的列表，width宽度

```python
import numpy as np
from matplotlib import pyplot as plt
import matplotlib
plt.figure(figsize=(16,9),dpi = 80)
plt.title('条形图绘制',fontsize = 40)
xlist = [10,20,30,40,50]
ylist = [5,15,10,50,45]
plt.bar(xlist,ylist,width = 5)
plt.show()
```

![条形图](http://poatdt87z.bkt.clouddn.com/bar.png)

`numpy.histogram(ndarray,bins = [])`自动区间分组计数器

- bins:分组区间

```python
import matplotlib
import numpy as np
import matplotlib.pyplot as plt
plt.figure(figsize = (16,9),dpi = 80)
plt.title('使用Histogram自动分组计数',fontsize = 30)
plt.xlabel('分数区间')
plt.ylabel('人数')

data = [86,62,55,42,98,45,58,60,75,79,82,85,72,77,32]
rank,bins = np.histogram(data,[0,10,20,30,40,50,60,70,80,90,100])
plt.xticks(bins)
plt.xlim(bins.min(),bins.max())
rects = plt.bar(bins[:len(bins)-1],rank,width = 6,align = 'edge',)
def autolabe(rects):
	for rect in rects:
		y = rect.get_height()
		x = rect.get_x()
		print(x,'\t',y)
		plt.text(x+3,y+0.05,'{}'.format(y),color = 'b',fontsize = 20,ha = 'center')
autolabe(rects)
plt.show()
```

![Histogram 自动分组计数](http://poatdt87z.bkt.clouddn.com/np_histogram.png)

`matplotlib.pyplot.hist()`可以轻松解决上面的复杂过程。

```python
import numpy as np
from matplotlib import pyplot as plt
import matplotlib
plt.figure(figsize = (16,9),dpi = 80)
plt.title('使用Histogram自动分组计数',fontsize = 30)
plt.xlabel('分数区间')
plt.ylabel('人数')
bins = np.array([0,10,20,30,40,50,60,70,80,90,100])
plt.xticks(bins)
plt.xlim(bins.min(),bins.max())
data = np.array([86,62,55,42,98,45,58,60,75,79,82,85,72,77,32])
plt.hist(data,bins = bins,width = 6)
plt.show()
```

![hist(ndarray,bins)生成条形图](http://poatdt87z.bkt.clouddn.com/hist.png)

### 绘制破损条形图

使用`plt.broken_barh([(star,len),(star2,len2)[,],facecolor = 'b',frameon = Ture)`，`plt.broken_bar([(star,len),(star2,len2)[,],)`来绘制破损条形图。

### 绘制饼图

`plot.pie(x, explode=None, labels=None, colors=None, autopct=None,
        pctdistance=0.6, shadow=False, labeldistance=1.1, startangle=None,
        radius=None, counterclock=True, wedgeprops=None, textprops=None,
        center=(0, 0), frame=False, rotatelabels=False, hold=None, data=None)`用来绘制饼图

- x       :(每一块)的比例，如果sum(x) > 1会使用sum(x)归一化；
- labels  :(每一块)饼图外侧显示的说明文字；
- explode :(每一块)离开中心距离；
- startangle :起始绘制角度,默认图是从x轴正方向逆时针画起,如设定=90则从y轴正方向画起；
- shadow  :在饼图下面画一个阴影。默认值：False，即不画阴影；
- labeldistance :label标记的绘制位置,相对于半径的比例，默认值为1.1, 如<1则绘制在饼图内侧；
- autopct :控制饼图内百分比设置,可以使用format字符串或者format function
  '%1.1f%%'指使用百分比法且精确到小数点前后1位数(没有用空格补齐)；
- pctdistance :类似于labeldistance,指定autopct的位置刻度,默认值为0.6；
- radius  :控制饼图半径，默认值为1；
- counterclock ：指定指针方向；布尔值，可选参数，默认为：True，即逆时针。将值改为False即可改为顺时针。
- wedgeprops ：字典类型，可选参数，默认值：None。参数字典传递给wedge对象用来画一个饼图。例如：wedgeprops={'linewidth':3}设置wedge线宽为3。
- textprops ：设置标签（labels）和比例文字的格式；字典类型，可选参数，默认值为：None。传递给text对象的字典参数。
- center ：浮点类型的列表，可选参数，默认值：(0,0)。图标中心位置。
- frame ：布尔类型，可选参数，默认值：False。如果是true，绘制带有表的轴框架。
- rotatelabels ：布尔类型，可选参数，默认为：False。如果为True，旋转每个label到指定的角度。

```python
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import savepath

plt.figure(figsize = (16,9),dpi = 80)

plt.suptitle('青年人经济支出构成')
labels = ['娱乐','教育','衣食','住房','交通','育儿','其他']
data = [.1,.12,.14,.3,.11,.22,.01]
plt.pie(data,explode = [0,0.1,0.1,0,0,0.1,0],labels = labels,autopct = '%1.1f%%',shadow = True)
plt.legend(frameon = True,framealpha = 0.7,loc = 'upper left')
plt.show()
```

![pie](http://poatdt87z.bkt.clouddn.com/pie.png)



### 绘制一个完整的线型图

1. 首先先汇出正弦和余弦函数各一个周期。

   ```python
   import numpy as np
   from matplotlib import pyplot as plt
   import matplotlib
   plt.figure(figsize = (16,9),dpi = 80)
   plt.title('绘制正余弦函数',fontsize = 30)
   x = np.linspace(0,2*np.pi,256)
   y1 = np.sin(x)
   y2 = np.cos(x)
   plt.ylim(y1.min()*1.1,y1.max()*1.1)
   plt.xlim(x.min()*1.1,x.max()*1.1)
   plt.xticks([0,np.pi/4,np.pi/2,np.pi*3/4,np.pi,np.pi*5/4,np.pi*3/2,np.pi*7/4,np.pi*2],\
   			[r'$0$',r'$\frac{1}{4}\pi$',r'$\frac{1}{2}\pi$',r'$\frac{3}{4}\pi$',r'$\pi$',\
   			r'$\frac{5}{4}\pi$',r'$\frac{3}{2}\pi$',r'$\frac{7}{4}\pi$',r'$2\pi$',])
   plt.plot(x,y1,'-b',linewidth = 2)
   plt.plot(x,y2,'-r',linewidth = 2)
   
   plt.show()
   ```

   ![绘制正余弦函数Base](http://poatdt87z.bkt.clouddn.com/sin_cos_base.png)

   ​	图片绘制出来看起来非常平滑，非常美。虽然大体的图像已经绘制出来了，但是作为一个科学绘图库这点只是皮毛。接下来要给图像增加更多元素，使之看起来更完美。

   2. 添加图例

      使用`plt.legend(loc = (upper,left),frameon = True,framealpha = 0.7)`给图片添加图例。

      ```python
      import numpy as np
      from matplotlib import pyplot as plt
      import matplotlib
      plt.figure(figsize = (16,9),dpi = 80)
      plt.title('绘制正余弦函数',fontsize = 30)
      x = np.linspace(0,2*np.pi,256)
      y1 = np.sin(x)
      y2 = np.cos(x)
      plt.ylim(y1.min()*1.1,y1.max()*1.1)
      plt.xlim(x.min()*1.1,x.max()*1.1)
      plt.xticks([0,np.pi/4,np.pi/2,np.pi*3/4,np.pi,np.pi*5/4,np.pi*3/2,np.pi*7/4,np.pi*2],\
      			[r'$0$',r'$\frac{1}{4}\pi$',r'$\frac{1}{2}\pi$',r'$\frac{3}{4}\pi$',r'$\pi$',\
      			r'$\frac{5}{4}\pi$',r'$\frac{3}{2}\pi$',r'$\frac{7}{4}\pi$',r'$2\pi$',])
      plt.plot(x,y1,'-b',linewidth = 2, label = 'sine')
      plt.plot(x,y2,'-r',linewidth = 2, label = 'cosine' )
      plt.legend(loc = 'upper left',frameon = True,framealpha = 0.7)
       
      plt.show()
      ```

      ![legend](http://poatdt87z.bkt.clouddn.com/sin_cos_legend.png)

   3.  调整坐标轴原点使其与图像中心对齐

      坐标轴线和上面的记号连在一起就形成了脊柱（Spines）

      在matplotlib的定义中一个图像有四条脊柱，我们为了实现目标，必须把上和右的spines置为无色，然后把左和下的spines调整到合适的位置。

      ```python
      ax = plt.gca()
      ax.spines['top'].set_color('none')
      ax.spines['right'].set_color('none')
      ax.spines['bottom'].set_position(('data',0))
      ax.spines['left'].set_position(('data',0))
      ```

      ![sin_cos_coords](http://poatdt87z.bkt.clouddn.com/sin_cos_coords.png)

   4. 添加锚点和虚线，添加标注

      ```python
      import numpy as np
      from matplotlib import pyplot as plt
      import matplotlib
      plt.figure(figsize = (16,9),dpi = 80)
      plt.title('绘制正余弦函数',fontsize = 40,va = 'bottom')
      x = np.linspace(-np.pi,2*np.pi,384)
      y1 = np.sin(x)
      y2 = np.cos(x)
      
      plt.ylim(y1.min()*1.1,y1.max()*1.1)
      plt.xlim(x.min()*1.1,x.max()*1.1)
      plt.xticks([-np.pi,-np.pi*3/4,-np.pi/2,-np.pi/4,0,np.pi/4,np.pi/2,np.pi*3/4,np.pi,np.pi*5/4,np.pi*3/2,np.pi*7/4,np.pi*2],\
      			[r'$-\pi$',r'$-\frac{3}{4}\pi$',r'$-\frac{1}{2}\pi$',r'$-\frac{1}{4}\pi$',r'$0$',r'$\frac{1}{4}\pi$',r'$\frac{1}{2}\pi$',r'$\frac{3}{4}\pi$',r'$\pi$',\
      			r'$\frac{5}{4}\pi$',r'$\frac{3}{2}\pi$',r'$\frac{7}{4}\pi$',r'$2\pi$',],fontsize = 20)
      plt.yticks(np.linspace(-1,1,9),np.linspace(-1,1,9),fontsize = 20)
      
      ax = plt.gca()
      ax.spines['top'].set_color('none')
      ax.spines['right'].set_color('none')
      ax.spines['bottom'].set_position(('data',0))
      ax.spines['left'].set_position(('data',0))
      
      plt.plot(x,y1,'-b',linewidth = 2, label = 'sine')
      plt.plot(x,y2,'-r',linewidth = 2, label = 'cosine' )
      plt.legend(loc = 'upper left',frameon = True,framealpha = 0.7,fontsize = 14)
      
      t = np.pi*3/4
      plt.plot([t,t],[np.sin(t),0],'--b',linewidth = 2)
      plt.scatter(t,np.sin(t),50,color = 'b')
      plt.annotate(r'$\sin(\frac{3\pi}{4})=\frac{\sqrt{2}}{2}$',(t,np.sin(t)),ha = 'left',xytext = (+50,+30), xycoords = 'data',\
      	textcoords='offset points',fontsize = 16, arrowprops = dict(arrowstyle = '->',connectionstyle = 'arc3,rad = 0.2'))
      plt.plot([t,t],[0,np.cos(t)],'--r',linewidth = 2)
      plt.scatter(t,np.cos(t),50,color = 'r')
      plt.annotate(r'$\cos(\frac{3\pi}{4})=-\frac{\sqrt{2}}{2}$',(t,np.cos(t)),ha = 'left',xytext = (-130,-50),  xycoords = 'data',\
      	textcoords='offset points',fontsize = 16, arrowprops = dict(arrowstyle = '->',connectionstyle = 'arc3,rad = 0.2'))
      
      plt.show()
      ```

      ![sin_cos_batter](http://poatdt87z.bkt.clouddn.com/sin_cos_better.png)

### 使用Axes 布局

可以使用plt.axes((x,y,w,h))创建一个新的坐标系，可以适用该方法绘制出更具有制订性的多子图。相对于subplot来讲这种方法可以设计出更加复杂的布局，因此参数也更加复杂。再绘制前应该画出草稿并计算各子图的坐标及宽高。

**注意：**

> 该函数的参数中x,y,w,h均为0-1的浮点数。代表所占figure的百分比。
>
> 使用坐标轴绘图各个图之间有叠加关系，后绘的图会遮住先前绘制的图像。

```python
import numpy as np
import matplotlib
from matplotlib import pyplot as plt
plt.figure(figsize = (16,9),dpi = 80)

plt.axes([.05,.65,.9, .3])
plt.xticks([])
plt.yticks([])
plt.text(.5,.5,'Axes1',ha = 'center',va = 'center',size = 16)

plt.axes([.05,.35,.55, .25])
plt.xticks([])
plt.yticks([])
plt.text(.5,.5,'Axes2',ha = 'center',va = 'center',size = 16)

plt.axes([.65,.05,.3, .55])
plt.xticks([])
plt.yticks([])
plt.text(.5,.5,'Axes3',ha = 'center',va = 'center',size = 16)

plt.axes([.05,.05,.25, .25])
plt.xticks([])
plt.yticks([])
plt.text(.5,.5,'Axes4',ha = 'center',va = 'center',size = 16)

plt.axes([.35,.05,.25, .25])
plt.xticks([])
plt.yticks([])
plt.text(.5,.5,'Axes5',ha = 'center',va = 'center',size = 16)

plt.show()
```

![axes](http://poatdt87z.bkt.clouddn.com/axes.png)

### 记号

使用Tick Locators来制定记号：

下面有为不同需求设计的一些 Locators。

| 类型              | 说明                                                         |
| :---------------- | :----------------------------------------------------------- |
| `NullLocator`     | No ticks. ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012569-1664-ticks-NullLocator.png) |
| `IndexLocator`    | Place a tick on every multiple of some base number of points plotted.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012569-4591-ticks-IndexLocator.png) |
| `FixedLocator`    | Tick locations are fixed.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012569-6368-ticks-FixedLocator.png) |
| `LinearLocator`   | Determine the tick locations.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012570-7138-ticks-LinearLocator.png) |
| `MultipleLocator` | Set a tick on every integer that is multiple of some base.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012570-8671-ticks-MultipleLocator.png) |
| `AutoLocator`     | Select no more than n intervals at nice locations.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012570-3960-ticks-AutoLocator.png) |
| `LogLocator`      | Determine the tick locations for log axes.  ![img](http://www.runoob.com/wp-content/uploads/2018/10/1540012571-8369-ticks-LogLocator.png) |

这些 Locators 都是 matplotlib.ticker.Locator 的子类，你可以据此定义自己的 Locator。以日期为 ticks 特别复杂，因此 Matplotlib 提供了 matplotlib.dates 来实现这一功能。



### 基础教程到此结束，高级教程后续更新。

