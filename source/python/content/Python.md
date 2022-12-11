+++
lastmod = "2022-12-11 10:49:48"
categories = ["Python"]
draft = false
toc = true
+++

## Help {#help}


### list pkg {#list-pkg}

```sh

# 1)list pkg
help("modules")
```


### install lib in anaconda {#install-lib-in-anaconda}

```sh

# 2)instll lib in anadonda
  a.Anaconda Navigator->Environments->search packages
  b.Anaconda Prompt->pip install xxx
  c.Anaconda Prompt->conda install xxx
  d.pycharm->Terminal->pip install xxx
  test :python -c "import **; **.test()"
```


### cmdline {#cmdline}

```sh

# 3)cmdline
PATH #D:\Program Files\JetBrains\Anaconda3\condabin
conda info --envs
#base                  *  D:\Program Files\JetBrains\Anaconda3
activate base
```


### jupyter {#jupyter}

```sh

# 4)jupyter
C:\Users\SWH\.jupyter\jupyter_notebook_config.py
#c.NotebookApp.notebook_dir = 'E:/Refinement/Python/jupyter'
```


### python3 {#python3}

```sh

# 5)python3
print('this is 1\r', end='')	#\r 清除上次输出； end='' 输出不换行
python2
print 'this is 1\r',			#\r 清除上次输出,  逗号   输出不换行，
```


### version {#version}

```sh

# 6)verson
cmd->python3-:[MSC v.1927 64 bit (AMD64)] on win32 #64bit
python --version	#Python 3.8.6
```


### where {#where}

```sh

>>>where python
C:\Users\SWH\AppData\Local\Microsoft\WindowsApps\python.exe
D:\Program Files\JetBrains\Anaconda3\pkgs\python-3.8.3-he1778fa_2\python.exe

>>>import sys
>>>sys.executable
'C:\\Users\\SWH\\AppData\\Local\\Microsoft\\WindowsApps\\PythonSoftwareFoundation.Python.3.8_qbz5n2kfra8p0\\python.exe'
```


## Tool {#tool}


### python2 to python3 {#python2-to-python3}

```sh
# 1)python2 to python3
#D:\Program Files\JetBrains\Anaconda3\Tools\scripts\2to3.py
Python 2to3.py -w demo.py	#generate demo.py.bak(python2) ,demo.py changed(python3)
```


### pyinstaller {#pyinstaller}

```sh
# 2)pyinstaller
pyinstaller -w -F pk_test.py	#-w 去掉 win 下的黑窗口 -F 打包依赖包
win 和 linux 下打包命令一样
```


### freeze {#freeze}

```sh
pip freeze > requirements.txt	#生成当前项目的依赖配置文件，此文件中的内容包含了整个项目的依赖
pip download -d packages/ -r requirements.txt 将系统外的依赖下载到 packages 目录
```


### debug {#debug}

```sh

debug(){
# 1)print()
# 2)assert n != 0, 'n is zero!'	#表达式 n != 0 应该是 True，否则，根据程序运行的逻辑，后面的代码肯定会出错
# 3)logging
  #允许指定记录信息的级别，有 debug，info，warning，error 等几个级别
  # 当我们指定 level=INFO 时，logging.debug 就不起作用了
  # 指定 level=WARNING 后，debug 和 info 就不起作用了。
  # logging 的另一个好处是通过简单的配置，一条语句可以同时输出到不同的地方，比如 console 和文件。
# 4)pdb
  python -m pdb err.py
  (Pdb) l	#查看代码
  (Pdb) n	#单步执行
  (Pdb) p s	查看变量 s 的值
  (Pdb) q

# 5)pdb.set_trace()
import pdb
s = '0'
n = int(s)
pdb.set_trace() # 运行到这里会自动暂停

  p s #查看变量，或者用命令 c 继续运行
  c 	#继续执行
# 6)IDE
visual studio code
pycharm

  }
```


## Str {#str}


### str-init {#str-init}

```sh

str_int(){
#内建的 isinstance 函数可以判断一个变量是不是字符串
isinstance("123",str) Out:Ture

>>> int('123')	#123
>>> int(12.34)	#12
>>> float('12.34')	#12.34
>>> str(1.23)	#'1.23'
>>> str(100)	#'100'
>>> bool(1)		#True
>>> bool('')	#False

print("I'm %s. I'm %d year old" % ('Vamei', 99))
}
```


### len {#len}

```sh
_len(){
#获取字符串长度
>>> a='http://c.biancheng.net'
>>> len(a)
22

#获取字节长度
>>> str1 = "人生苦短，我用 Python"
>>> len(str1.encode())	#utf-8
27

>>> str1 = "人生苦短，我用 Python"
>>> len(str1.encode('gbk'))	#gbk
20
}
```


### slices {#slices}

```sh

slices(){
list/tuple

L[0:3]	#索引 0，1，2，正好是 3 个元素,3 不取
L[:3]

L[-2:]	#倒数 2 个值

L[:10:2]	#前 10 全值，每两个取值
L[::5]		#所有隔 5 取值

[:]		#所有取值

#字符串也可以切片操作
}
```


### split {#split}

```sh

_split(){
str.split(sep,maxsplit)
#sep：用于指定分隔符，可以包含多个字符。此参数默认为 None，表示所有空字符，包括空格、换行符“\n”、制表符“\t”等;
  #当字符串中有连续的空格或其他空字符时，都会被视为一个分隔符对字符串进行分割
#maxsplit：可选参数，用于指定分割的次数，最后列表中子串的个数最多为 maxsplit+1。如果不指定或者指定为 -1，则表示分割次数没有限制。
}
```


### join {#join}

```cfg

newstr = str.join(iterable)
#str：用于指定合并时的分隔符；

>>> list = ['c','biancheng','net']
>>> '.'.join(list)
'c.biancheng.net'

>>> dir = '','usr','bin','env'
>>> type(dir)
<class 'tuple'>
>>> '/'.join(dir)
'/usr/bin/env'

```


### find index {#find-index}

```cfg

_find_index(){

str.find(sub[,start[,end]])
str.index(sub[,start[,end]])

#sub：表示要检索的目标字符串；
start：表示开始检索的起始位置。如果不指定，则默认从头开始检索；
#end：表示结束检索的结束位置。如果不指定，则默认一直检索到结尾。
>>> str = "c.biancheng.net"
>>> str.find('.')	#首次出现 “.” 的位置索引
1

>>> str = "c.biancheng.net"
>>> str.find('.',2,-4)
-1	#索引（2，-4）之间的字符串为“biancheng”，由于其不包含“.”，因此 find() 方法的返回值为 -1。

${同 find() 方法类似，不同之处在于，当指定的字符串不存在时，index() 方法会抛出异常。}
>>> str = "c.biancheng.net"
>>> str.index('z')
Traceback (most recent call last):
  File "<pyshell#49>", line 1, in <module>
    str.index('z')
ValueError: substring not found

${它是从右边开始检索}
str.find(sub[,start[,end]])
str.index(sub[,start[,end]])s

}
```


### l/r/center just {#l-r-center-just}

