---
title: Python科学计算
date: 2019-03-09 21:23:56
tags:

	- python
	- science conputing
toc: true
---
# Python 科学计算

---
[TOC]
---

## NumPy(MatLab 替代品之一)

>- 数组的算数和逻辑运算
>- 傅立叶变换和用于图形操作的例程
>-   与线性代数有关的操作。 NumPy 拥有线性代数和随机数生成的内置函数
frmemeta

## SciPy（科学计算）

>SciPy是一个开源的算法库和数学工具包。
>
>其包含最优化、线性代数、积分、插值、特殊函数、快速傅里叶变换、信号处理和图像处理、常微分方程求解和其他科学与工程常用的计算。

## Matplotlib（科学绘图）

>Matplotlib是Numpy的数值可视化包，它利用通用的图形用户界面工具包向应用程序嵌入式绘图提供接口。

<!--more-->

## NumPy

### NumPy Ndarray

NumPy 是用来处理数组的，在其内部可生成 Ndarray 对象表示数组。

ndarray 对象用于存放同类型元素的多维数组。

ndarray 中的每个元素在内存中都有相同存储大小区域。

ndarrary 内部构成

> 一个指向数据的指针
>
> 数据类型 dtype(描述数据在内存中固定大小的格子)
>
> 一个表示数组形状 (shape) 的元组 (表示各维度大小的元组)
>
> 一个跨度元组 (stride) (可为负数意义大致和切片类似)
>
> ![ndarray内部结构](http://www.runoob.com/wp-content/uploads/2018/10/ndarray.png)

numpy 创建 array
> `numpy.array(object, dtype = None,copy = True, order = None, subok = False， ndmin = 0)`
> 参数说明：
>
> | 名称   | 描述                                          |
> | ------ | --------------------------------------------- |
> | object | 数组或嵌套数列                                |
> | dtype  | 数组元素的类型                                |
> | copy   | 深拷贝                                        |
> | order  | 创建数组样式（C 为行，F为列，A任意(default)） |
> | subok  | 默认返回一个与基类类型一致的数组              |
> | ndmin  | 指定生成数组的最小维度                        |

eg:
>创建一维数组
> ```python
> import numpy as np
> a = np.array([1,2,3])
> print(a)
>```
>创建二维数组
>```python
>import numpy as np
> a = np.array([[1,2,3],[3,4,5]])
> print(a)
>```
>创建二维数组
>```python
>import numpy as np
> a = np.array([[1,2,3],[3,4,5]],order = F)
> print(a)
>```
>创建最小维度为二维的数组
>```python
> import numpy as np
> a = np.array([1,2,3],ndmin = 2)
> print(a)
> 【output】[[1,2,3]]
> ```
>创建数据类型为复数的数组
>```python
>import numpy as np
> a = np.array([1,2,3],dtype = complex,dmin = 2)
> print(a)
> 【output】[[1.+0.j,2.+0.j,3.+0.j]]
> ```
### NumPy数据类型
numpy 支持大量的数据类型，可与C语言的数据类型做参照

| 名称   | 描述                                                   | 字符代码                                               |
| ------ | ------------------------------------------------------ | ------------------------------------------------------ |
| bool_  | 布尔类型(True, False)                                  | b                                 |
| int_   | 默认整数类型(类比C语言的long->int32，int64)            | int         |
| intc  | 类比C语言的int->int32,int64                            | int                         |
| intp   | 用于索引的正数类型类比C语言的size_t->int32.int64       | int    |
| int8   | 8bit，1字节，类比于char(-128 to 127)                   | i1                 |
| int16  | 16bit整数(-32768 to 32767)                             | i2                           |
| int32  | 32bit整数(-2147483648 to 2147483647)                   | i3                 |
| int64  | 64bit整数(-9223372036854775808 to 9223372036854775807) | i4 |
| uint8  | 无符号8bit整数(0 to 255)                               | u1                             |
| uint16  | 无符号16bit整数(0 to 65535)                             | u2                           |
| uint32  | 无符号32bit整数(0 to 4294967295)                   | u3                 |
| uint64  | 无符号64bit整数(0 to 18446744073709551615) | u4 |
| float_  | float64类型简写 | f |
| float16 | 半精度浮点型 ->1 个符号位，5 个指数位，10 个尾数位 | f2 |
| float32 | 单精度浮点型 ->1 个符号位，8 个指数位，23 个尾数位 | f4 |
| float64 | 双精度浮点型 ->1 个符号位，11 个指数位，52 个尾数位 | f8 |
| complex_ | cpmplex128简写，128bit复数 | c16 |
| complex64 | 64bit复数 | c8 |
| complex128 | 128bit复数 | c16 |

| 符号         | 描述                                    |
| ------------ | --------------------------------------- |
| `'?'`        | boolean                                 |
| `'b'`        | (signed) byte                           |
| `'B'`        | unsigned byte                           |
| `'i'`        | (signed) integer                        |
| `'u'`        | unsigned integer                        |
| `'f'`        | floating-point                          |
| `'c'`        | complex-floating point                  |
| `'m'`        | timedelta                               |
| `'M'`        | datetime                                |
| `'O'`        | (Python) objects                        |
| `'S'`, `'a'` | zero-terminated bytes (not recommended) |
| `'U'`        | Unicode string                          |
| `'V'`        | raw data (`void`)                       |

| Build_In     | 等价                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| `int` | `int_`                                     |
| `bool` | `bool_`                                    |
| `float` | `float_`                                   |
| `complex` | `cfloat`                                   |
| `bytes` | `bytes_`                                   |
| `str` | `bytes_` (Python2) or `unicode_` (Python3) |
| `unicode`                                                    | `unicode_`                                 |
| `buffer`                                                     | `void`                                     |
| (all others)                                                 | `object_`                                  |

dtype 可取类型 np.bool_,np.int32,np.float_,np.complex128

*** 数据类型对象dtype ***

数据类型对象是用来描述与数组对应的内存区域如何使用

- 数据的类型
- 数据的大小
- 数据的字节顺序 (`‘<’:小端法(最小的存储在最小的地址，低位存前面，低位先存)，’>‘:大端法`)

构造dtype `np.dtype(object, align, copy)`

align（True/False）如果为 true，填充字段使其类似 C 的结构体

copy（True/False）复制 dtype 对象 ，如果为 False，则是对内置数据类型对象的引用

eg:

> ```python
> import numpy as np
> student = np.dtype([('name','S20'), ('age', 'i1'), ('marks', 'f4')]) 
> a = np.array([('abc', 21, 50),('xyz', 18, 75)], dtype = student) 
> print(student)
> print(a['name'])
> print(a['age'])
> print(a['marks'])
> ```
> 输出
> ```python
> [('name', 'S20'), ('age', 'i1'), ('marks', '<f4')]
> [b'abc' b'xyz']
> [21 18]
> [50. 75.]
> ```
>

### NumPy数组属性

数组的维度成为秩（rank), 一维数组 r=1，二维数组r=2...

