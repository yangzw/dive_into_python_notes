#Dive Into Python

##Chapter 1
nothing to say

##Chapter 2
###2.2 函数声明
1. Python既是*动态类型语言*(不使用显示数据类型声明)，又是*强类型语言*(需要明确的类型转换)

###2.3文档化函数

```python
    def function(para):
		"""this function aims to do
		something"""
```
doc string 必须是函数要定义的**第一个**内容
###2.4万物皆对象
1. 模块导入的搜索路径:sys.path;sys模块是用c写的
2. 函数也为对象，所有函数都有一个__doc__属性，返回doc string

###2.6测试模块

```python
	if __name__ == "__main__":
```
如果import模块，那么`__name__`的值通常为文件名，不带路径和扩展名；如果直接运行模块，则是`__main__`

##Chapter 3. 内置数据类型
###3.1 Dictionary
1. 无序
2. 大小写敏感
3. 混用数据类型

###3.2 List
1. 负数索引理解：`list[-n] == list[len(list) - n]`
2. 切片
3. 增加元素：append/insert/extend
	* extend与append区别：extend连接list,append插入任何值，就算是系数是list
4. 搜索：index/ `if 'c' in list`
5. 删除:remove() 一次删除一个/ pop()删除最后一个，并返回该值
6. list可以+ 和 *

###3.3Tuple
1. 一个Tuple即一个不可变list,支持分片
2. 没有index方法，有in查看元素是否存在
3. tuple速度比list快；对不需要改变的数据写保护；可以做dic的keys
4. 定义一个只有一个元素的tuple时，元素后的逗号是必须的

###3.4. 变量声明
1. 变量不需要显示声明，第一次赋值时产生。
2. 一次赋多值

###3.6映射list
`li = [elem*2 for elem in list]`

###3.7list连接与分割
1. jion只能用于元素是字符串的list
2. split,可选系数表分割次数

##Chapter 4自省的威力
自省是指代码可以查看内存中以对象形式存在的其它

###4.2 可选参数和命名参数
调用函数时唯一必须做的事情就是为每一个必备参数指定值 

###4.3内置函数
1. type
2. str() 强制转换成字符串， 可以作用于任何数据类型，甚至是None, 都能得到'None'
3. dir 函数返回任意对象的属性和方法列表
4. callable 函数，它接收任何对象作为参数，如果参数对象是可调用的，返回True，否则返回False
5. type,str等内置函数都包含在__buidin__这个特殊的模块中

###4.4 通过getattr获得对象引用
1. getattr(object, "attribute")等价于object.attribute;如果object是一个模块的话，那么attribute可能是定义在模块中的任何东西：函数、类或者全局变量；如果object是内置数据类型，得到的是方法
2. getattr作为一个分发者;statsout模块定义了三个函数:`output_html`,`output_text`,`output_xml`

```python
	import statsout
	def output(data, format="text"):
    	output_function = getattr(statsout, "output_%s" % format, statsout.output_text)
    	return output_function(data)
```
最后一个为getattr的可选参数，是一个缺省返回值

###4.5过滤列表
`[mapping-expression for element in source-list if filter-expression]`

###4.6 and 和 or 的特殊性质
1. 如果and逻辑演算的值为假，则返回第一个假值；如果为真，则返回最后一个真值
2. or返回第一个真值或者最后一个假值
3. and-or技巧： bool and a or b, 类似bool ? a : b,但如果a的值为假，则不会正确工作。安全工作方法：`(bool and [a] or [b])[0]

###4.7使用lambda函数
1. 可以将lambda赋予一个变量进行调用
2. lambda 函数在布尔环境中总是为真。(这并不意味这 lambda 函数不能返回假值。

`'some string'.ljust(spacing)` :ljust 用空格填充字符串以符合指定的spacing长度.

##第五章对象和面向对象
###5.3类的定义
1. 子类不会自动调用父类的方法，需要显示调用.__init__方法也是。  __init__方法从不返回一个值
2. self 必须作为每个方法的第一个参数

###5.4类的实例化
3. 创建一个实例只需要调用一个类就行。
4. 内存回收：引用计数变为0以后，python自动销毁实例;   ?循环引用问题？

###5.5 UserDic一个封装类
1. update:字典复制器,合并
2. python没有函数重载
3. 建议尽量在__init__方法中将所有的数据属性赋初值 
4. copy模块可以拷贝任何的python对象。在父类定义copy函数时，因为不知道时自己还是子类调用copy，所以得判断__class__。当时子类调用时，则用copy模块

###5.6专用类方法
1. 专用方法是在特殊情况下或当使用特别语法时由 Python 替你调用的:__getitem__/ __setitem__等;专用方法可以被子类覆盖
2. __repr__/__cmp__/__len__/__delitem__

###5.8类属性介绍
1. 一个类属性在任何实例之前就有效了。类属性既可以通过直接对类的引用，也可以通过对类的任意实例的引用来使用。
2. python中的类属性相当与java中的静态变量，数据属性相当与实例变量

###私有函数
1. python函数、类方法或者属性名字开头以两个下划线开头，但不是结束,则它是私有的。专有方法是公用的.
2. 严格的说， python的私有还是能被外部访问。

##第六章异常和文件处理
###6.1异常处理
1. try...except...[else...] try没有发生异常时，else里面的执行;raise 抛出异常;无论try还是except,finally:总是会执行的代码

###6.2 文件对象
1. open/file()返回一个对象。fd.tell()//tell()方法返回打开文件的当前位置

###6.4 sys.modules
1. python类都有一个内置的类属性 __module__, 它定义了这个类的模块的名字 

###6.5目录
1. os.path: join,expanduser,split,splitext(文件名和扩展名分开);path封装了平台之间的不同;isfile,isdir;normcase
2. os.listdir:返回目录内容的list
3. glob模块的glob方法支持通配符

##第7章正则表达式
1. re模块
2. 松散型正则表达式:忽略空白符and忽略注释(指的是传给search的pattern),并添加re.VERBOSE参数: re.search(pattern, string, re.VERBOSE)

##第8章HTML处理
###8.2 sgmllib.py介绍
1. SGMLParse类. SGMLParser将HTML分为:开始标记/结束标记/字符引用/实体引用/注释/处理指令/声明/文本数据
2. SGMLParse类只是一个消费者，只负责分解。应该定义其子类，定义相应的方法
3. python处理list比字符串快
4. locals 和globals: 命名空间; locals 返回的只是拷贝，而globals不是
5. 基于dictionary的字符串格式化
```python
	params = {'exam1':'ddd','exam2':'kkk'}
	print "%(exam1)s is %(exam2)s" % params
```