```cfg
_ljust_rjust_center(){

# 1）S.ljust(width[, fillchar])
width：表示包括 S 本身长度在内，字符串要占的${总长度}；
#fillchar：作为可选参数，用来指定填充字符串时所用的字符，默认情况使用空格。

${rjust() 方法是向字符串的左侧填充指定字符，从而达到右对齐文本的目的}
${center() 字符串方法与 ljust() 和 rjust() 的用法类似}

# 2）str.format
{:<x}表左对齐
{:>x}为右对齐，
{:^x}为居中），
#少于 x 位自动补齐（默认为空格补齐）
#这里值得注意的是，x也可以作为变量代入:

utf-8 中中文占用 3 个字节，GBK 中占用了 2 个字节

print('[{str:<{len}}x'.format(str=name+']',len=22-len(name.encode('GBK'))+len(name)))
print('[{str:<{len}}\tx'.format(str=name+']',len=22-len(name.encode('GBK'))+len(name)))
name：变量
len	：长度
x	：
\t	：解决 0.5-1 个字符的问题，可能中文不是等宽字体
len=22:预期的输出长度
-len(name.encode('GBK'))+len(name)))	：将汉字折算成 1 长输出长度
}
```


### strip {#strip}

```cfg

_strip(){
${特殊字符，指的是制表符（\t）、回车符（\r）、换行符（\n）}
#strip()：删除字符串前后（左右两侧）的空格或特殊字符。
#lstrip()：删除字符串前面（左边）的空格或特殊字符。
#rstrip()：删除字符串后面（右边）的空格或特殊字符。
${Python 的 str 是不可变的（不可变的意思是指，字符串一旦形成，它所包含的字符序列就不能发生任何改变），
因此这三个方法只是返回字符串前面或后面空白被删除之后的副本，并不会改变字符串本身。}

str.strip([chars])
#str 表示原字符串，
#[chars] 用来指定要删除的字符，可以同时指定多个，如果不手动指定，则默认会删除空格以及制表符、回车符、换行符等特殊字符。

}
```


### title lower upper {#title-lower-upper}

```cfg

_title_lower_upper(){
1)title() 方法用于将字符串中每个单词的首字母转为大写，其他字母全部转为小写
2)lower() 方法用于将字符串中的所有大写字母转换为小写字母
3)upper() 用于将字符串中的所有小写字母转换为大写字母
${以上 3 个方法都仅限于将转换后的新字符串返回，而不会修改原字符串。}
}

_start_end_with(){
str.startswith(sub[,start[,end]])
str.endswith(sub[,start[,end]])
#方法用于检索字符串是否以指定字符串开头/结尾，如果是返回 True；反之返回 False。
  sub：要检索的子串；
  start：指定检索开始的起始位置索引，如果不指定，则默认从头开始检索；
    end：指定检索的结束位置索引，如果不指定，则默认一直检索在结束。
}
```


### formate {#formate}

```cfg

_format(){

str.format(args)
#str 用于指定字符串的显示样式；args 用于指定要进行格式转换的项，如果有多项，之间有逗号进行分割。
创建显示样式模板时，需要使用{}和：来指定占位符，其完整的语法格式为：
{ [index][ : [ [fill] align] [sign] [#] [width] [.precision] [type] ] }	#格式中用 [] 括起来的参数都是可选参数，即可以使用，也可以不使用

cat <<EOF
ndex：指定：后边设置的格式要作用到 args 中第几个数据，数据的索引值从 0 开始。如果省略此选项，则会根据 args 中数据的先后顺序自动分配。
fill：指定空白处填充的字符。注意，当填充字符为逗号(,)且作用于整数或浮点数时，该整数（或浮点数）会以逗号分隔的形式输出，例如（1000000 会输出 1,000,000）。
align：指定数据的对齐方式
  <	数据左对齐。
  >	数据右对齐。
  =	数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对数字类型有效。
  ^	数据居中，此选项需和 width 参数一起使用。
sign：指定有无符号数
  +		正数前加正号，负数前加负号。
  -		正数前不加正号，负数前加负号。
  空格	正数前加空格，负数前加负号。
  #		对于二进制数、八进制数和十六进制数，使用此参数，各进制数前会分别显示 0b、0o、0x 前缀；反之则不显示前缀。
width：指定输出数据时所占的宽度。
.precision：指定保留的小数位数。

type：指定输出数据的具体类型
s	对字符串类型格式化。
d	十进制整数。
c	将十进制整数自动转换成对应的 Unicode 字符。
e/E 转换成科学计数法后，再格式化输出。
g/G	自动在 e 和 f（或 E 和 F）中切换。
b	将十进制数自动转换成二进制表示，再格式化输出。
o	将十进制数自动转换成八进制表示，再格式化输出。
x/X	将十进制数自动转换成十六进制表示，再格式化输出。
f/F	转换为浮点数（默认小数点后保留 6 位），再格式化输出。
%	显示百分比（默认显示小数点后 6 位）。
EOF
  }

```


### encode {#encode}

```cfg

_encode(){
#在 Python 中，有 2 种常用的字符串类型，分别为 str 和 bytes 类型，其中 str 用来表示 Unicode 字符，bytes 用来表示二进制数据。
///str 类型和 bytes 类型之间就需要使用 encode() 和 decode() 方法进行转换。

encode() 用于将 str 类型转换成 bytes 类型，这个过程也称为${“编码”};
>>> str = "C 语言中文网"
>>> str.encode('GBK')
b'C\xd3\xef\xd1\xd4\xd6\xd0\xce\xc4\xcd\xf8'

#使用 encode() 方法对原字符串进行编码，不会直接修改原字符串，如果想修改原字符串，需要重新赋值
decode() 方法用于将 bytes 类型的二进制数据转换为 str 类型，这个过程也称为${“解码”}。
>>> str = "C 语言中文网"
>>> bytes=str.encode()
>>> bytes.decode()
'C 语言中文网'
   }
```


### dir_help {#dir-help}

```sh

_dir_help(){

#dir() 函数用来列出某个类或者某个模块中的全部内容，包括变量、方法、函数和类等
dir(obj)	#表示要查看的对象。obj 可以不写，此时 dir() 会列出当前范围内的变量、方法和定义的类型。

${ Python 标准库中，以__开头和结尾的方法都是私有的，不能在类的外部调用。}
${使用 help() 查看某个函数的用法时，函数名后边不能带括号，例如将上面的命令写作 help(str.lower())就是错误的}	>>> help(str.lower)
}

```


### iterate {#iterate}

```cfg

it  erate(){
1)
>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> for key in d:
...     print(key)
...
a
c
b

2)
>>> for ch in 'ABC':
...     print(ch)
...
A
B
C

3)for value in d.values()
4)cat <<EOF
默认情况下，dict 迭代的是 key。
  如果要迭代 value，可以用 for value in d.values()
  同时迭代 key 和 value，用 for k, v in d.items()
EOF

5)[d for d in os.listdir('.')] # os.listdir 可以列出文件和目录

6)>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
['y=B', 'x=A', 'z=C']

7)if ... else
>>> [x for x in range(1, 11) if x % 2 == 0]
[2, 4, 6, 8, 10]

>>> [x if x % 2 == 0 else -x for x in range(1, 11)]
[-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]
${在一个列表生成式中，for 前面的 if ... else 是表达式，而 for 后面的 if 是过滤条件，不能带 else}
}

list_gen(){
1)>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

2)>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

3)>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
}

```


### generator {#generator}

```cfg

generator(){
L = [x * x for x in range(10)]	#lsit
g = (x * x for x in range(10))	#generator
  #generator 保存的是算法，每次调用 next(g)，就计算出 g 的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出 StopIteration 的错误。
  #如果一个函数定义中包含 yield 关键字，那么这个函数就不再是一个普通函数，而是一个 generator：
  ${generator 和函数的执行流程不一样。
  函数是顺序执行，遇到 return 语句或者最后一行函数语句就返回。\
  而变成 generator 的函数，在每次调用 next()的时候执行，遇到 yield 语句返回，再次执行时从上次返回的 yield 语句处继续执行}
}

```