每一个线性数组称为一个轴（axis）,也称为维度（dimensions）。秩是轴或维度的数量

axis表示轴，对于二维数组来说，axis = 0对列操作，axis = 1是对行操作。

NumPy比较重要的属性有：

| 属性              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| ndarray.ndim      | 秩，即轴的数量或维度的数量                                   |
| ndarray.shape     | 数组的维度，对于矩阵（二维数组）来说即行列数（n, m）         |
| ndarray.size      | 数组元素的总个数(n*m)                                        |
| ndarray.dtype     | ndarray 对象的类型                                           |
| ndarray.itemsizes | ndarray 每个元素的大小                                       |
| ndarray.flag      | ndarray 对象的信息                                           |
| ndarray.real      | ndarray 元素的实部                                           |
| ndarray.imag      | ndarray 元素的虚部                                           |
| ndarray.data      | 包含实际数组元素的缓冲区，一般通过数组的索引获得元素（可忽略） |

eg:

np.arange[^arange]

```python
import numpy as np
a = np.arange
```


[^arange]: arange和range

range返回list，arange返回numpy.ndarray。

都是以三点切片方式控制生成的数列。


```python
arange(start, end, step)
range(start, end, step)
```
但是arange的step可以是小数，其返回值数列元素类型也为float。

但是有一点类似，返回结果都不包括end。

ndarray.ndim

```python
import numpy as np
a = np.arange(24)
print(a.ndim) #1
b = np.array(a,shape(3,4,2))
print(b)
print(b.ndim) #3
```



ndarray.shape

```python
import numpy as np
a = n.array([[1,2,3],[4,5,6]])
print(a.shape) #(2, 3)
```

ndarray.reshape

注意:修改a.shape = shape或a.reshape()是返回一个视图，若返回的视图被修改，源数组也会发生改变。

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
b = a.reshape(3, 2)
print(b)
[[1, 2],[3, 4],[5, 6]]
a.shape = (3,2)
print(a)
[[1, 2],[3, 4],[5, 6]]
```

ndarray.itemsize

```python
import numpy as np
x = np.array([1,2,3,4,5,6],dtype = np.int8)
print(x.itemsize) #1
y = np.array([1,2,3,4,5],dtype = np.float64)
print(y.itemsize) #8
```

ndarray.flags

返回ndarray的对象信息

| 属性             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| C_CONTIGUOUS (C) | 数据是在一个单一的C风格的连续段中                            |
| F_CONTIGUOUS (F) | 数据是在一个单一的Fortran风格的连续段中                      |
| OWNDATA (O)      | 数组拥有它所使用的内存或从另一个对象中借用它                 |
| WRITEABLE (W)    | 数据区域可以被写入，将该值设置为 False，则数据为只读         |
| ALIGNED (A)      | 数据和所有元素都适当地对齐到硬件上                           |
| UPDATEIFCOPY (U) | 这个数组是其它数组的一个副本，当这个数组被释放时，原数组的内容将被更新 |

```python
import numpy as np
x = np.array([1, 2, 3, 4, 5])
print(x.flags)
# 
C_CONTIGUOUS : True
F_CONTIGUOUS : True
OWNDATA : True
WRITEABLE : True
ALIGNED : True
WRITEBACKIFCOPY : False
UPDATEIFCOPY : False
```

### NumPy创建数组

1. b = np.array([...] ,dtype = ...)

2. numpy.empty(shape,dtype = float, order = 'C')

   | 参数  | 描述                                                         |
   | ----- | ------------------------------------------------------------ |
   | shape | 数组形状                                                     |
   | dtype | 数据类型，可选                                               |
   | order | 有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |

   ```python
   import numpy as np
   x = np.empty([1,2],dtype = int)
   print(x)
   #未初始化所以是随机值
   #未初始化所以是随机值
   [[-5968 18343]
    [32766     0]
    [-1344 18343]]
   [Finished in 0.3s]
   ```

3. numpy.zeros(shape, dtype = np.float, order = 'C')

   ```python
   import numpy as np
   x = np.zeros([3,2], dtype = np.int)
   print(x)
   y = np.zeros([2,3], dtype = [('x','i4'),('y','i4'),('z', 'i4')])
   print(y)
   #
   [[0 0]
    [0 0]
    [0 0]]
   [[(0, 0) (0, 0) (0, 0)]
    [(0, 0) (0, 0) (0, 0)]]
   ```

4. numpy.ones(shape, dtype = np.int4)

   ```python
   import numpy as np
   x = np.ones([3,2], dtype = np.int4)
   print(x)
   #
   [[1 1]
    [1 1]
    [1 1]]
   ```

### NumPy从已有的数组创建数组

**numpy.asarray方法**

numpy.asarray 类似numpy.array，但是numpy.asarray的参数只有三个。

`numpy.asarray(a, dtype = None, order = None)`

| 参数  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| a     | 任意形式的输入参数，可以是，列表, 列表的元组, 元组, 元组的元组, 元组的列表，多维数组 |
| dtype | 数据类型，可选                                               |
| order | 可选，有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |

将数列转换成 ndarray

```python
import numpy as np
x = [1, 2, 3]
a = np.asarray(x)
print(a)
#
[1, 2, 3]
```

将元组转化为ndarray

```python
import numpy as np
x = (1, 2, 3)
a = np.asarray(x)
print(a)
#
[1, 2, 3]
```

将元组列表转换成ndarray

```python
import numpy as np
x = [(1, 2, 3), (4, 5, 6)]
a = np.asarray(x)
print(a)
#
[[1,2,3],
 [4,5,6]]
