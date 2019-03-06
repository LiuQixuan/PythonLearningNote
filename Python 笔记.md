# Python 进阶笔记
***
[TOC]



***

## 函数式编程

- 高阶函数(参数里有函数类型)
>map/reduce(functools.reduce())
>filter
>sorted
- 返回函数（返回函数类型）
- 匿名函数（`lambda`）
- 装饰器（`@：有参装饰器、无参装饰器,functools.wraps(function)`）
- 偏函数（`functools.partor(function[,args,**kwords]`)

---
## 面向对象
### 变量
>1.静态字段
>2.普通字段(self.value)

###方法(存储在内存中)
>1.普通方法def func(self[,args])
>2.类方法(@classmethod def func(cls[,args]))
>3.静态方法(@staticmethod def func())

###属性（@property def func(self)）
>1.静态字段
>2.装饰类
>
>>经典装饰器
>>新装饰器
>>
>>>方法一
>>>继承object
>>>
>>>```python
>>>@property object.func
>>>@func.setter object.func = value
>>>@func.deleter del object.func
>>>```
>>>方法二
>>>创建property对象的静态字段
>>>```python
>>>pro = property(get_value(),set_value(),del_value(),__doc__)
>>>obj = Object()
>>>ov = obj.pro
>>>obj.pro = value
>>>del obj.pro
>>>obj.pro.__doc__
>>>```
>>>类的特殊成员
>
>- `__doc__` 表示类的描述信息
>
>- `__name__`类名
>
>- `__bases__`类的所有父类构成的元组:tuple,不包含该类的type (类名即type类型使用`(my_class,)`可获得该类名的元组）
>
>- `__mro__`类的继承顺序包含类本身<class '__main__.My_class'>, 
>
>- `__module__` 表示当前操作的对象在那个模块 packages.module
>
>- `__class__` 表示当前操作的对象的类 packages.module.class
>
>- `__init__()` 类的构造方法
>
>- `__del__()` 类的析构方法
>
>- `__call__()` 对象的方法 obj() self()
>
>- `__getattr__()`当访问obj不存在的属性时会调用该方法  
>
>    getattr(obj, name, value)  ==> obj.name 不存在该属性返回value
>
>    name是函数name()需要添加@property 描述符
>
>- `__dict__` 类或对象中的所有成员
>
>- `__str__` 将类格式化成字符串 print(obj) 时调用,即toString()方法
>
>- `__repr__` 将类格式化成字符串 print(obj) 时调用,和 `__str__` 的区别：更适合从编程语言上理解 
>  print(obj) 
>  [output:] class_name.method(self, arg1, arg2, ...)
>
>- `__getitem__` 用于索引操作[num]，获取数据
>
>- `__setitem__` 用于索引操作[num]，设置数据
>
>- `__delitem__` 用于索引操作[num]，删除数据
>>```python
>> class mydict(object):
>> def __getitem__(self, key):
>> return self.key
>> def __setitem__(self, key, value):
>> self.key = value
>> def __delitem__(self, key):
>> del self.key
>> obj = mydict()
>> result = obj[]
>> obj['key'] = value
>> del obj['key']
>>```
>> **实现切片操作**
>>`__getitem__(self, n)`传入的参数n 可能是int也可能是slice
>>
>> ```python
>> class Fib(object):
>> def __getiter__(self, n):
>> 	if isinstance(n, int):
>>        a, b = 1, 1
>>        for x in range(n):
>>            a, b = b, a + b
>>     	return a
>>    if isinstanece(n, slice):
>>        l = []
>>        slice.start = 0 if (slice.start is None)
>>        a, b = 1, 1
>>        for x in range(n.stop):
>>        	if (x >= n.start and (x - n.start)%n.step == 0):
>>            	l.append(a)
>>            a, b = b, a+b
>>        return l
>>        
>>
>> ```
>- `__getslice__` (self, i, j) obj[-1:1]
>
>- `__setslice__` (self, i, j, sequence) obj[0:1] = [11,22,33,44]
>
>- `__delslice__` (self, i, j) del obj[0:2]
>
>- `__iter__` 迭代器
>
>- `__next__` 配合`__iter__`实现类的interable属性
>
>- `__new__`方法`__new__(cls, name, bases, attrs)` 类准备将自身实例化时调用，在`__init__()`调用之前调用`__new__（）`，该方法是一个类方法@classmethod
>
>    cls：当前准备创建的类的对象:type
>
>    name：类的名字:str
>
>    bases：类继承的父类集合:class
>
>    attrs：类的方法集合:dict
>
>- `__metaclass__` 该属性定义一个类的元类，即表示类该有哪个类（元类）来实例化
### 创建类的两种方法
>1.普通方法
>```python
>class Object(object):
>def func(self):
>	print('hello world!')
>object = Object()
>```
>2.特殊方法（元类type构造对象）
>
>```python
>def func(self):
>print('Hello world!')
>object = type('Object', (object,), {'func':func})
>#arg1:str 类名 ;arg2:tuple 基类; arg3:dict 成员;
>```
>***类的创建过程***
>![类的创建过程](file:///C:/Users/LiuQixuan/Desktop/pypro/type_class.png)
>【CODE】
>
>```python
>class MyType(type):
>    def __init__(self, what, bases=None, dict=None):
>        super(MyType, self).__init__(what, bases, dict)
>
>    def __call__(self, *args, **kwargs):
>        obj = self.__new__(self, *args, **kwargs)
>        self.__init__(obj)
>class Foo(object):
>    __metaclass__ = MyType
>    def __init__(self, name):
>        self.name = name
>    def __new__(cls, *args, **kwargs):
>        return object.__new__(cls, *args, **kwargs)
># 第一阶段：解释器从上到下执行代码创建Foo类
># 第二阶段：通过Foo类创建obj对象
>obj = Foo()
>
>```
### 使用枚举类(枚举类不可比较大小，但是同一枚举类的成员可以做等值is / not is判断)
>```python
>from enum import Enum
>month = Enum('Mouth',('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))
>for name ,member in month.__members__.items():
>	print(f'{name}=>{member}=>{member.value}')
>```
### 定义枚举类
>```python
>from enum import Enum, unique
>@unique#unique装饰器帮助检查Enum内部字段，保证字段不重复
>class My_weekday(Enum):
>	Sun = 0
>	Mon = 1
>	Tue = 2
>	Wed = 3
>	Thu = 4
>	Fri = 5
>	Sat = 6 
>my_weekday = My_weekday()#my_weekday.Sun
>print(my_weekday.Sun)#my_weekday.Sun
>print(my_weekday['Sun'])#my_weekday.Sun
>print(my_weekday(0))#my_weekday.Sun
>print(my_weekday.Sun.value)#0
>for name, member in my_weekday.__members__.item():
>	print(f'{name} {member} {member.value}')
>【output】
>"""
>Sun  My_weekday.Sun 0
>Mon  My_weekday.Mon 1
>Tue  My_weekday.Tue 2
>Wed  My_weekday.Wed 3
>Thu  My_weekday.Thu 4
>Fri  My_weekday.Fri 5
>Sat  My_weekday.Sat 6
>"""
>```


## 高级面向对象

### 元类types
>动态地给对象添加方法(MethodType(func[, object/None], Object))
>```python
>from types import MethodType
>
>def func(self, value):
>	self.age = value
>class Student(object):
>	def __init__(self,name):
>		self.name = name
>student = Student('Bob')
>student.age_setter = MethodType(age_setter,func)
>student.age_setter(21)
>print(f'{student.name}is {student.age} years old.')
>```
>动态的给类添加方法
>```python
>def func(self, value):
>	self.age = value
>class Student(object):
>	def __init__(self,name):
>		self.name = name
>Student.age_setter = func
>Student.age_setter = MethodType(func, None, Student)
>student = Student('Bob')
>student.age_setter(21)
>print(f'{student.name}is {student.age} years old.')
>```
### 元类type构造对象
>```python
>def func(self):
>	print('Hello world!')
>object = type('Object', (object,), {'func':func})
>#arg1:str 类名 ;arg2:tuple 基类; arg3:dict('a' = a, 'b' = b...) 类变量/静态字段;
>```
### 使用Slot限制添加属性
>slot是一个特殊静态字段,tuple类型.slot只对当前类起作用，对其子类并不起作用
>```python
>class Student(object):
>		__slot__ = ('name', 'age')
>		def __init__(self, name, age):
>			super(Student,self).__init__()
>			self.name = name
>			self.age = age
>		@property
>		def name(self):
>			return self.name
>
>		@name.setter
>		def name(self,name):
>			self.name = name
>
>		@property
>		def age(self):
>			return self.age
>
>		@age.setter
>		def age(self,name):
>			self.age = age
>s1 = Student('Bill',21)
>s1.score = 89                [ERROR]:不能添加score字段
>```

### 装饰器
>一般装饰器（@decorate）
>描述符装饰器
>
>>实现了
>>```__get__() __set__() __del__()```
>>```@property @func.setter @func.deleter```
>>
>>>数据描述符（实现了get set）
>>>非数据描述符（只实现get 没有实现set)

### python垃圾回收机制
>- 引用计数器（当一个对象被引用机会增加其引用计数，当不被引用时减少引用计数，减少至0时在合适的时机下内存被回收）
>- 循环垃圾收集器（针对循环引用）
>- 手动内存回收 del obj.obj (将引用计数置零，只有最后引用该内存的对象释放后才执行析构函数__del__())




## python 异常（Exception）、调试（Debug）、回溯（Traceback)
### 异常（Exception）
>
>```python
>
>try:
>pass
>except Exception as e:
>raise
>else:
>pass
>finally:
>pass
>
>```
>
>#### 常见的异常：
>
>>| 异常名称       |描述              |
>>| ------------- | --------------- |
>>| BaseException | 所有异常K的基类 |
>>| SystemExit    | 解释器请求退出  |
>>| KeyboardInterrupt | 用户自行中断执行^C |
>>| Exception | 常规错误的基类 |
>>| StopIteration | 迭代器溢出 |
>>| GeneratorExit | 生成器发生异常后通知退出 |
>>| StandardError | 所有标准异常类的基类 |
>>| ArithmeticError | 所有数值计算错误的基类 |
>>| FloattingPointError | 浮点计算错误 |
>>| OverflowError | 数值运算溢出 |
>>| ZeroDivisionError | 除[,取模]by0 |
>>| AssertionError | 断言语句失败 |
>>| AttributeError | 对象缺失该属性 |
>>| EOFError | 没有内建输入，到达EOF标记 |
>>| EnvironmentError | 操作系统错误的基类 |
>>| IOError | 输入/输出操作失败 |
>>| OSError | 操作系统错误 |
>>| WindowsError | 系统调用失败 |
>>| ImportError | 导入模块/对象失败 |
>>| LookupError | 无效数据查询的基类 |
>>| IndexError | 序列中没有此索引 |
>>| KeyError | 映射中没有此键 |
>>| MemoryError | 内存溢出（对于Python解释起来说非致命） |
>>| NameError | 未声明/初始化对象 |
>>| UnboundLocalError | 访问未初始化的本地变量 |
>>| ReferenceError | 试图访问已被回收器回收的对象（弱引用） |
>>| RuntimeError | 一般运行时错误 |
>>| NotImplementedError | 尚未实现的方法 |
>>| SyntaxError | Python语法错误 |
>>| IndentationError | 缩进错误 |
>>| TabError | Tab和Space混用 |
>>| SystemError | 一般的解释器系统错误 |
>>| TypeError | 对类型无效的操作 |
>>| ValueError | 传入无效的参数 |
>>| UnicodeError | Unicode相关错误 |
>>| UnicodeDecodeError | Unicode解码时的错误 |
>>| UnicodeEncodeError | Unicode编码时的错误 |
>>| UnicodeTranslateError | Unicode转码时的错误 |
>>| Warning | 警告的基类 |
>>| DeprecationWarning | 关于被弃用的特性的警告 |
>>| FutureWarning | 关于构造将来语义会有改变的警告 |
>>| OverflowWarning | 旧的关于自动提升为长整型(long)的警告 |
>>| pendingDeprecationWarning | 关于特性将会被废弃的警告 |
>>| RuntimeWarning | 可疑的运行时行为的警告 |
>>| SysntaxWarning | 可疑语法的警告 |
>>| UserWarning | 用户代码生成的警告 |
>>
>
### 调试（Debug）
>
>#### 单元测试
>
>>单元测试的类在unittest包中使用时直接导入包`import unittest`.
>>
>>```python
>>import unittest
>>class TestClass(unitest.TestCase):
>>	def setUp(self):
>>        pass
>>    def tearDown(self):
>>        pass
>>    def test_init(self):
>>        self.assertEqual()
>>        self.assertTrue()
>>        self.assertRaises()
>>    def test_func1(self):
>>        pass
>>    def test_func2(self):
>>        pass
>>```
>#### 文档测试(doctest)
>>
>> Python的文档测试模块可以直接提取注释中的代码并执行
>>
>>```python
>>class Dict(dict):
>>    '''
>>    Simple dict but also support access as x.y style.
>>
>>    >>> d1 = Dict()
>>    >>> d1['x'] = 100
>>    >>> d1.x
>>    100
>>    >>> d1.y = 200
>>    >>> d1['y']
>>    200
>>    >>> d2 = Dict(a=1, b=2, c='3')
>>    >>> d2.c
>>    '3'
>>    >>> d2['empty']
>>    Traceback (most recent call last):
>>        ...
>>    KeyError: 'empty'
>>    >>> d2.empty
>>    Traceback (most recent call last):
>>        ...
>>    AttributeError: 'Dict' object has no attribute 'empty'
>>    '''
>>    def __init__(self, **kw):
>>        super(Dict, self).__init__(**kw)
>>
>>    def __getattr__(self, key):
>>        try:
>>            return self[key]
>>        except KeyError:
>>            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)
>>
>>    def __setattr__(self, key, value):
>>        self[key] = value
>>
>>if __name__=='__main__':
>>    import doctest
>>    doctest.testmod()
>>```
>
>
>
### 回溯（Traceback)
>代码
>以下代码功能相同
>```python
>import traceback
>
>traceback.print_exc()
>traceback.format_exc()
>traceback.print_exception(*ss.exc_info())
>
>```
## with 用法
>事前事后用with（前后文管理器）
>```python
>【version 1.0】
>file = open("/src/tmp.txt")
>data = file.read()
>file.close()  
>#可能会忘记关闭句柄
>#可能会出现异常
>【version 2.0】
>file = open("/src/tmp.txt")
>try:
>data = file.read()
>finally:
>file.close()
>#总体结构安全性都有提升
>【version 3.0 with】
>with open("/src/tmp.txt") as file:
>data = file.read()
>```
>
>with 对处理对象需要自定义`__enter__() __exit__()`方法
>
>```python
>class Sample:
>def __enter__(self):
>print('function:enter')
>return "SAMPLE"
>    def __exit__(self, type, value, trace):
>    	print('function:exit')
>def get_sample():
>return Sample()
>
>with get_sample() as sample:
>print(f'{sample}do somethings')
>
>
>[result:]
>function:enter
>SAMPLE do somethings
>function:exit
>
>class Sample:
>def __init__(self, value):
>self.num = value
>def __enter__(self):
>print('function:enter')
>return self
>    def __exit__(self, type, value, trace):
>    	print('function:exit')
>    	print('m_type:{type}\tm_value:{value}\ttrace:{trace})
>    def func(self, value):
>    	return self.num/value
>def get_sample(num):
>return Sample(num)
>
>with get_sample() as sample:
>print(f'{sample}do somethings')
>num = input("input a number:")
>sample.func(num)
>
>
>#执行顺序：
>#with 后面的函数/或type对象使用类的__init__()创建出一个对象,然后调用__enter__()方法将返回值赋给as 后的变量。在with执行完毕后调用类中的__exit__（）方法，清理或关闭句柄。
>```
>
>- `open`(*file*, *mode='r'*, *buffering=-1*, *encoding=None*, *errors=None*, *newline=None*, *closefd=True*, *opener=None*)
>
## f_string 处理`__str__，__repr__`
>
>- `__str __（）`和`__repr __（）`方法处理对象如何呈现为字符串，因此您需要确保在类定义中包含至少一个这些方法。如果必须选择一个，请使用`__repr __（）`，因为它可以代替`__str __（）`。
>- `__str __（）`返回的字符串是对象的非正式字符串表示，应该可读。`__repr __（）`返回的字符串是官方表示，应该是明确的。调用`str（）`和`repr（）`比直接使用`__str __（）`和`__repr __（）`更好。
>- 默认情况下，f字符串将使用`__str __（）`，但如果包含转换标志`!r`，则可以确保它们使用`__repr __（）`。
>
>```python
>f"{new_comedian}"
>'This __str__'
>f"{new_comedian!r}"
>'This __repr__'
>```
>