### iterator {#iterator}

```cfg

iterator(){
#直接作用于 for 循环的对象统称为可迭代对象：Iterable;可以使用 isinstance()判断一个对象是否是 Iterable 对象：
#被 next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。;可以使用 isinstance()判断一个对象是否是 Iterator 对象：
            Iterable	Iterator
(x for x in range(10))	Y			Y
[]						Y			N
{}						Y			N
'abc'					N			N

生成器都是 Iterator 对象，但 list、dict、str 虽然是 Iterable，却不是 Iterator。
${把 list、dict、str 等 Iterable 变成 Iterator 可以使用 iter()函数：}
>>> isinstance(iter([]), Iterator)	#True
>>> isinstance(iter('abc'), Iterator)	#True

#为什么 list、dict、str 等数据类型不是 Iterator？
#这是因为 Python 的 Iterator 对象表示的是一个数据流，Iterator 对象可以被 next()函数调用并不断返回下一个数据，直到没有数据时抛出 StopIteration 错误。
          }
```


### fun {#fun}

```cfg

___Fun___(){}

map(){
#接收两个参数，一个是函数，一个是 Iterable，map 将传入的函数依次作用到序列的每个元素，并把结果作为新的 Iterator 返回
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]

    }
```


### reduce {#reduce}

```cfg

reduce(){
#reduce 把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce 把结果继续和序列的下一个元素做累积计算
EG. reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

    }

```


### filter {#filter}

```cfg

filter(){
#也接收 一个函数和一个序列;filter()把传入的函数依次作用于每个元素，然后根据返回值是 True 还是 False 决定保留还是丢弃该元素。
#filter()函数返回的是一个 Iterator，也就是一个惰性序列，所以要强迫 filter()完成计算结果，需要用 list()函数获得所有结果并返回 list。
}

```


### sorted {#sorted}

```cfg

_sorted() {
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)#['about', 'bob', 'Credit', 'Zoo']
sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)	#['Zoo', 'Credit', 'bob', 'about']
}

```


### lambda {#lambda}

```cfg

lambda(){
lambda x: x * x
#关键字 lamb  da 表示匿名函数，冒号前面的 x 表示函数参数。
#匿名函数有个限制，就是只能有一个表达式，不用写 return，返回值就是该表达式的结果
}

```


### decorator {#decorator}

```cfg

decorator(){
#在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）

#最终代码：
import functools
def log(text):
    def decorator(func):	#func 固定
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

@log('execute')
def now():
    print('2020-10-3')
#执行 log('execute')，返回的是 decorator 函数，
#再调用返回的 decorator 函数，func 参数是装饰器后面的 now 函数，返回值最终是 wrapper 函数。

cat <<EOF
返回的那个 wrapper()函数名字就是'wrapper'\
所以，需要把原始函数的__name__等属性复制到 wrapper()函数中\
否则，有些依赖函数签名的代码执行就会出错。
///只需在定义 wrapper()的前面加上@functools.wraps(func)即可///
EOF
  }
```


### try {#try}

```cfg

try(){
try:
    print('try...')
    r = 10 / int('2')
    print('result:', r)
except ValueError as e:
    print('ValueError:', e)
except ZeroDivisionError as e:
    print('ZeroDivisionError:', e)
else:
    print('no error!')
finally:
    print('finally...')
print('END')

  }
```


## Instance {#instance}


### Class_Instance {#class-instance}

```sh

Class_Instance(){
#class 后面紧接着是类名，即 Student，类名通常是大写开头的单词，紧接着是(object)，表示该类是从哪个类继承下来的;
#如果没有合适的继承类，就使用 object 类，这是所有类最终都会继承的类。
创建实例是通过类名+()

cat <<EOF
由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。
通过定义一个特殊的__init__方法，在创建实例的时候，就把 name，score 等属性绑上去
EOF

class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.score = score
cat <<EOF
__init__方法的第一个参数永远是 self，表示创建的实例本身，\
在__init__方法内部，就可以把各种属性绑定到 self，因为 self 就指向创建的实例本身。
EOF

#有了__init__方法，在创建实例的时候，就不能传入空的参数了，必须传入与__init__方法匹配的参数
#但 self 不需要传，Python 解释器自己会把实例变量传进去：

cat @@数据封装@@ << EOF
实例本身就拥有这些数据，要访问这些数据，就没有必要从外面的函数去访问
可以直接在 Student 类的内部定义访问数据的函数（如下 def print_score），这样，就把“数据”给封装起来了。
这些封装数据的函数是和 Student 类本身是关联起来的，我们称之为类的方法：
EOF
class Student(object):
----__init__实例本身，绑定各种属性到 self，因为 self 是指向实例本身。
    def __init__(self, name, score):
        self.name = name
        self.score = score
----方法
    def print_score(self):
        print('%s: %s' % (self.name, self.score))
----增加新的方法
      def get_grade(self):
        if self.score >= 90:
            return 'A'
        elif self.score >= 60:
            return 'B'
        else:
            return 'C'

}
```


### inherit_polymorphism {#inherit-polymorphism}

```sh

inherit_polymorphism(){
#定义一个 class 的时候，可以从某个现有的 class 继承，新的 class 称为子类（Subclass），
#而被继承的 class 称为基类、父类或超类（Base class、Super class）

当我们定义一个 class 的时候，我们实际上就定义了一种数据类型。
我们定义的数据类型和 Python 自带的数据类型，比如 str、list、dict 没什么两样：

a = list() # a 是 list 类型
b = Animal() # b 是 Animal 类型
c = Dog() # c 是 Dog 类型
>>> isinstance(a, list)		#True
>>> isinstance(b, Animal)	#True
>>> isinstance(c, Dog)		#True
>>> isinstance(c, Animal)	#True	#Dog 是从 Animal 继承下来的


cat polymorphism << EOF
对于一个变量，我们只需要知道它是 Animal 类型，无需确切地知道它的子类型，就可以放心地调用 run()方法，
而具体调用的 run()方法是作用在 Animal、Dog、Cat 还是 Tortoise 对象上，由运行时该对象的确切类型决定，
这就是多态真正的威力：调用方只管调用，不管细节，
而当我们新增一种 Animal 的子类时，只要确保 run()方法编写正确，不用管原来的代码是如何调用的。这就是著名的“开闭”原则：
对扩展开放：允许新增 Animal 子类；
对修改封闭：不需要修改依赖 Animal 类型的 run_twice()等函数。
EOF

}

```


### unittest {#unittest}

```sh

unittest(){
#编写单元测试时，我们需要编写一个测试类，从 unittest.TestCase 继承。
#以 test 开头的方法就是测试方法，不以 test 开头的方法不被认为是测试方法，测试的时候不会被执行。

    # 1)python mydict_test.py
  if __name__ == '__main__':
    unittest.main()
# 2)python -m unittest mydict_test

# 可以在单元测试中编写两个特殊的 setUp()和 tearDown()方法。这两个方法会分别在每调用一个测试方法的前后分别被执行。

}

```


### doctest {#doctest}

```sh

doctest(){
if __name__=='__main__':
    import doctest
    doctest.testmod()
}
```


## IO {#io}

\__\__IO\__\__(){}


### fnmatch {#fnmatch}