```

**numpy.frombuffer方法**

numpy.frombuffer可以实现动态数组，其接受buffer输入参数，以流的形式读入转化成ndarray对象

```python
numpy.frombuffer(buffer, dtype = float, count = -1, offset = 0)
```

| 参数   | 描述                                     |
| ------ | ---------------------------------------- |
| buffer | 可以是任意对象，会以流的形式读入。       |
| dtype  | 返回数组的数据类型，可选                 |
| count  | 读取的数据数量，默认为-1，读取所有数据。 |
| offset | 读取的起始位置，默认为0。                |

```python
import numpy as np
s = b'Hellow,world!'
a = np.frombuffer(s,dtype = 'S1')
print(a)
#
[b'H' b'e' b'l' b'l' b'o' b'w' b',' b'w' b'o' b'r' b'l' b'd' b'!']
```

**NumPy.fromiter方法**

numpy.fromiter方法可从可迭代对象中建立ndarray 对象，返回一维数组

`np.fromer(iterable, dtype, count = -1)`

| 参数     | 描述                                   |
| -------- | -------------------------------------- |
| iterable | 可迭代对象                             |
| dtype    | 返回数组的数据类型                     |
| count    | 读取的数据数量，默认为-1，读取所有数据 |

```python
import numpy as np 
l = range(9)
i = iter(l)
x = np,fromiter(i, dtype = np.int4)
print(x)
#
[0 1 2 3 4 5 6 7 8]
```

### NumPy从数值范围创建数组

使用**numpy.arange**方法生成ndarray对象。

`numpy.arange(start, stop, step, dtype)`

| 参数    | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| `start` | 起始值，默认为`0`                                            |
| `stop`  | 终止值（不包含）                                             |
| `step`  | 步长，默认为`1`(step 可以为浮点小数)                         |
| `dtype` | 返回`ndarray`的数据类型，如果没有提供，则会使用输入数据的类型 |

eg:

x = np.arange(5)

#[0,1,2,3,4]

x = np.arange(5, dtype = float)

print(x)

#
[0.  1.  2.  3.  4.]

```python
x =np.arange(10, 20, 2)
print(x)
#
[10 12 14 16 18]
```

**numpy.linspace**函数用于创建一个一维数组，数组是一个等差数列构成的。

`np.linspace(start, stop, num = 50, endpoint = True, retstep = False, dtype = None)`

| 参数     | 描述                                     |
| -------- | ---------------------------------------- |
| start    | 序列起始值                               |
| stop     | 序列终止值                               |
| num      | 要生成等步长样本的数量，默认值为50       |
| endpoint | Ture代表包含stop,反之不包含。默认为True  |
| retstep  | Ture代表生成的数组会显示间距，反之不显示 |
| dtype    | ndarray的数据类型                        |

```python
import numpy as np
a = np.linsapce(1, 10, 50,retstep = True)
print(a)
#
(array([ 1.        ,  1.59183673,  2.18367347,  2.7755102 ,  3.36734694,
        3.95918367,  4.55102041,  5.14285714,  5.73469388,  6.32653061,
        6.91836735,  7.51020408,  8.10204082,  8.69387755,  9.28571429,
        9.87755102, 10.46938776, 11.06122449, 11.65306122, 12.24489796,
       12.83673469, 13.42857143, 14.02040816, 14.6122449 , 15.20408163,
       15.79591837, 16.3877551 , 16.97959184, 17.57142857, 18.16326531,
       18.75510204, 19.34693878, 19.93877551, 20.53061224, 21.12244898,
       21.71428571, 22.30612245, 22.89795918, 23.48979592, 24.08163265,
       24.67346939, 25.26530612, 25.85714286, 26.44897959, 27.04081633,
       27.63265306, 28.2244898 , 28.81632653, 29.40816327, 30.        ]), 0.5918367346938775)
```

**NumPy.logspace**函数用于创建一个一维数组，数组是一个等比数列构成的。

`numpy.logspace(star, stop, num = 50, endpoint, base = '10.0', dtype)`

| `start`    | 序列的起始值为：base ** start                                |
| ---------- | ------------------------------------------------------------ |
| `stop`     | 序列的终止值为：base ** stop。如果`endpoint`为`true`，该值包含于数列中 |
| `num`      | 要生成的等步长的样本数量，默认为`50`                         |
| `endpoint` | 该值为 `ture` 时，数列中中包含`stop`值，反之不包含，默认是True。 |
| `base`     | 对数 log 的底数。                                            |
| `dtype`    | `ndarray` 的数据类型，默认float                              |

```python
import numpy as np
a = np.logspace(1,10,dtype = np.int64)
print(a)
#
[         10          15          23          35          54          82
         126         193         294         449         686        1048
        1599        2442        3727        5689        8685       13257
       20235       30888       47148       71968      109854      167683
      255954      390693      596362      910298     1389495     2120950
     3237457     4941713     7543120    11513953    17575106    26826957
    40949150    62505519    95409547   145634847   222299648   339322177
   517947467   790604321  1206792640  1842069969  2811768697  4291934260
  6551285568 10000000000]
```

```python
import numpy as np
a = np.logspace(1,10,num = 10,base = 2)
print(a)
#
[   2.    4.    8.   16.   32.   64.  128.  256.  512. 1024.]
```

### NumPy 切片和索引

numpy的ndarray 可以像list那样通过切片和索引操作或访问

```python
import numpy as np
a = np.arange(8)
s = slice(0,5,2)
b = a[s]
c = a[:5:2]
print(a,b,c,sep = '\n')
#
[0 1 2 3 4 5 6 7]
[0 2 4]
[0 2 4]
```

python list多维数组下标访问

```python
a = [
    [[1,2,4],[4,5,6]],
    [[7,8,9],[10,11,12]],
    [[13,14,15],[16,17,18]]
]
print(a[2][1][2])
#
18
```

numpy ndarray多维数组下标访问

```python
import numpy as np
a = np.arange(64).shape(4,4,4)
b = a[2,2,2]
print(b)
```



多维数组操作

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6],[7,8,9]])
print(a[:2,:2])
#
[[1 2]
 [4 5]]
```

用`...`代替全维度`::`

```python
import numpy as np
a = np.arange(64)
b = a.reshape(4,4,4)
print(b[...,2,2])
#
[[[ 0  1  2  3]
  [ 4  5  6  7]
  [ 8  9 10 11]
  [12 13 14 15]]

 [[16 17 18 19]
  [20 21 22 23]
  [24 25 26 27]
  [28 29 30 31]]

 [[32 33 34 35]
  [36 37 38 39]
  [40 41 42 43]
  [44 45 46 47]]

 [[48 49 50 51]
  [52 53 54 55]
  [56 57 58 59]
  [60 61 62 63]]]

[10 26 42 58]
```

### NumPy 高级索引

