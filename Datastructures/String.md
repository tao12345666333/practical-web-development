# 字符串

### 定义

可以由单引号，双引号，三引号进行定义。

```python
>>> 'It\'s a Python string.'  # 单引号中的单引号注意转义
"It's a Python string."
>>>
>>> "It's a Python string."  # 双引号中的单引号可自由使用
"It's a Python string."
>>>
>>> 'double quote "a" '  # 单引号中的双引号可自由使用
'double quote "a" '
>>> s = """
... It's a Python string.
... """  # 多行可使用三引号
>>> s
"\nIt's a Python string.\n"
>>>
>>> s = """\
... It's a Python string.
... """  # 三引号的开头加 \ 可去除开头的空行
>>> s
"It's a Python string.\n"
```

当字符串中包含转义字符时，可使用 `r` 前缀避免转义

```python
>>> r'row string\n'  # 使用前缀 r 定义 raw-string
'row string\\n'
>>> print('C:\path\name')  # \n 是一个转义字符，会被转义为一个新行
C:\path
ame
>>> print(r'C:\path\name')  # 加 r 前缀可避免转义
C:\path\name
```

同时，Python 可自动合并相邻的字符串，需要注意使用场景，如下：

```python
>>> 'Talk ''is ''cheap.'
'Talk is cheap.'
>>> 'show '"me "'your '"code."  # 单双引号可混用
'show me your code.'
>>> 'Love ' * 3  # 使用 * 指定重复次数
'Love Love Love '
>>>
>>> ('Love ' * 3) + 'you'  # 使用 + 连接两个字符串
'Love Love Love you'
>>>
>>> 'Love ' * 3 'you'  # 动态生成的字符串不会自动合并，而且有语法错误
  File "<stdin>", line 1
    'Love ' * 3 'you'
                    ^
SyntaxError: invalid syntax
>>>
>>> ('Talk is cheap, '
... 'show me your code.')  # 用于连接多行也很方便
'Talk is cheap, show me your code.'
>>>
```

### 编解码

在 Python 2.x 中使用中文尤其需要注意编码问题，其自身默认使用的是 ASCII 编码，在使用时需考虑到系统编码情况。

```python
>>> import sys
>>> sys.getdefaultencoding()  # 获取默认编码
'ascii'
>>>
>>> import locale
>>> locale.getdefaultlocale()  # 获取系统默认编码
('zh_CN', 'UTF-8')
```

一般来说，这个过程可以表述为：其他编码格式的字符串—>解码(decode)—>unicode—>编码(encode)—>所需要的编码格式。 看下面的例子：


```python
>>> s = '人生苦短'  # 使用系统默认编码 UTF-8 字符串
>>> s
'\xe4\xba\xba\xe7\x94\x9f\xe8\x8b\xa6\xe7\x9f\xad'
>>> print(s)
人生苦短
>>> len(s), type(s)
(12, <type 'str'>)
>>> u = u'人生苦短'  # 使用 u 前缀转换为 unicode 编码
>>> u
u'\u4eba\u751f\u82e6\u77ed'
>>> print(u)
人生苦短
>>> len(u), type(u)
(4, <type 'unicode'>)
>>>
>>> s.decode('utf-8')  # 解码成 unicode
u'\u4eba\u751f\u82e6\u77ed'
>>> s.decode('utf-8') == u
True
>>> s.decode('utf-8').encode('gb2312')  # 解码后再进行编码
'\xc8\xcb\xc9\xfa\xbf\xe0\xb6\xcc'
```

另外，标准库中提供了一个很方便用于处理编解码的模块 [`codecs`](https://docs.python.org/2.7/library/codecs.html) 推荐使用。


### 基本操作

以下按增删改查的顺序列出的字符串常用操作方法。

```python
>>> # 连接
>>> 'Py' 'thon'
'Python'
>>> # 重复
>>> 'Py' * 3
'PyPyPy'
>>> # 合并序列
>>> '-'.join(['P', 'y', 't', 'h', 'o', 'n'])
'P-y-t-h-o-n'
>>> # 指定字符切割
>>> 'Moe Love is my site.'.split(' ')
['Moe', 'Love', 'is', 'my', 'site.']
>>> 'Moe Love is my site.'.split()
['Moe', 'Love', 'is', 'my', 'site.']
>>> 'Moe Love is my site.'.split(' ', 2)  # 第二个参数为 maxsplit
['Moe', 'Love', 'is my site.']
>>> # 按行切割
>>> 'Moe\nLove\n'.splitlines()
['Moe', 'Love']
>>> 'Moe\nLove\n'.splitlines(True)  # 接收一个 keepends 参数用于是否保留换行符
['Moe\n', 'Love\n']
>>> 'Moe\nLove\n'.split('\n')
['Moe', 'Love', '']
>>> # 去除指定字符
>>> 'MoeLove'.strip('ve')
'MoeLo'
>>> # 注意下面的例子，这也是容易被忽视的地方
>>> 'MoeLove'.strip('Love')  # 前后
'M'
>>> 'MoeLove'.lstrip('Love')  # 左侧
'MoeLove'
>>> 'MoeLove'.rstrip('Love')  # 右侧
'M'
>>> '  MoeLove '.strip()
'MoeLove'
>>> '  MoeLove '.lstrip()
'MoeLove '
>>> '  MoeLove '.rstrip()
'  MoeLove'
>>> 'MoeLoveMoe'.replace('oe', 'ie')
'MieLoveMie'
>>> 'MoeLoveMoe'.replace('oe', 'ie', 1)  # 可指定替换次数
'MieLoveMoe'
>>> 'MoeLove'.lower()  # 转小写
'moelove'
>>> 'MoeLove'.upper()  # 转大写
'MOELOVE'
>>> 'MoeLove'.find('o')
1
>>> 'MoeLove'.find('o', 2)  # 也可传入第三个参数指定结束位置
4
>>> 'MoeLove'.startswith('Moe')
True
>>> 'MoeLove'.endswith('ove')
True
>>> # 填充
>>> 'MoeLove'.center(30, '-')
'-----------MoeLove------------'
>>> 'MoeLove'.ljust(30, '-')
'MoeLove-----------------------'
>>> 'MoeLove'.rjust(30, '-')
'-----------------------MoeLove'
```


### 格式化

Python 中对字符串格式化的方法有很多