```sh

_fnmatch(){
#fnmatch 模块主要用于文件名称的匹配,使用简单的通配符就能完成文件名的匹配
nmatch.filter(names, pattern)			对 names 列表进行过滤，返回 names 列表中匹配 pattern 的文件名组成的子集合。
fnmatch.fnmatch(filename, pattern)		判断 filename 文件名，是否和指定 pattern 字符串匹配
fnmatch.fnmatchcase(filename, pattern)	和 fnmatch() 函数功能大致相同，只是该函数区分大小写。
fnmatch.translate(pattern)				将一个 UNIX shell 风格的 pattern 字符串，转换为正则表达式

fnmatch 模块匹配文件名的模式使用的就是 UNIX shell 风格，其支持使用如下几个通配符：
  *：		可匹配任意个任意字符。
  ？：	可匹配一个任意字符。
  [字符序列]：	可匹配中括号里字符序列中的任意字符。该字符序列也支持中画线表示法。比如 [a-c] 可代表 a、b 和 c 字符中任意一个。
  [!字符序列]：	可匹配不在中括号里字符序列中的任意字符


>>>print(fnmatch.translate('a*b.txt'))
>>>(?s:a.*b\.txt)\Z
}

```


### tell_seek {#tell-seek}

```sh

_tell_seek(){
#通过移动文件指针的位置，再借助 read() 和 write() 函数，就可以轻松实现，读取文件中指定位置的数据（或者向文件中的指定位置写入数据）。
${当向文件中写入数据时，如果不是文件的尾部，写入位置的原有数据不会自行向后移动，新写入的数据会将文件中处于该位置的数据直接覆盖掉。}

a.txt <http://c.biancheng.net>
f = open("a.txt",'r')
>>>print(f.tell())	#0
>>>print(f.read(3))#htt
>>>print(f.tell())	#3

${seek()}
file.seek(offset[, whence])
#whence：作为可选参数，用于指定文件指针要放置的位置，该参数的参数值有 3 个选择：
  0 代表文件头（默认值）、
  1 代表当前位置、
  2 代表文件尾。
#offset：表示相对于 whence 位置文件指针的偏移量，正数表示向后偏移，负数表示向前偏移。
${当 offset 值非 0 时，Python 要求文件必须要以二进制格式打开，否则会抛出 io.UnsupportedOperation 错误。}
}

```


### open_close_file {#open-close-file}

```sh

# 1)
try:
f = open('/path/to/file', 'r')
    print(f.read())
finally:
    if f:
        f.close()

# 2)自动补充 f.close()
with open('/path/to/file', 'r') as f:
    print(f.read())


# 3)要读取二进制文件，比如图片、视频等等，用'rb'模式打开文件即可：
>>> f = open('/Users/michael/test.jpg', 'rb')
>>> f.read()
b'\xff\xd8\xff\xe1\x00\x18Exif\x00\x00...' # 十六进制表示的字节

# 4)要读取非 UTF-8 编码的文本文件，需要给 open()函数传入 encoding 参数，例如，读取 GBK 编码的文件：
>>> f = open('/Users/michael/gbk.txt', 'r', encoding='gbk')
>>> f.read()
  '测试'
   f = open('/Users/michael/gbk.txt', 'r', encoding='gbk', errors='ignore')	#errors='ignore',非法字符自动忽略

# 5)with open('/Users/michael/test.txt', 'w') as f:	#'w' or 'rb'
    f.write('Hello, world!')
${传入'a'以追加（append）模式写入}

${READ}
/read() 函数：逐个字节或者字符读取文件中的内容；
  file.read([size])
  #size 作为一个可选参数，用于指定一次最多可读取的字符（字节）个数，如果省略，则默认一次性读取所有内容。
  #如果文件是以文本模式（非二进制模式）打开的，则 read() 函数会逐个字符进行读取；
  #反之，如果文件以二进制模式打开，则 read() 函数会逐个字节进行读取
/readline([size]) 函数：逐行读取文件中的内容；		#size 为可选参数，用于指定读取每一行时，一次最多读取的字符（字节）数。
/readlines([size]) 函数：一次性读取文件中多行内容,entire file。	#该函数返回是一个字符串列表，其中每个元素为文件中的一行内容。
{WRITE}
write()        str
wirtes()       list of str,not include the '\n'
writelines()	entire file,include the '\n'
${使用 writelines() 函数向文件中写入多行数据时，不会自动给各行添加换行符。}
}

```


### operate_dir_file {#operate-dir-file}

```sh

_operate_dir_file(){
---Python 的 os 模块封装了操作系统的目录和文件操作，要注意这些函数有的在 os 模块中，有的在 os.path 模块中


>>> import os
>>> os.name # 操作系统类型
'posix'		#系统是 Linux、Unix 或 Mac OS X
'nt'		#Windows

os.environ				#操作系统中定义的环境变量
os.environ.get('PATH')	#获取某个环境变量的值

--------${$Directory}
>>> os.path.abspath('.')	#'/Users/michael'
>>> os.path.join('/Users/michael', 'testdir')	#'/Users/michael/testdir'
>>> os.mkdir('/Users/michael/testdir')
>>> os.rmdir('/Users/michael/testdir')

把两个路径合成一个时，不要直接拼字符串，而要通过 os.path.join()函数
  part-1/part-2	#linux
  part-1\part-2	#windows
>>> os.path.split('/Users/michael/testdir/file.txt')	#('/Users/michael/testdir', 'file.txt')
>>> os.path.splitext('/path/to/file.txt')				#('/path/to/file', '.txt')
cat <<EOF
这些合并、拆分路径的函数并不要求目录和文件要真实存在，它们只对字符串进行操作。
EOF

--------${File}
import os
>>> os.rename('test.txt', 'test.py')
>>> os.remove('test.py') 		#rm
>>> os.getcwd()					#'/root/python'
>>> os.chdir('/etc')			#cd /etc		>>> os.getcwd()		#'/etc'
>>> os.listdir(os.getcwd())		#lsit content in dir
>>> os.mkdir('/root/pythontest')
>>> os.rmdir('/root/pythontest')#rm empty dir
>>> os.linesep					#'\n' 给出平台使用的终止符，windows \r\n; linxu \n
>>> os.path.isdir('/root/python')	#True
>>> os.path.isfile('/root/python')	#False
>>> os.path.exists('/root')			#True
>>> os.path.exists('/root/1.py')	#False
>>> os.path.dirname('/root/python/if.py')	#'/root/python'
>>> os.path.basename('/root/python/if.py')	#'if.py'
>>> os.path.split(os.getcwd())				#('/root', 'python')
>>> os.path.getsize('/root/python/if.py')	#282
>>> os.path.join('/dave/test/','1.py')		#'/dave/test/1.py' 连接目录文件

>>> os.environ['HOME']			#'/root'
>>> os.makedirs(os.path.join(os.environ['HOME'],'test','py'))
>>> os.system('ls -lR /root/test')	#
  /root/test:
  /root/test/py:

import shutil
shutil.copyfile()

--------${File}_filter
>>> [x for x in os.listdir('.') if os.path.isdir(x)]
['.lein', '.local', '.m2', '.npm', '.ssh', '.Trash', '.vim', 'Applications', 'Desktop', ...]

>>> [x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1]=='.py']
['apis.py', 'config.py', 'models.py', 'pymonitor.py', 'test_db.py', 'urls.py', 'wsgiapp.py']

}

```


### fileinput {#fileinput}

```sh

_fileinput(){
#fileinput 模块可以遍历文本文件的所有行.
    #它的工作方式和 readlines 很类似,不同点在于,它不是将全部的行读到列表中而是创建了一个 xreadlines 对象.
  input() 		#它会返回能够用于 for 循环遍历的对象.
  filename() 		#返回当前文件的名称
  lineno() 		#返回当前(累计)的行数
  filelineno() 	#返回当前文件的行数
  isfirstline() 	#检查当前行是否是文件的第一行
  close()			#关闭序列
}
```