- 整数数组索引

  使用二维数组分别表示行列值

  输出矩阵四角元素的值。

  ```python
  import numpy as np
  x = np.arange(12).reshape(4,3)
  print(x)
  print(x[[0,0,3,3],[0,2,0,2]])
  #
  [[ 0  1  2]
   [ 3  4  5]
   [ 6  7  8]
   [ 9 10 11]]
  [0 2 9 11]
  
  y = x[0:-2:-1,[0:-2:-1]]
  
  rows = np.array([[0,0],[3,3]]) 
  cols = np.array([[0,2],[0,2]]) 
  y = x[rows,cols]  
  print(y)
  #
  [[0 2]
   [9 11]
  ```

  ```python
  import numpy as np
   
  a = np.array([[1,2,3], [4,5,6],[7,8,9]])
  b = a[1:3, 1:3]
  c = a[1:3,[1,2]]
  d = a[...,1:]
  print(b)
  print(c)
  print(d)
  
  #
  b = [5 6 8 9]
  c = [[5 6][8 9]]
  d = [[2 3][5 6][8 9]]
  ```

- 布尔索引

  使用布尔切片过滤掉ndarray小于等于5的值

  ```python
  import numpy as np
  x = np.array([[0,1,2],[3,4,5],[6,7,8],[9,10,11]])
  print(x[x>5])
  #
  [ 6  7  8  9 10 11]
  ```
  使用布尔切片过滤掉ndarray等于NaN的值
  ```python
  import numpy as np
  a = np.array(np.nan,1,2,np.nan,4)
  print(a[~isnan(a)])
  [ 1 2 4]
  ```
  使用布尔切片保留复数

  ```python
  import numpy as np
  a = np.array([1, 2+6j, 5, 3.5+5j])
  print(a[np.iscomplex(a)])
  #
  [2. +6.j 3.5+5.j]
  ```

- 花式索引

  使用整数数组进行索引

  一维数组为第一维度

  ```python
  import numpy as np
  x = np.arange(32).reshape(8,4)
  print(x[[4,2,1,7]])
  #
  [[16 17 18 19]
   [ 8  9 10 11]
   [ 4  5  6  7]
   [28 29 30 31]]
  ```

  传入倒序一维数组

  ```python
  import numpy as np
  x = np.arange(32).reshape(8,4)
  print(x)
  print(x[[-4,-2,-1,-7]])
  #
  [[16 17 18 19]
   [24 25 26 27]
   [28 29 30 31]
   [ 4  5  6  7]]
  ```

  传入两个索引数组

  ```python
  import numpy as np
  x = np.arange(32).reshape(8,4)
  print(x)
  print(x[np.ix_([1,5,3,2],[0,3,2])])
  #
  [[ 4  7  6]
   [20 23 22]
   [12 15 14]
   [ 8 11 10]]
  ```

  ### 广播数组（Broadcast）

  ndarray 做算术运算时要求两个ndarray同型即a.shape=b,shape

  但是遇到在末尾维度相同但是前面不相同时即会自动触发广播机制。

  ```python
  import numpy as np
  a = np.arange(12).reshape(4,3)
  b = np.arange(12,24).reshape(4,3)
  c = np.asarray([10,20,30])
  print(a,b,c,sep = '\n')
  print(f'a,b同型直接运算："\n"{a+b}')
  print(f'a,c不同维度，a自动出发广播然后运算："\n"{a+c}')
  #
  [[ 0  1  2]
   [ 3  4  5]
   [ 6  7  8]
   [ 9 10 11]]
  [[12 13 14]
   [15 16 17]
   [18 19 20]
   [21 22 23]]
  [10 20 30]
  a,b同型直接运算：
  [[12 14 16]
   [18 20 22]
   [24 26 28]
   [30 32 34]]
  a,c不同维度，a自动出发广播然后运算：
  [[10 21 32]
   [13 24 35]
   [16 27 38]
   [19 30 41]]
  ```

  广播原理：

  ![broadcase](http://www.runoob.com/wp-content/uploads/2018/10/image0020619.gif)

  **np.tile(x,y,z,...)方法**：tile即瓷砖，即将该数组进行横向纵向复制

  ```python
  import numpy as np
  mat = np.tile(np.array([[1,2,3],[4,5,6]]),(2,3))
  print(mat)
  #
  [[1 2 3 1 2 3 1 2 3]
   [4 5 6 4 5 6 4 5 6]
   [1 2 3 1 2 3 1 2 3]
   [4 5 6 4 5 6 4 5 6]]
  ```

  即broadcast 执行过程：

  ```python
  import numpy as np
  a = np.array([[0,0,0],
                [10,10,10],
                [20,20,20],
                [30,30,30]
  			])
  b = np.array([1,2,3])
  c = a+b
  d = a+np.tile(b,(4,1))
  print(c,d,sep = '\n')
  #
  [[ 1  2  3]
   [11 12 13]
   [21 22 23]
   [31 32 33]]
  [[ 1  2  3]
   [11 12 13]
   [21 22 23]
   [31 32 33]]
  ```

  **广播的规则:**

- 让所有输入数组都向其中形状最长的数组看齐，形状中不足的部分都通过在前面加 1 补齐。

- 输出数组的形状是输入数组形状的各个维度上的最大值。

- 如果输入数组的某个维度和输出数组的对应维度的长度相同或者其长度为 1 时，这个数组能够用来计算，否则出错。

- 当输入数组的某个维度的长度为 1 时，沿着此维度运算时都用此维度上的第一组值。

  **简单理解：**对两个数组，分别比较他们的每一个维度（若其中一个数组没有当前维度则忽略），满足：

- 数组拥有相同形状。

- 当前维度的值相等。

- 当前维度的值有一个是 1。

  若条件不满足，抛出 **"ValueError: frames are not aligned**或者

  **ValueError: operands could not be broadcast together with shapes"** 异常。

### NumPy迭代数组

Numpy提供了numpt.nditer用来灵活访问数组元素


```python
import numpy as np

a = np.arange(6).reshape(3,2)

print(a)

for x in np.nditer(a):
	print(x,end = ',')
print('\n')
for x in np.nditer(a.T):
	print(x,end = ',')
print('\n')
for x in np.nditer(a.T.copy(order = 'C')):
	print(x,end = ',')
print('\n')
for x in np.nditer(a.T,order = 'C'):
	print(x,end = ',')
print('\n')
for x in np.nditer(a.T,order = 'F'):
	print(x,end = ',')
print('\n')
#
[[0 1]
 [2 3]
 [4 5]]
0,1,2,3,4,5,

0,1,2,3,4,5,

0,2,4,1,3,5,

0,2,4,1,3,5,

0,1,2,3,4,5, #反反得反
```
**ndarray.T**表示ndarray的转置

```python
import numpy as np
 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print ('原始数组是：') 
print (a) 
print ('\n') 
print ('原始数组的转置是：') 
b = a.T #b是a的转置
print (b) 
print ('\n') 
print ('以 C 风格顺序排序：') 
c = b.copy(order='C')  
print (c)
for x in np.nditer(c):  
    print (x, end=", " )
print  ('\n') 
print  ('以 F 风格顺序排序：')
c = b.copy(order='F')  
print (c)
for x in np.nditer(c):  
    print (x, end=", " )
#
原始数组是：
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]


原始数组的转置是：
[[ 0 20 40]
 [ 5 25 45]
 [10 30 50]
 [15 35 55]]


以 C 风格顺序排序：
[[ 0 20 40]
 [ 5 25 45]
 [10 30 50]
 [15 35 55]]
0, 20, 40, 5, 25, 45, 10, 30, 50, 15, 35, 55, 

以 F 风格顺序排序：
[[ 0 20 40]
 [ 5 25 45]
 [10 30 50]
 [15 35 55]]
0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55,
```
**修改数组中元素的值**

op_flags = ['readwrite']

```python
import numpy as np

a = np.arange(0,60,5).reshape(3,4)
print('原始数据：\n',a)
for x in np.nditer(a, op_flags = ['readwrite']):
	x[...]*=2
print('现在数据：\n',a)
#
原始数据：
 [[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]
现在数据：
 [[  0  10  20  30]
 [ 40  50  60  70]
 [ 80  90 100 110]]
```

**使用外部循环**(不重要)

np.nditer()有很多参数其中flags参数可取下列值

| 参数            | 描述                                           |
| --------------- | ---------------------------------------------- |
| `c_index`       | 可以跟踪 C 顺序的索引                          |
| `f_index`       | 可以跟踪 Fortran 顺序的索引                    |
| `multi-index`   | 每次迭代可以跟踪一种索引类型                   |
| `external_loop` | 给出的值是具有多个值的一维数组，而不是零维数组 |

```python
import numpy as np 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print ('原始数组是：')
print (a)
print ('\n')
print ('修改后的数组是：')
for x in np.nditer(a, flags =  ['external_loop'], order =  'F'):  
   print (x, end=", " )
```



**使用广播循环**

如果两个数组可以广播，nditer组合对象能够同时迭代它们。（广播条件，见上广播规则)

