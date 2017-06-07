# 基础数据类型

## 字符串

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

```
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
>>> 'Love ' * 3 'you'  # 动态生成的字符串不会自动合并
  File "<stdin>", line 1
    'Love ' * 3 'you'
                    ^
SyntaxError: invalid syntax
>>> ('Love ' * 3) + 'you'  # 使用 + 连接两个字符串
'Love Love Love you'
>>>
```

* 格式化

```python
print(s.center(30))  # 居中
print(s.ljust(30))  # 靠左
print(s.rjust(30))  # 靠右
```

## 列表

## 元组

## 字典

## 集合

## 布尔