### sys_stdin_fileinput {#sys-stdin-fileinput}

```sh

_sys_stdin_fileinput(){
# 1)import sys
for line in sys.stdin:
            print(line,end="")

${cat /etc/passwd|python demo02.py}	#法 1
${python demo02.py </etc/passwd}	#法 2

# 2)import fileinput
for line in fileinput.input():
print(line,end='')

${python demo04.py /etc/passwd /etc/group}
}

```


### pickling {#pickling}

```sh

pickling(){
我们把变量从内存中变成可存储或传输的过程称之为序列化;在其他语言中也被称之为 serialization，marshalling，flattening 等等
把变量内容从序列化的对象重新读到内存里称之为反序列化，即 unpickling


>>> import pickle
>>> d = dict(name='Bob', age=20, score=88)
>>> pickle.dumps(d)
#pickle.dumps()方法把任意对象序列化成一个 bytes，然后，就可以把这个 bytes 写入文件。
#或者用另一个方法 pickle.dump()直接把对象序列化后写入一个 file-like Object：
>>> f = open('dump.txt', 'wb')
>>> pickle.dump(d, f)
>>> f.close()

#要把对象从磁盘读到内存时，可以先把内容读到一个 bytes，然后用 pickle.loads()方法反序列化出对象，
#也可以直接用 pickle.load()方法从一个 file-like Object 中直接反序列化出对象。
>>> f = open('dump.txt', 'rb')
>>> d = pickle.load(f)
>>> f.close()

JSON 表示的对象就是标准的 JavaScript 语言的对象，JSON 和 Python 内置的数据类型对应如下：

JSON 类型	Python 类型
{}			dict
[]			list
"string"	str
1234.56		int 或 float
true/false	True/False
null		None
>>> import json
>>> d = dict(name='Bob', age=20, score=88)
>>> json.dumps(d)

}

```


### re {#re}

```sh

re(){
#在正则表达式中，如果直接给出字符，就是精确匹配。
  \d 可以匹配一个数字，
  \w 可以匹配一个字母或数字
  . 可以匹配任意字符
  \s 可以匹配一个空格
#要匹配变长的字符，在正则表达式中，
  *表示任意个字符（包括 0 个），
  +表示至少一个字符，
  ?表示 0 个或 1 个字符，
  {n}表示 n 个字符，
  {n,m}表示 n-m 个字符
#更精确地匹配
[0-9a-zA-Z\_]可以匹配一个数字、字母或者下划线；
[0-9a-zA-Z\_]+可以匹配至少由一个数字、字母或者下划线组成的字符串，比如'a100'，'0_Z'，'Py3000'等等；
[a-zA-Z\_][0-9a-zA-Z\_]*可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是 Python 合法的变量；
[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}更精确地限制了变量的长度是 1-20 个字符（前面 1 个字符+后面最多 19 个字符）

A|B 可以匹配 A 或 B，所以(P|p)ython 可以匹配'Python'或者'python'。
^表示行的开头，^\d 表示必须以数字开头。
$表示行的结束，\d$表示必须以数字结束。
你可能注意到了，py 也可以匹配'python'，但是加上^py$就变成了整行匹配，就只能匹配'py'了。

//////////////
s = 'ABC\\-001' 	# 'ABC\-001'	#\转义
s = r'ABC\-001'		#使用 Python 的 r 前缀，就不用考虑转义的问题

${匹配}
正则表达式切分字符串比用固定的字符更灵活
>>> 'a b   c'.split(' ')				#['a', 'b', '', '', 'c']
>>> re.split(r'\s+', 'a b   c')			#['a', 'b', 'c']
>>> re.split(r'[\s\,]+', 'a,b, c  d')	#['a', 'b', 'c', 'd']
>>> re.split(r'[\s\,\;]+', 'a,b;; c  d')#['a', 'b', 'c', 'd']

re.match(r'^\d{3}\-\d{3,8}$', '010-12345')

${提取分组}
正则表达式还有提取子串的强大功能,用()表示的就是要提取的分组（Group）
#^(\d{3})-(\d{3,8})$分别定义了两个组
>>> m = re.match(r'^(\d{3})-(\d{3,8})$', '010-12345')
>>> m.group(0)	#'010-12345'
>>> m.group(1)	#'010'
>>> m.group(2)	#'12345'
#group(0)永远是原始字符串，group(1)、group(2)……表示第 1、2、……个子串

${贪婪匹配}
>>> re.match(r'^(\d+)(0*)$', '102300').groups()		#('102300', '')	#由于\d+采用贪婪匹配，直接把后面的 0 全部匹配了，结果 0*只能匹配空字符串了。
>>> re.match(r'^(\d+?)(0*)$', '102300').groups()	#('1023', '00')	#加个?就可以让\d+采用非贪婪匹配

${编译}
如果一个正则表达式要重复使用几千次，出于效率的考虑，我们可以预编译该正则表达式，接下来重复使用时就不需要编译这个步骤了，直接匹配：
>>> import re
>>> re_telephone = re.compile(r'^(\d{3})-(\d{3,8})$')
>>> re_telephone.match('010-12345').groups()	#('010', '12345')
>>> re_telephone.match('010-8086').groups()		#('010', '8086')
#编译后生成 Regular Expression 对象，由于该对象自己包含了正则表达式，所以调用对应的方法时不用给出正则字符串。

}

```


## LIB {#lib}


### shell_sh {#shell-sh}

```sh

shell in python
  import sh
  #sh.command_name("para1" "para2")
  sh.pwd()
  sh.mkdir( folder )
  sh.echo( This is great! )

  sh.ls("-l")	#ls -l
  print(sh.ls("-l"))

  curl https://www.baidu.com -o page.html --silent
  sh.curl("https://www.baidu.com", o="page.html", silent=True)

  sh.adduser("amoffat", system=True, shell="/bin/bash", no_create_home=True)
  sh.adduser("amoffat", "--system", "--shell", "/bin/bash", "--no-create-home”)	#"

from sh import ls
ls = ls.bake("-la")
print(ls("/home")) # 这样默认就加上了选项-la

```


### BeautifulSoup {#beautifulsoup}

```sh

BeautifulSoup(){
soup.find_all("li")
soup.find_all(id='link2')
tag.p.a.get_text()	#获取到 tag 中包含的所有文版内容包括子孙 tag 中的内容,并将结果作为 Unicode 字符串返回:
}

```


### multiprocessing {#multiprocessing}

```sh

multiprocessing(){
import multiprocessing

# 1)Unix/Linux 操作系统提供了一个 fork()系统调用，它非常特殊。
#普通的函数调用，调用一次，返回一次，但是 fork()调用一次，返回两次
# 因为操作系统自动把当前进程（称为父进程）复制了一份（称为子进程），然后，分别在父进程和子进程内返回。
# Python 的 os 模块封装了常见的系统调用，其中就包括 fork;multiprocessing 模块就是跨平台版本的多进程模块,windows

# start()方法启动，这样创建进程比 fork()还要简单。
# join()方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步。

multiprocessing.process()	#启动单个进程
multiprocessing.pool()	#启动进程池
  pool(4)

# 2)进程间通信是通过 Queue、Pipes 等实现的
multiprocessing.queue.put()	#write
multiprocessing.queue.get() #read
)
```


### multithread {#multithread}