```python
import numpy as np
a = np.arange(0,60,5).reshape(3,4)
b = np.array([11,22,33,44],dtype = 'int')
for x,y in np.nditer([a,b],order = 'C'):
    print(f'{x}:{y}',end = ',')
#
0:11,5:22,10:33,15:44,20:11,25:22,30:33,35:44,40:11,45:22,50:33,55:44,
```




### NumPy数组操作

- 修改数组形状(reshape)

  `ndarray.reshape`可以重定义数组行列

  `ndarray.flat`是一个数组元素迭代器，可用for in 访问迭代器内的值

  `ndarray.flatten`返回一份数组拷贝，对拷贝进行修改并不会改变原始数组

  > ndarray.flatten(order = 'C')#按照C（即按行）展开
  >
  > ndarray.flatten(order = 'F')#按照F（即按列）展开

  `numpy.ravel(ndarray, order = 'C')`展平数组元素，返回引用修改会引起原来的ndarray发生改变

  > order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'K' -- 元素在内存中的出现顺序

- 翻转数组(transpose)
  `numpy.transpose(ndarray, axes)`翻转数组（相当于ndarray.T）

  axes：维度

  `numpy.rollaxis(ndarray,axis,start)`函数向后滚动一个特定的轴到特定的位置

  axis：要向后滚动的轴

  start = 0：默认为0表示完整的滚动


```python
import numpy as np

a = np.arange(27).reshape([3,3,3])
print(a)

print(np.rollaxis(a,2))

print(np.rollaxis(a,2,1))
print(np.rollaxis(a,1,0))
#
[[[ 0  1  2]
  [ 3  4  5]
  [ 6  7  8]]

 [[ 9 10 11]
  [12 13 14]
  [15 16 17]]

 [[18 19 20]
  [21 22 23]
  [24 25 26]]]
yzx
[[[ 0  3  6]
  [ 9 12 15]
  [18 21 24]]

 [[ 1  4  7]
  [10 13 16]
  [19 22 25]]

 [[ 2  5  8]
  [11 14 17]
  [20 23 26]]]
xzy
[[[ 0  3  6]
  [ 1  4  7]
  [ 2  5  8]]

 [[ 9 12 15]
  [10 13 16]
  [11 14 17]]

 [[18 21 24]
  [19 22 25]
  [20 23 26]]]
yxz
[[[ 0  1  2]
  [ 9 10 11]
  [18 19 20]]

 [[ 3  4  5]
  [12 13 14]
  [21 22 23]]

 [[ 6  7  8]
  [15 16 17]
  [24 25 26]]]
```

​	`numpy.swapaxes(ndarray,axis1,axis2)`交换数组的两个轴

```python
import numpy as np

a = np.arange(27).reshape([3,3,3])
print(a)
print(np.swapaxes(a,2,1))
print(np.swapaxes(a,1,0))
print(np.swapaxes(a,2,0))
#
[[[ 0  1  2]
  [ 3  4  5]
  [ 6  7  8]]

 [[ 9 10 11]
  [12 13 14]
  [15 16 17]]

 [[18 19 20]
  [21 22 23]
  [24 25 26]]]
xzy
[[[ 0  3  6]
  [ 1  4  7]
  [ 2  5  8]]

 [[ 9 12 15]
  [10 13 16]
  [11 14 17]]

 [[18 21 24]
  [19 22 25]
  [20 23 26]]]
yxz
[[[ 0  1  2]
  [ 9 10 11]
  [18 19 20]]

 [[ 3  4  5]
  [12 13 14]
  [21 22 23]]

 [[ 6  7  8]
  [15 16 17]
  [24 25 26]]]
 zyx
[[[ 0  9 18]
  [ 3 12 21]
  [ 6 15 24]]

 [[ 1 10 19]
  [ 4 13 22]
  [ 7 16 25]]

 [[ 2 11 20]
  [ 5 14 23]
  [ 8 17 26]]]
```

