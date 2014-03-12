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
###4.5