```sh

multithread(){
import threading

# 1)Python 的 threading 模块有个 current_thread()函数，它永远返回当前线程的实例。
while n < 5:
        n = n + 1
        print('thread %s >>> %s' % (threading.current_thread().name, n))

# 2)threading.Lock()
# 线程因为获得了锁，因此其他线程不能同时执行 change_it()，只能等待，直到锁被释放后，获得该锁以后才能改。
# 由于锁只有一个，无论多少线程，同一时刻最多只有一个线程持有该锁，所以，不会造成修改的冲突。
for i in range(100000):
    lock.acquire()   # 先要获取锁:
    try:
        change_it(n)
    finally:
    lock.release()	# 改完了一定要释放锁:

}

```


### multi_processing_thread {#multi-processing-thread}

```sh

multi_processing_thread(){
在 Thread 和 Process 中，应当优选 Process，因为 Process 更稳定\
而且，Process 可以分布到多台机器上，而 Thread 最多只能分布到同一台机器的多个 CPU 上。其中 managers 子模块还支持把多进程分布到多台机器上。

我们在一台机器上写多进程程序时，创建的 Queue 可以直接拿来用\
但是，在分布式多进程环境下，添加任务到 Queue 不可以直接对原始的 task_queue 进行操作\
那样就绕过了 QueueManager 的封装，必须通过 manager.get_task_queue()获得的 Queue 接口添加

而 Queue 之所以能通过网络访问，就是通过 QueueManager 实现的。由于 QueueManager 管理的不止一个 Queue\
所以，要给每个 Queue 的网络调用接口起个名字，比如 get_task_queue
authkey 有什么用？这是为了保证两台机器正常通信，不被其他机器恶意干扰


threads = []
# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)
# 开启新线程
thread1.start()
thread2.start()
# 添加线程到线程列表
threads.append(thread1)
threads.append(thread2)
# 等待所有线程完成，之后才会执行 print()
for t in threads:
    t.join()
print "Exiting Main Thread"
}

```


### datetime {#datetime}

```sh

datetime(){
#datetime 是模块，datetime 模块还包含一个 datetime 类，通过 from datetime import datetime 导入的才是 datetime 这个类
>>> from datetime import datetime
>>> now = datetime.now()
>>> dt = datetime(2015, 4, 19, 12, 20)
>>> print(dt)	#2015-04-19 12:20:00

${timestamp}
在计算机中，时间实际上是用数字表示的。我们把 1970 年 1 月 1 日 00:00:00 UTC+00:00 时区的时刻称为 epoch time，记为 0
（1970 年以前的时间 timestamp 为负数），当前时间就是相对于 epoch time 的秒数，称为 timestamp。
>>> dt = datetime(2015, 4, 19, 12, 20)
>>> dt.timestamp() #1429417200.0

>>> t = 1429417200.0
>>> print(datetime.fromtimestamp(t))	#本地时间 2015-04-19 12:20:00	UTC+8:00
>>> print(datetime.utcfromtimestamp(t)) # UTC 时间 2015-04-19 04:20:00

${str 与 datetime 转换}
>>> from datetime import datetime
>>> cday = datetime.strptime('2015-6-1 18:19:59', '%Y-%m-%d %H:%M:%S')
>>> print(cday)	#2015-06-01 18:19:59

>>> now = datetime.now()
>>> print(now.strftime('%a, %b %d %H:%M'))	#Mon, May 05 16:28

${datetime 加减}
加减可以直接用+和-运算符，不过需要导入 timedelta 这个类
>>> from datetime import datetime, timedelta
>>> now = datetime.now()
>>> now									#datetime.datetime(2015, 5, 18, 16, 57, 3, 540997)
>>> now + timedelta(hours=10)			#datetime.datetime(2015, 5, 19, 2, 57, 3, 540997)
>>> now - timedelta(days=1)				#datetime.datetime(2015, 5, 17, 16, 57, 3, 540997)
>>> now + timedelta(days=2, hours=12)	#datetime.datetime(2015, 5, 21, 4, 57, 3, 540997)

${本地时间转换为 UTC 时间}
一个 datetime 类型有一个时区属性 tzinfo，但是默认为 None，所以无法区分这个 datetime 到底是哪个时区
>>> from datetime import datetime, timedelta, timezone
>>> tz_utc_8 = timezone(timedelta(hours=8)) # 创建时区 UTC+8:00
>>> now = datetime.now()
>>> now	#datetime.datetime(2015, 5, 18, 17, 2, 10, 871012)
>>> dt = now.replace(tzinfo=tz_utc_8) # 强制设置为 UTC+8:00
>>> dt	#datetime.datetime(2015, 5, 18, 17, 2, 10, 871012, tzinfo=datetime.timezone(datetime.timedelta(0, 28800)))	#28800=8x3600

${时区转换}
utcnow()拿到当前的 UTC 时间，再转换为任意时区的时间：
>>> utc_dt = datetime.utcnow().replace(tzinfo=timezone.utc)
>>> print(utc_dt)		#2015-05-18 09:05:12.377316+00:00
>>> bj_dt = utc_dt.astimezone(timezone(timedelta(hours=8)))		# astimezone()将转换时区为北京时间:
>>> print(bj_dt)		#2015-05-18 17:05:12.377316+08:00
>>> tokyo_dt = utc_dt.astimezone(timezone(timedelta(hours=9)))	# astimezone()将转换时区为东京时间:
>>> print(tokyo_dt)		#2015-05-18 18:05:12.377316+09:00
>>> tokyo_dt2 = bj_dt.astimezone(timezone(timedelta(hours=9)))	# astimezone()将 bj_dt 转换时区为东京时间:
>>> print(tokyo_dt2)	#2015-05-18 18:05:12.377316+09:00
///利用带时区的 datetime，通过 astimezone()方法，可以转换到任意时区///

}

```


### hashlib {#hashlib}

```sh

hashlib(){
    #how to use md5 in python hashlib?#
${md5}
import hashlib
md5 = hashlib.md5()
md5.update('how to use md5 in python hashlib?'.encode('utf-8'))
#print(md5.hexdigest())
等价于
md5.update('how to use md5 in '.encode('utf-8'))
md5.update('python hashlib?'.encode('utf-8'))
#print(md5.hexdigest())

${sha1}
import hashlib
sha1 = hashlib.sha1()
sha1.update('how to use sha1 in '.encode('utf-8'))
sha1.update('python hashlib?'.encode('utf-8'))
#print(sha1.hexdigest())
}

```


### requests {#requests}

```sh

requests(){
>>> import requests
>>> r = requests.get('https://www.douban.com/') # 豆瓣首页
>>> r.status_code	#200
>>> r.text			#r.text	#'<!DOCTYPE HTML>\n<html>\n<head>\n<meta name="description" content="提供图书、电影、音乐唱片的推荐、评论和...'
#带参数的 URL，传入一个 dict 作为 params 参数
>>> r = requests.get('https://www.douban.com/search', params={'q': 'python', 'cat': '1001'})
>>> r.url 		#实际请求的 URL	'https://www.douban.com/search?q=python&cat=1001'
>>> r.encoding	#'utf-8'
#无论响应是文本还是二进制内容，我们都可以用 content 属性获得 bytes 对象：
>>> r.content	#b'<!DOCTYPE html>\n<html>\n<head>\n<meta http-equiv="Content-Type" content="text/html; charset=utf-8">\n...'
#传入一个 dict 作为 headers 参数
>>> r = requests.get('https://www.douban.com/', headers={'User-Agent': 'Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit'})
#要发送 POST 请求，只需要把 get()方法变成 post()，然后传入 data 参数作为 POST 请求的数据：
>>> r = requests.post('https://accounts.douban.com/login', data={'form_email': 'abc@example.com', 'form_password': '123456'})
>>> r.headers	#{Content-Type': 'text/html; charset=utf-8', 'Transfer-Encoding': 'chunked', 'Content-Encoding': 'gzip', ...}
>>> r.headers['Content-Type']	#'text/html; charset=utf-8'
>>> r.cookies['ts']				#'example_cookie_12345'
>>> cs = {'token': '12345', 'status': 'working'}
>>> r = requests.get(url, cookies=cs)
>>> r = requests.get(url, timeout=2.5) # 2.5 秒后超时
}

```