- 修改数组维度(broadcast,broadcast_to,expand_dims,squeeze)

  | 函数           | 描述                       |
  | -------------- | -------------------------- |
  | `broadcast`    | 产生模仿广播的对象         |
  | `broadcast_to` | 将数组广播到新形状         |
  | `expand_dims`  | 扩展数组的形状             |
  | `squeeze`      | 从数组的形状中删除一维条目 |

  `numpy.broadcast `用于模仿广播对象，它返回一个对象（numpy.broadcast object），该对象封装了将一个数组广播到另一个数组的结果。

  

  `numpy.broadcast_to(array, shape, subok)` 函数将数组广播到新形状。它在原始数组上返回只读视图。 它通常不连续。 如果新形状不符合 NumPy 的广播规则，该函数可能会抛出ValueError。

  

  ``numpy.expand_dims(arr, axis)`` 函数通过在指定位置插入新的轴来扩展数组形状。

  `numpy.squeeze(arr,axis = 0)`函数从给定数组的形状中删除一维的条目

  

- 连接数组

  | 函数          | 描述                           |
  | ------------- | ------------------------------ |
  | `concatenate` | 连接沿现有轴的数组序列         |
  | `stack`       | 沿着新的轴加入一系列数组。     |
  | `hstack`      | 水平堆叠序列中的数组（列方向） |
  | `vstack`      | 竖直堆叠序列中的数组（行方向） |

`numpy.concatenate((a1, a2, ...), axis = 0)`

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
# 两个数组的维度相同
 
print ('沿轴 0 连接两个数组：')
print (np.concatenate((a,b)))
print ('\n')
 
print ('沿轴 1 连接两个数组：')
print (np.concatenate((a,b),axis = 1))
#
第一个数组：
[[1 2]
 [3 4]]
第二个数组：
[[5 6]
 [7 8]]
沿轴 0 连接两个数组：
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
沿轴 1 连接两个数组：
[[1 2 5 6]
 [3 4 7 8]]
[Finished in 0.3s]
```

`numpy.stack(arrays, axis)`沿新的轴连接数组，新建一个维度

`numpy.hstack(ndarray1,ndarray2)`水平堆叠生成数组

`numpy.vstack(ndarray1,ndarray2)`垂直堆叠生成数组

- 分割数组

| 函数     | 数组及操作                             |
| -------- | -------------------------------------- |
| `split`  | 将一个数组分割为多个子数组             |
| `hsplit` | 将一个数组水平分割为多个子数组（按列） |
| `vsplit` | 将一个数组垂直分割为多个子数组（按行） |

`numpy.split(ary, indices_or_sections, axis)`沿特定轴将数组分割为子数组
>`ary`：被分割的数组
>`indices_or_sections`：果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭）
>`axis`：沿着哪个维度进行切向，默认为0，横向切分。为1时，纵向切分

```python
import numpy as np
 
a = np.arange(9)
 
print ('第一个数组：')
print (a)
print ('\n')
 
print ('将数组分为三个大小相等的子数组：')
b = np.split(a,3)
print (b)
print ('\n')
#[array([0,1,2]),array([3,4,5]),array([6,7,8])]
 
print ('将数组在一维数组中表明的位置分割：')
b = np.split(a,[4,7])
print (b)
#[array([0,1,2,3],array([4,5,6]),array([7,8])]
```

`numpy.hsplit `函数用于水平分割数组，通过指定要返回的相同形状的数组数量来拆分原数组，用法和split类似。

`numpy.vsplit` 沿着垂直轴分割，其分割方式与split用法相同

- 数组元素的添加和删除

| 函数     | 元素及描述                               |
| -------- | ---------------------------------------- |
| `resize` | 返回指定形状的新数组                     |
| `append` | 将值添加到数组末尾                       |
| `insert` | 沿指定轴将值插入到指定下标之前           |
| `delete` | 删掉某个轴的子数组，并返回删除后的新数组 |
| `unique` | 查找数组内的唯一元素                     |

`numpy.resize(arr, shape)` np.resize(arr,shape)等价于arr.resize(shape)

`numpy.append(arr, values, axis=None)`函数在数组的末尾添加值。 追加操作会分配整个数组，并把原来的数组复制到新数组中。 此外，输入数组的维度必须匹配否则将生成ValueError。

```python
import numpy as np
 
a = np.array([[1,2,3],[4,5,6]])
print (a)
#
[[1 2 3]
 [4 5 6]]
 print ('向数组添加元素：')
print (np.append(a, [7,8,9]))
#未传递axis数组会展开
[1 2 3 4 5 6 7 8 9]
 
print ('沿轴 0 添加元素：')
print (np.append(a, [[7,8,9]],axis = 0))
#
[[1 2 3]
 [4 5 6]
 [7 8 9]] 
print ('沿轴 1 添加元素：')
print (np.append(a, [[5,5,5],[7,8,9]],axis = 1))
#
[[1 2 3 5 5 5]
 [4 5 6 7 8 9]]
```

`numpy.insert(arr, obj, values, axis)`函数在给定索引之前，沿给定轴在输入数组中插入值。

```python
import numpy as np
 
a = np.array([[1,2],[3,4],[5,6]])
print (a)
#
[[1 2]
 [3 4]
 [5 6]]
print ('未传递 Axis 参数。 在插入之前输入数组会被展开。')
print (np.insert(a,3,[11,12]))
#
[1 2 3 11 12 4 5 6]
print ('传递了 Axis 参数。 会广播值数组来配输入数组。')
print ('沿轴 0 广播：')
print (np.insert(a,1,[11],axis = 0))
#自动广播
[[1 2]
 [11 11]
 [3 4]
 [5 6]]
print ('沿轴 1 广播：')
print (np.insert(a,1,11,axis = 1))
[[1 11 2]
 [3 11 4]
 [5 11 6]]
