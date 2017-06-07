# 基础数据类型

## 字符串

* 定义

可以由单引号，双引号，三引号进行定义。

```python
>>> m = 'It\'s a Python string.'  # 单引号中的单引号注意转义
>>> m
"It's a Python string."
>>>
>>> n = "It's a Python string."  # 双引号中的单引号可自由使用
"It's a Python string."
>>>
>>> o = 'double quote "a" '  # 单引号中的双引号可自由使用
'double quote "a" '
>>> s = """
... It's a Python string.
... """  # 多行可使用三引号
>>> s
"\nIt's a Python string.\n"
>>>
>>> p = r'row string\n'  # 使用前缀 r 定义 raw-string
'row string\\n'
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