### chardet {#chardet}

```sh

chardet(){
>>> chardet.detect(b'Hello, world!')	#{'encoding': 'ascii', 'confidence': 1.0, 'language': ''}
#confidence 字段，表示检测的概率是 1.0（即 100%）
>>> data = '离离原上草，一岁一枯荣'.encode('gbk')
>>> chardet.detect(data)	#{'encoding': 'GB2312', 'confidence': 0.7407407407407407, 'language': 'Chinese'}
}

```


### psutil {#psutil}

```sh

psutil(){
>>> import psutil
${cpu}
>>> psutil.cpu_count()					# CPU 逻辑数量
>>> psutil.cpu_count(logical=False) 	# CPU 物理核心

>>> psutil.cpu_times()					#统计 CPU 的用户／系统／空闲时间
scputimes(user=10963.31, nice=0.0, system=5138.67, idle=356102.45)

>>> for x in range(10):			#实现类似 top 命令的 CPU 使用率，每秒刷新一次，累计 10 次
...     print(psutil.cpu_percent(interval=1, percpu=True))

${memory}
>>> psutil.virtual_memory()	${返回的是字节为单位的整数}
>>> psutil.swap_memory()

${disk}
>>> psutil.disk_partitions() 	#[sdiskpart(device='/dev/disk1', mountpoint='/', fstype='hfs', opts='rw,local,rootfs,dovolfs,journaled,multilabel')]
>>> psutil.disk_usage('/')	 	# sdiskusage(total=998982549504, used=390880133120, free=607840272384, percent=39.1)
>>> psutil.disk_io_counters()	# sdiskio(read_count=988513, write_count=274457, read_bytes=14856830464, write_bytes=17509420032, read_time=2228966, write_time=1618405)
以上信息：磁盘'/'的总容量是 998982549504 = 930 GB，使用了 39.1%。文件格式是 HFS，opts 中包含 rw 表示可读写，journaled 表示支持日志

${net}
>>> psutil.net_io_counters() # 获取网络读写字节／包的个数
>>> psutil.net_if_addrs() # 获取网络接口信息
>>> psutil.net_if_stats() # 获取网络接口状态
 psutil.net_connections() # 获取网络当前连接状态	#需要 root 权限

${pid}
>>> psutil.pids() # 所有进程 ID
>>> p = psutil.Process(3776) # 获取指定进程 ID=3776，其实就是当前 Python 交互环境
>>> p.name() # 进程名称
>>> p.exe() # 进程 exe 路径
>>> p.cmdline() # 进程启动的命令行
>>> p.ppid() # 父进程 ID
>>> p.parent() # 父进程
>>> p.children() # 子进程列表
>>> p.status() # 进程状态
>>> p.username() # 进程用户名
>>> p.create_time() # 进程创建时间
>>> p.terminal() # 进程终端	#'/dev/ttys002'
>>> p.cpu_times() # 进程使用的 CPU 时间	#pcputimes(user=0.081150144, system=0.053269812, children_user=0.0, children_system=0.0)
>>> p.memory_info() # 进程使用的内存	#pmem(rss=8310784, vms=2481725440, pfaults=3207, pageins=18)
>>> p.open_files() # 进程打开的文件	#[]
>>> p.connections() # 进程相关网络连接	#[]
>>> p.num_threads() # 进程的线程数量	#1
>>> p.threads() # 所有线程信息	#[pthread(id=1, user_time=0.090318, system_time=0.062736)]
>>> p.environ() # 进程环境变量	#{'SHELL': '/bin/bash', 'PATH': '/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:...', 'PWD': '/Users/michael', 'LANG': 'zh_CN.UTF-8', ...}
>>> p.terminate() # 结束进程	#Terminated: 15 <-- 自己把自己结束了
>>> psutil.test()	#模拟 ps 效果
}

```


### virtualenv {#virtualenv}

```sh

virtualenv(){
用于创建独立的 Python 运行环境
virtualenv --no-site-packages venv
  #--no-site-packages	安装到系统 Python 环境中的所有第三方包都不会复制过来，
source venv/bin/activate
  #在 venv 环境下，用 pip 安装的包都被安装到 venv 这个环境下
deactivate
}

```


### splinter_selenium {#splinter-selenium}

```sh

splinter_selenium(){
Headless Chrome 是 Chrome 浏览器的无界面形态

chrome_options = webdriver.ChromeOptions()	# 使用 headless 无界面浏览器模式
chrome_options.add_argument('--headless') //增加无界面选项
  #or  chrome_options.set_headless()
chrome_options.add_argument('--disable-gpu') //如果不加这个选项，有时定位会出现问题

}

```


## Graphic {#graphic}


### Tkinter {#tkinter}

```sh

Tkinter(){
#Python 支持多种图形界面的第三方库，包括：Tk,wxWidgets,Qt,GTK/
///Python 自带的库是支持 Tk 的 Tkinter

from tkinter import *

class Application(Frame):	#从 Frame 派生一个 Application 类，这是所有 Widget 的父容器
    def __init__(self, master=None):
        Frame.__init__(self, master)
        self.pack()
        self.createWidgets()

    def createWidgets(self):	#创建一个 Label 和一个 Button，当 Button 被点击时，触发 self.quit()使程序退出
        self.helloLabel = Label(self, text='Hello, world!')
        self.helloLabel.pack()
        self.quitButton = Button(self, text='Quit', command=self.quit)
        self.quitButton.pack()

app = Application()	#实例化 Application
app.master.title('Hello World')	# 设置窗口标题:
app.mainloop()		# 主消息循环:

#GUI 中，每个 Button、Label、输入框等，都是一个 Widget。Frame 则是可以容纳其他 Widget 的 Widget
#'pack()方法把 Widget 加入到父容器中，并实现布局。pack()是最简单的布局，grid()可以实现更复杂的布局。'

${输入文本}
from tkinter import *
import tkinter.messagebox as messagebox

class Application(Frame):
    def __init__(self, master=None):
        Frame.__init__(self, master)
        self.pack()
        self.createWidgets()

    def createWidgets(self):
        self.nameInput = Entry(self)
        self.nameInput.pack()
        self.alertButton = Button(self, text='Hello', command=self.hello)
        self.alertButton.pack()

    def hello(self):
        name = self.nameInput.get() or 'world'
        messagebox.showinfo('Message', 'Hello, %s' % name)

app = Application()
app.master.title('Hello World')
app.mainloop()

}

```


### Turtle_Graphics {#turtle-graphics}

```sh

Turtle_Graphics(){
from turtle import *


width(4)		# 设置笔刷宽度:
forward(200)	# 前进:
right(90)		# 右转 90 度:
pencolor('red')	# 笔刷颜色:
forward(100)
right(90)
pencolor('green')
forward(200)
right(90)
pencolor('blue')
forward(100)
right(90)
done()			# 调用 done()使得窗口等待被关闭，否则将立刻关闭窗口:

}

```


## Socket {#socket}