```

`Numpy.delete(arr, obj, axis)`函数返回从输入数组中删除指定子数组的新数组。 与 insert() 函数的情况一样，如果未提供轴参数，则输入数组将展开。
>  `arr`：输入数组
>   `obj`：可以被切片，整数或者整数数组，表明要从输入数组删除的子数组
>   `axis`：沿着它删除给定子数组的轴，如果未提供，则输入数组会被展开

```python
a = np.array([1,2,3,4,5,6,7,8,9,10])
print (np.delete(a, np.s_[::2]))
#np.s_[：：]切片
```

`numpy.unique(arr, return_index, return_inverse, return_counts)`函数用于去除数组中的重复元素。

>arr：输入数组，如果不是一维数组则会展开
>return_index：如果为true，返回新列表元素在旧列表中的位置（下标），并以列表形式储
>return_inverse：如果为true，返回旧列表元素在新列表中的位置（下标），并以列表形式储
>return_counts：如果为true，返回去重数组中的元素在原数组中的出现次数

### 位运算(bitwise按位)

`numpy.bitwise_and(a,b)`与运算

`numpy.bitwise_or(a,b)`或运算

`numpy.invert()`非

`left_shift(a,width = 8)`按位左移

`right_shift(a,width = 8)`按位右移

### 字节转换函数

`ndarray.byteswap(True/False)`对ndarray中的元素进行大小端字节转换

### 字符串函数

| 函数           | 描述                                       |
| -------------- | ------------------------------------------ |
| `numpy.char.add(['s1'],['s2'])` | 对两个数组的逐个字符串元素进行连接         |
| `numpy.char.multiply(['s'],mult)` | 返回按元素多重连接后的字符串               |
| `numpy.char.center('str',width = Num,fillchar = '*')` | 居中字符串                                 |
| `numpy.char.capitalize('str')` | 将字符串第一个字母转换为大写               |
| `numpy.char.title('str')` | 将字符串的每个单词的第一个字母转换为大写   |
| `numpy.char.lower('str')` | 数组元素转换为小写                         |
| `numpy.char.upper('str')` | 数组元素转换为大写                         |
| `numpy.char.split('str',sep = '*')` | 指定分隔符对字符串进行分割，并返回数组列表 |
| `numpy.char.splitlines('str')` | 返回元素中的行列表，以换行符分割           |
| `numpy.char.strip('str','char')` | 移除元素开头或者结尾处的特定字符           |
| `numpy.char.join(['char1','char2'],['str1',str2])` | 通过指定分隔符来连接数组中的元素           |
| `numpy.char.replace('str','s1',s2)` | 使用新字符串s2替换字符串中的所有子字符串s1 |
| `numpy.char.decode()`     | 数组元素依次调用`str.decode`               |
| `numpy.char.encode()`     | 数组元素依次调用`str.encode`               |

### 数学函数

 **三角函数**

​	NumPy 提供了标准的三角函数：numpy.sin()、numpy.cos()、numpy.tan()

```python
import numpy as np
 
a = np.array([0,30,45,60,90])
print ('不同角度的正弦值：')
# 通过乘 pi/180 转化为弧度  
print (np.sin(a*np.pi/180))
print ('\n')
print ('数组中角度的余弦值：')
print (np.cos(a*np.pi/180))
print ('\n')
print ('数组中角度的正切值：')
print (np.tan(a*np.pi/180))
```

numpy.arcsin，numpy.arccos，和 numpy.arctan 函数返回给定角度的 sin，cos 和 tan 的反三角函数

**舍入函数**

​	numpy.around(a,decimals)四舍五入

	>a: 数组
	>
	>decimals: 舍入的小数位数。 默认值为0。 如果为负，整数将四舍五入到小数点左侧的位置（即 numpy.around(192.586,decimals = -1） 190)

​	numpy.floor()向下舍入

​	numpy.ceil()向上舍入

### 运算函数

NumPy 算术函数包含简单的加减乘除: `numpy.add()，numpy.subtract()，numpy.multiply() 和 numpy.divide()`

`numpy.reciprocal() `函数返回参数逐元素的倒数

```python
import numpy as np 
 
a = np.array([0.25,  1.33,  1,  100])  
print ('调用 reciprocal 函数：')
print (np.reciprocal(a))
#
调用 reciprocal 函数：
[4.        0.7518797 1.        0.01     ]
```

`numpy.power() `函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组中相应元素的幂。

`numpy.mod()` 计算输入数组中相应元素的相除后的余数。 函数 numpy.remainder() 也产生相同的结果。

### 统计函数

`numpy.amin(arr,axis = None)`用于计算数组中的元素沿指定轴的最小值。axis 默认为None，即将arr展开。

`numpy.amax(arr,axis = None) `用于计算数组中的元素沿指定轴的最大值。用法与numpy.amin相似。

numpy.ptp(arr,axis = None)函数计算数组中元素最大值与最小值的差（最大值 - 最小值）。

`numpy.percentile(a,q,axis = None，keepdims = False)`百分位数是统计中使用的度量，表示小于这个值的观察值的百分比。 函数numpy.percentile()接受以下参数。

> a：数组
>
> q：要计算的百分位数[0-100]
>
> axis：维度
>
> keepdims：保持原数组的dims

`numpy.median(arr, axis = None)` 函数用于计算数组 a 中元素的中位数（中值）

`numpy.mean(arr, axis = None) `函数返回数组中元素的算术平均值。 (算术平均值是沿轴的元素的总和除以元素的数量。)

`numpy.average(arr, axis = None,weights = wts)` 函数根据在另一个数组中给出的各自的权重计算数组中元素的加权平均值。不指定权重默认为1，此时和mean结果相同

```python
import numpy as np 
 
a = np.array([1,2,3,4])  
print ('我们的数组是：')
print (a)
print ('\n')
print ('调用 average() 函数：')
print (np.average(a))
print ('\n')
# 不指定权重时相当于 mean 函数
wts = np.array([4,3,2,1])  
print ('再次调用 average() 函数：')
print (np.average(a,weights = wts))
print ('\n')
# 如果 returned 参数设为 true，则返回权重的和  
print ('权重的和：')
print (np.average([1,2,3,  4],weights =  [4,3,2,1], returned =  True))
```

`numpy.std(arr,axis = None)`标准差，等价于 `sqrt(numpy.mean(arr-numpy.mean(arr,axis = None)**2))`

`numpy.var(arr,axis = None)`方差，等价于`numpy.mean(arr-numpy.mean(arr,axis = None)**2)`

### NumPy排序

`numpy.sort(ndarray,axis,kind,order) `

axis 默认为None这时数组会展开；kind 可以选quicksort(defult),mergesort,heapsort

order如果数组包含字段则是要排序的字段

```python
import numpy as np

dtp = [('name','S10'),('age',np.int8)]
a = np.array([("bob",12),('alis',13),('john',11)],dtype = dtp)
print(a)
print('sort by name:',np.sort(a,order = 'name'))
print('sort by age:',np.sort(a,kind = 'quicksort',order = 'age'))
#
[(b'bob', 12) (b'alis', 13) (b'john', 11)]
sort by name: [(b'alis', 13) (b'bob', 12) (b'john', 11)]
sort by age: [(b'john', 11) (b'bob', 12) (b'alis', 13)]
```

`numpy.argsort(ndarray,axis = -1,kind = 'quicksort',order = None)`函数返回排序后的索引值。

`numpy.lexsort(tuple)` 按照多个序列排序。返回排序后的索引值，可使用 for 遍历。

`numpy.msort(ndarray)` = `numpy.sort(a,axis = 0)`按照第一个轴排序

`sort_complex(ndarray)` 对复数数列按照先实部后虚部进行排序。

`partition(ndarray, kth[, axis, kind, order])` 指定一个数对数组进行分区(即快速排序的步骤)

kth接收tuple表示的区间，np.partition(arr,(1,3))即小于1的放最前面，[1,3)放中间，大于3的放最后。

`argpartition(ndarray,kth[, axis, kind, order])` 返回partition结果中元素的索引

`numpy.argmax()`返回给定轴最大元素的索引

`numpy.argmin()`返回给定轴最小元素的索引

`numpy.nonzero()`返回数组中非零元素的索引

`numpy.where()`返回满足条件的元素的索引（参照布尔切片）

`numpy.extract()`根据条件返回满足条件的元素

```python
import numpy as np
x = np.arange(9).reshape(3,3)
condition = np.mod(x,2) == 0#返回一个bool_numpy.ndarray
print(condition)
print(np.extract(condition,x))#print(x[x%2==0])
#
[[ True False  True]
 [False  True False]
 [ True False  True]]
[0 2 4 6 8]
```



### 矩阵库

NumPy 中包含一个矩阵库 numpy.matlib,操作对象和返回对象都是矩阵，而不是ndarray。

`numpy.matlib.empty(shape, dtype = np.float, order)`返回一个新的矩阵

`numpy.matlib.zeros(shape, dtype = np.float, order)`返回一个初始值为0的新矩阵

`numpy.matlib.ones(shape, dtype = np.float, order)`返回一个初始值为1的新矩阵

`numpy.matlib.eye(n, M = n, k, dtype = np.float)`返回一个主对角线为1的对角矩阵。(k为对角线偏置，为0则为主对角线，小于0向下偏，大于0向上偏)

`numpy.matlib.identity()`返回给定大小的单位阵。

>`np.matlib.identity(5, dtype = np.float)`等价于`numpy.matlib.eye(5,k=0,dtype = np.float)`

`numpy.matlib.rand(n,M,dtype = np.float)`返回一个n维矩阵，数值随机（值小于1大于0）

matlib总是一个二维数组，其本质是ndarray。二者之间可以直接赋值或深拷贝。



### 线性代数

NumPy内置了线性代数库linalg。

| 函数          | 描述                             |
| ------------- | -------------------------------- |
| `dot`         | 两个数组的点积，即元素对应相乘。 |
| `vdot`        | 两个向量的点积，高维数组自动降维 |
| `inner`       | 两个数组的内积                   |
| `matmul`      | 两个数组的矩阵积                 |
| `determinant` | 数组的行列式                     |
| `solve`       | 求解线性矩阵方程                 |
| `inv`         | 计算矩阵的乘法逆矩阵             |

`numpy.dot(a, b, out = None)`两个向量的矢量积

>a : ndarray 数组
>
>b : ndarray 数组
>
>out : ndarray, 可选，用来保存dot()的计算结果
>
>```python
>import numpy as np
>import numpy.linalg
>import numpy.matlib
>a = np.arange(1,7).reshape(3,2,order = 'F')
>b = np.arange(1,7).reshape(2,3,order = 'C')
>print(a,b,sep = '\n')
>n = np.dot(a,b)
>print(n)
>m = np.dot(b,a)
>print(m)
>#
>[[1 4]
> [2 5]
> [3 6]]
>[[1 2 3]
> [4 5 6]]
>[[17 22 27]
> [22 29 36]
> [27 36 45]]
>[[14 32]
> [32 77]]
>```

`numpy.vdot(a, b)`两个向量的数量积在计算高维数量积时，先把高维降到一维，然后进行数量积运算。

`numpy.inner(ndarray)`一维ndarray内积运算，高维数组为对应维度上的内积运算。

对于多维数组相当：

```python
import numpy as np 
a = np.arange(1,5).reshape(2,2)
b = np.arange(5,9).reshape(2,2)
print (a,b,np.inner(a,b),sep = '\n')
print(np.dot(a,b))
#
[[1 2]
 [3 4]]
[[5 6]
 [7 8]]
inner()
[[17 23]
 [39 53]]
dot()
[[19 22]
 [43 50]]
inner运算类似于
[a11*b11+a12*b12,a11*b21+a12*b22]
[a21*b11+a22*b12,a21*b21+a22*b22]
```

`numpy.matmul(a, b, out = None)`返回矩阵乘积，高于二维视为存在最后两个索引的矩阵的栈，若有一个为一维，则横向广播，然后再进行乘积，最后反横向广播。

```python
import numpy as np 
a = np.array([[1,2],[3,4]])
b = np.array([[2,2],[3,3]])
c = np.array([2,3])
print(np.matmul(a,c))
print(np.matmul(a,b))
#
[ 8 18]
[[ 8  8]
 [18 18]]
```

`numpy.linalg.det(ndarray)`计算输入矩阵的行列式的值。

`numpy.linalg.solve(ndarray1,ndarray2)`计算增广矩阵的解。

```python
import numpy as np 
import numpy.linalg

a = np.array([2,2,-1,1,-2,4,5,8,-1]).reshape(3,3)
b = np.array([6,3,27])
print(np.linalg.solve(a,b))
#
[1. 3. 2.]
```



`numpy.linalg.inv(ndarray)`计算可逆矩阵的逆矩阵。

```python
import numpy as np 
import numpy.linalg

print(np.linalg.inv(np.array([1,2,-1,-3]).reshape(2,2)))
#
[[ 3.  2.]
 [-1. -1.]]
```

### 副本和视图

副本即拷贝，在内存中重新划出一块区域把源数据拷贝一份，修改副本内的内容源数据不会同时修改。

视图本身上还是源数据，只是改变了形状(shape)，修改视图会导致源数据发生变化。reshape,ravel,切片返回的都是视图，

**视图一般发生在：**

- 1、numpy 的切片操作返回原数据的视图。
- 2、调用 ndarray 的 view() 函数产生一个视图。

**副本一般发生在：**

- Python 序列的切片操作，调用deepCopy()函数。
- 调用 ndarray 的 copy() 函数产生一个副本。

注意：对于numpy.ndarray对象来说，简单的赋值（a = b）不会引起产生副本。

修改视图的形状不会改变原数组的形状