### usr_agent {#usr-agent}

```sh
user_agent(){
# 1)Firefox 4.0.1 – Windows
#User-Agent:Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1

local： Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:81.0) Gecko/20100101 Firefox/81.0

# 2)Chrome
local：Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36

# 3)confirm UA
Chrome url:		about:version | chrome://version/
Firefox url:	about:support

}
```


### TCP {#tcp}

```sh

TCP(){

${客户端}
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('www.sina.com.cn', 80))	#建立连接，参数是一个 tuple
s.send(b'GET / HTTP/1.1\r\nHost: www.sina.com.cn\r\nConnection: close\r\n\r\n')	## 发送数据:
  #AF_INET 指定使用 IPv4 协议-->更先进的 IPv6，指定为 AF_INET6
  #SOCK_STREAM 指定使用面向流的 TCP 协议
  #新浪网站的 IP 地址可以用域名 www.sina.com.cn 自动转换到 IP 地址
  #端口号小于 1024 的是 Internet 标准服务的端口，端口号大于 1024 的，可以任意使用。

# 接收数据:
buffer = []
while True:
    d = s.recv(1024)	# 每次最多接收 1k 字节:
    if d:
        buffer.append(d)
    else:
        break
data = b''.join(buffer)
s.close()	# 关闭连接

#分离数据
把 HTTP 头和网页分离一下，把 HTTP 头打印出来，网页内容保存到文件：
header, html = data.split(b'\r\n\r\n', 1)
print(header.decode('utf-8'))
with open('sina.html', 'wb') as f:	# 把接收的数据写入文件:
    f.write(html)


${服务器}
#一个 Socket 依赖 4 项：服务器地址、服务器端口、客户端地址、客户端端口来唯一确定一个 Socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('127.0.0.1', 9999))	# 绑定监听端口
  #服务器可能有多块网卡，可以绑定到某一块网卡的 IP 地址上，
  #也可以用 0.0.0.0 绑定到所有的网络地址，
  #还可以用 127.0.0.1 绑定到本机地址，127.0.0.1 是一个特殊的 IP 地址，表示本机地址；
    #如果绑定到这个地址，客户端必须同时在本机运行才能连接，也就是说，外部的计算机无法连接进来。
s.listen(5)	#传入的参数指定等待连接的最大数量
print('Waiting for connection...')
while True:
    sock, addr = s.accept()	# 接受一个新连接:
    t = threading.Thread(target=tcplink, args=(sock, addr))	    # 创建新线程来处理 TCP 连接:
    t.start()

def tcplink(sock, addr):
    print('Accept new connection from %s:%s...' % addr)
    sock.send(b'Welcome!')
    while True:
        data = sock.recv(1024)
        time.sleep(1)
        if not data or data.decode('utf-8') == 'exit':
            break
        sock.send(('Hello, %s!' % data.decode('utf-8')).encode('utf-8'))
    sock.close()
    print('Connection from %s:%s closed.' % addr)
}

```


### UDP {#udp}

```sh

UDP(){
${服务器}
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.bind(('127.0.0.1', 9999))	# 绑定端口
print('Bind UDP on 9999...')
while True:
    data, addr = s.recvfrom(1024)	    # 接收数据:
    print('Received from %s:%s.' % addr)
    s.sendto(b'Hello, %s!' % data, addr)

#recvfrom()方法返回数据和客户端的地址与端口

${客户端}
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
for data in [b'Michael', b'Tracy', b'Sarah']:
    # 发送数据:
    s.sendto(data, ('127.0.0.1', 9999))
    # 接收数据:
    print(s.recv(1024).decode('utf-8'))
s.close()

#从服务器接收数据仍然调用 recv()方法。
#不需要调用 connect()，直接通过 sendto()给服务器发数据
#服务器绑定 UDP 端口和 TCP 端口互不冲突，也就是说，UDP 的 9999 端口与 TCP 的 9999 端口可以各自绑定。

}
```


### sqlite_mysql {#sqlite-mysql}

```sh

sqlite_mysql(){
#SQLite 是一种嵌入式数据库，它的数据库就是一个文件。SQLite 本身是 C 写的，而且体积很小\
#所以，经常被集成到各种应用程序中，甚至在 iOS 和 Android 的 App 中都可以集成。Python 就内置了 SQLite3

# //先导入数据库对应的驱动->数据库连接称为 Connection->打开游标，称之为 Cursor->通过 Cursor 执行 SQL 语句->输出结果。

>>> import sqlite3			# 导入 SQLite 驱动:
>>> conn = sqlite3.connect('test.db')	# 连接到 SQLite 数据库,# 数据库文件是 test.db,# 如果文件不存在，会自动在当前目录创建:
>>> cursor = conn.cursor()	# 创建一个 Cursor:
>>> cursor.execute('create table user (id varchar(20) primary key, name varchar(20))')	## 执行一条 SQL 语句，创建 user 表:
  <sqlite3.Cursor object at 0x10f8aa260>
>>> cursor.execute('insert into user (id, name) values (\'1\', \'Michael\')')	'# 继续执行一条 SQL 语句，插入一条记录:
  <sqlite3.Cursor object at 0x10f8aa260>
>>> cursor.rowcount	# 通过 rowcount 获得插入的行数:
  1
>>> cursor.close()	# 关闭 Cursor:
>>> conn.commit()	# 提交事务:
>>> conn.close()	# 关闭 Connection:

${查询}
>>> conn = sqlite3.connect('test.db')
>>> cursor = conn.cursor()
>>> cursor.execute('select * from user where id=?', ('1',))# 执行查询语句:
  <sqlite3.Cursor object at 0x10f8aa340>
>>> values = cursor.fetchall()	# 获得查询结果集:
>>> values
  [('1', 'Michael')]
>>> cursor.close()
>>> conn.close()


# ==========================================================
${mysql()}

#MySQL 的配置文件默认存放在/etc/my.cnf 或者/etc/mysql/my.cnf
[client]
default-character-set = utf8

[mysqld]
default-storage-engine = INNODB
character-set-server = utf8
collation-server = utf8_general_ci

#如果 MySQL 的版本≥5.5.3，可以把编码设置为 utf8mb4，utf8mb4 和 utf8 完全兼容，但它支持最新的 Unicode 标准，可以显示 emoji 字符

pip install mysql-connector-python --allow-external mysql-connector-python
#pip install mysql-connector	#上面安装失败，就使用这个


>>> import mysql.connector
>>> conn = mysql.connector.connect(user='root', password='password', database='test')
>>> cursor = conn.cursor()

#MySQL 的数据库代码和 SQLite 类似;
#执行 INSERT 等操作后要调用 commit()提交事务；
#MySQL 的 SQL 占位符是%s
>>> cursor.execute('select * from user where id = %s', ('1',))

}
```


## Other {#other}


### percent {#percent}

```sh
Percent(){
a = 0.3214323
bb = "%.2f%%" % (a * 100)
print bb	## 输出结果是 32.14%

b = str(a*100) + '%'
print b	# 输出结果是 32.14323%
}
```


## Modules {#modules}


### import {#import}

```sh
_import(){
    #Python 中导入模块时，实际上会把被导入的模块执行一遍
    #简单来说就是，如果不涉及模块导入的话，__name__的值就是” __main__“，如果当此模块被导入引用的话，那么这个模块内的__name__值就是文件的名字
    #要想被调用模块代码不被执行,在被调用的模块中，可执行的代码前加上这么一句判断，if __name__ == '__main__':，被调用的模块的代码就不会被执行了
    import string
    print(string.__all__)	#查看模块

}
```