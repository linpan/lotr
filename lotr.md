# Code of Conduct

## 版本管理

| 变更者 | 变更时间 | 变更内容 | 版本 |备注|
| :-----:| :-----: | :----: | :----: | :----: |
| Hiro | 2021-04-28 | 初稿 | v0.28 |    |
| Hiro | 2021-05-06 | 初稿 | v0.29 | add git hooks    |
| Hiro | 2021-05-06 | 初稿 | v0.29.1 | PEP731    |
| Hiro | 2021-05-11 | 初稿 | v0.29.2 | 接口文档    |
| Hiro | 2021-05-14 | 初稿 | v0.29.3 | 注释类型声明 |
| Hiro | 2021-05-14 | 初稿 | v0.29.4 | 算法结构 |

## FastAPI项目开发规范

### 开发环境

- 推荐IDE: Pycharm
- 虚拟环境: Virtualenv
- python版本: Python3.8+
- 部署文件: Docker
- 测试: Pytest
- Git 钩子: pre-commit

要求每个项目使用单独的虚拟环境，环境依赖跟随项目.

### FastAPI目标结构

```
├── app 
    ├── /api 
        ├── api_v1  # v1版本
        ├── api_v2  # v2版本
    ├── /core # 配置文件
    ├── /crud # 数据库操作
    ├── /db   # 数据库的配置
        ├── reids.py
        ├── mongodb.py
        ├── mysql.py
        ├── postgres.py
    ├── /models # 数据库的orm
    ├── /schemas # 数据模型
    ├── /util # 其他通用的类或工具
    ├── version.py # 版本
    └── main.py  # 创建fastpi app及应用扩展
    └── exceptions.py
├── DockerFile /
├── ReadMe.md /

```

模块或文件命名规范的参考:

- exceptions.py # 异常
- middlewares.py # 中间件
- types.py #类型标准
- permissions.py # 权限
- dependecies.py # 依赖
- conf.py # 配置文件
- routes.py # 路由
- backends.py
- cli.py # 脚本命令

### Readme的规范

- 项目描述
- 项目的基本结构/框架图
- 项目的依赖
- 安装及快速使用
- ChangeLog记录

**算法工程结构.**

以 Ludwig [算法为例](https://github.com/ludwig-ai/ludwig)

```

├──transformer
    ├── /scripts  # command cli
    ├── /Ludwig  #算法包
       ├── /models
       ├── /utils
       ├── cli.py 
       ├── train.py 
    ├── /api # api 接口
    ├── /tests # 单元测试
    ├── /example # 例子及用法
    ├── /notebooks  ipynb 文件 
    ├── /util # 其他通用的类或工具
    ├── docker # docker 编排
    └── version.py # 版本
```

**算法工程的文档包含入门、API接口文档和教程三大部分.**

接口文档示例：

### POST /api/pool/autoscale/(.+)

Autoscaling worker pool

Request:

```bash
POST /api/worker/pool/autoscale/celery@worker2?min=3&max=10 HTTP/1.1

Content-Type: application/x-www-form-urlencoded; charset=utf-8


```

Response:

```bash
HTTP/1.1 200 OK
Content-Length: 66
Content-Type: application/json; charset=UTF-8

{
    "message": "Autoscaling 'Spacex@worker2' worker (min=3, max=10)"
}
```

### Query Parameters:

- min – minimum amount pool processes
- max – maximum amount pool processes

### Request Headers:

- Authorization –OAuth2 JWT token to authenticate

### Status Codes:

- 200 OK – no error
- 401 Unauthorized – unauthorized request
- 403 Forbidden – autoscaling is not enabled

### Git commit 规范

所有项目的Commit Log的格式精确控制，增加可读性，便于查看变更历史，形成良好的git使用习惯:

- feat: 新功能
- fix: 修复问题
- docs: 修改文档
- style: 修改代码格式，不影响代码逻辑
- refactor: 重构代码，理论上不影响现有功能
- perf: 优化相关，比如提升性能、体验
- typo: 修复小的拼写错误
- test: 测试用例，包括单元测试、集成测试等

### 数据库查询API规范

本部分FastAPI项目

结构组织
> crud.module_name.api

【推荐】基本的API函数:

- filters()
- all()
- distinct()
- first()  # get first item
- last()  # get last item

# Python 编码风格与规范

本规范的示例采用符合 Python3.6+ 的语法.

**必须**（Mandatory）：开发者必须采用；

**推荐**（Preferable）：开发者理应采用，但如有特殊情况，可以不采用；

**可选**（Optional）：开发者可参考，自行决定是否采用；

未明确指明的则默认为 **必须**（Mandatory）。

### 缩进

【**必须**】 对于每级缩进，统一要求使用4个 空格 ，而非 tab 键。 `pylint:mixed-indentation`, Anti-pattern-indentation.

【**必须**】 续行，要求使用括号等定限界符，并且需要垂直对齐。 pylint:`Anti-pattern-continuation`.

```bash

# 与定界（括号）符对齐
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 换行并增加4个额外的空格（一级缩进）
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# 悬挂需要增加一级缩进
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)

```

【**推荐**】 如果包含定界符（括号，中括号，大括号）的表达式跨越多行，那么定界符的扩回符， 可以放置与最后一行的非空字符对齐或者与构造多行的开始第一个字符对齐。

```bash
# 与最后一行的非空字符对齐
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )

# 或者与开始构造多行的第一个字符对齐
my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
```

【**推荐**】 对于会经常改动的函数参数、列表、字典定义，建议每行一个元素，并且每行增加一个。

```bash
yes = ('y', 'Y', 'yes', 'TRUE', 'True', 'true', 'On', 'on', '1')  # 基本不再改变

kwlist = [
    'False',
    'None',
    'True',
    'and',
    'as',
    'assert',
    ...
    'yield',  # 最后一个元素也增加一个逗号 ，方便以后diff不显示此行
]

person = {
    'name': 'bob',
    'age': 12,      # 可能经常增加字段
}
```

【**可选**】 对于 if 判断，一般来说尽量不要放置过多的判断条件。换行时增加 4 个额外的空格。 pylint:`Anti-pattern-continuation`. pycodestyle:E129 visually
indented line with same indent as next logical line.

```bash
# 更推荐：在续行中，增加额外的缩进级别。允许 and 操作符在前
if (this_is_one_thing
        and that_is_another_thing):
    do_something()

# 更推荐：在续行中，增加额外的缩进级别
if (this_is_one_thing and
        that_is_another_thing):
    do_something()

# 允许：与定界符（括号）对齐，不需要额外的缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# 允许：增加注释，编辑器会提示语法高亮，有助于区分
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()
```

### 每行最大长度

【**必须**】 每行最多不超过120个字符。每行代码最大长度限制的根本原因是过长的行会导致阅读障碍，使得缩进失效。 pylint:`line-too-long`.

除了以下两种情况例外： 1. 导入模块语句。 2. 注释中包含的URL。

如果需要一个长的字符串，可以用括号实现隐形连接。

```bash
x = ('This will build a very long long '
     'long long long long long long string')
 
```

### 空行

【`必须`】 模块中的一级函数和类定义之间，需要空两行。 pycodestyle:`E302 expected 2 blank lines`.

【`必须`】 类中函数定义之间，空一行。 pycodestyle:`E302 expected 1 blank line`.

【`必须`】 源文件末尾有且仅有 一行空行。 pylint:`missing-final-newline, trailing-newlines`.

【`必须`】 通常每个语句应该独占一行。 pylint:`multiple-statements`.

如果测试结果与测试语句在一行放得下，你也可以将它们放在同一行。 如果是if语句, 只有在没有else时才能这样做。 特别地，绝不要对 try/except 这样做，因为try和except不能放在同一行。

```bash
if foo:
    bar(foo)
else:
    baz(foo)

try:
    bar(foo)
except ValueError:
    baz(foo)
```

### 括号

【**必须**】 tuple 元组不允许逗号结尾，显式增加括号规避。即使一个元素也加上括号。 pylint:`trailing-comma-tuple`.

行尾的逗号可能导致本来要定义一个简单变量，结果变成 tuple 变量。

```bash
trailingcomma = (['f'],)

return (1,)

```

### 模块引用(import)

【**必须**】 每个导入应该独占一行。 pylint:`multiple-imports`.

必须】 导入总应该放在文件顶部，位于模块注释和文档字符串之后，模块全局变量和常量之前。 pylint:`wrong-import-order`.

导入应该按照从最通用到最不通用的顺序分组, 每个分组之间，需要空一行:

- 标准库导入
- 第三方库导入 -本地导入 每种分组中， 应该根据每个模块的完整包路径按***字典序***排序，并忽略大小写。

```bash
import foo
from foo import bar
from foo.bar import baz
from foo.bar import Quux
from Foob import ar

```

【**必须**】 避免使用 from <module> import *，因为可能会造成命名空间的污染。 pylint:`wildcard-import`.

【**必须**】 禁止导入了模块却不使用它。 pylint:`unused-import`.

``` bash
import os  # used
from pathlib import Path 
dir_path = os.path.abspath('.')
```

### 模块中的魔术变量(dunders)

【**必须**】 对于两个 _ 开头和两个 _ 结尾的变量， 如 `__all__`，`__author__`，`__version__`等，应该放在模块文档之后， 其他模块导入之前（__future__ 除外）。

【**必须**】 Python 要求 future 导入必须出现在其他模块导入之前。 pylint:`misplaced-future`.

```bash
# -*- coding: utf-8 -*-
#
# Copyright @ 2020 XXX

"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

### 注释

> 有效的注释有助于帮助开发者更快地理解代码，模块，函数，方法，以及行内注释的都有各自的风格。

【**必须**】 所有#开头的注释，必须与所在的代码块同级，并置放在代码之上。 pycodestyle:E262 `inline comment should start with '# '`.

【必须】 注释的每一行都应该以#和一个空格开头。 pycodestyle:`E266 too many leading '#' for block comment, E262 inline comment should start`
`with '# '.`

【**必须**】 行内注释#与代码离开至少2个空格。 pycodestyle:`E261 at least two spaces before inline comment`.

【**必须**】 块注释：对于复杂的操作，可以在代码之前写若干行注释，对简单的代码，可以放在行内。与代码离开至少2个空格。

```bash
# this is a very complex operation, please
# read this carefully

if i & (i-1) == 0:
    # do my job ...

# 单行注释，为可读性，至少离开代码2个空格
x = x + 1                 # Compensate for border
```

TODO 注释需要加上名字。

TODO注释应该在所有开头处包含TODO字符串，紧跟着是用括号括起来的你的名字， email地址或其它标识符，然后是一个可选的冒号。 接着必须有一行注释，解释要做什么。 主要目的是为了有一个统一的TODO格式，这样添加注释的人就可以搜索到(
并可以按需提供更多细节)。 写了TODO注释并不保证写的人会亲自解决问题。 当你写了一个`TODO`，请注上你的名字。

> 为临时代码使用TODO注释, 它是一种短期解决方案。常见的IDE在提交代码时， 会检查变更中包含了TODO并提醒开发者，防止提交是忘记还有未完成的代码。 如果TODO是将来做某事的形式,
> 那么请确保包含一个指定的日期或者一个特定的事件（条件）。 相同地，也可以留下FIXME, NOTES 注释。

```bash
# TODO(zhangsan): Change this to use relations.
# FIXME(zhangsan@xx.com): Please fix me here.
# NOTES(zhangsan): This is some notes.
# SEE: Pointers to other code, web link, etc.
 
```

### 文档字符串

Docstring 文档字符串提供了将文档与Python模块，函数，类和方法相关联的便捷方法。

```bash

def foobar():
    """Return a foobang

    Optional plotz says to frobnicate the bizbaz first.
    """

```

【**推荐**】 需对外发布的public 模块，函数，类，方法等需要包含文档字符串。内部使用的方法，函数等，要求使用简单的注释描述功能。 pylint:`missing-module-docstring`,
`missing-class-docstring`, `missing-function-docstring`.

一个函数或方法，如果可以直接被其他开发者使用，需要提供文档明确其含义，需要指出输入，输出，以及异常内容。

【**必须**】 第一行应为文档名，空一行后，输入文档描述。

【**推荐**】 在使用文档字符串时，推荐使用 reStructuredText 风格类型。

```python
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    :param big_table: An open Bigtable Table instance.
    :param keys: A sequence of strings representing the key of each table row
        to fetch.
    :param other_silly_variable: Another optional variable, that has a much
        longer name than the other args, and which does nothing.

    :return: A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    :raises ValueError: if `keys` is empty.
    :raises IOError: An error occurred accessing the bigtable.Table object.
    """
    pass

```

[**推荐**】 类应该在其定义下有一个用于描述该类的文档字符串。 如果类有公共属性(Attributes)，那么文档中应该有一个属性(Attributes)段， 并且应该遵守和函数参数相同的格式。

```python

class SampleClass:
    """Summary of class here.

    Longer class information....
    Longer class information....

    :ivar likes_spam: A boolean indicating if we like SPAM or not.
    :ivar eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```

### 类型提示

Python 是动态语言，在运行时无需指定变量类型。 虽然运行时不会执行函数与变量类型注解，但类型提示有助于阅读代码、重构、静态代码检查与IDE的语法提示。 推荐在项目中使用该特性。
更多使用可以参考 [类型标注支持](https://docs.python.org/zh-cn/3/library/typing.html "Google")

```bash
from typing import List


class Container(object):
    def __init__(self) -> None:
        self.elements: List[int] = []

    def append(self, element: int) -> None:
        self.elements.append(element)


def greeting(name: str) -> str:
    return 'Hello ' + name

```

对用重要的变量给予使用注释方式来类型标注:

```
self._bindings = {}  # type: Dict[str, Binding]
```

【**必须**】 模块级变量，类和实例变量以及局部变量的注释应在冒号后面有一个空格。 pycodestyle:`E231 missing whitespace after ':'`.

【**必须**】 冒号前不应有空格。 pycodestyle:`E203 whitespace before ':'`.

【**必须**】 如果有赋值符，则等号在两边应恰好有一个空格。 pycodestyle:`E225 missing whitespace around operator`.

【**推荐**】 当使用类型提示出现循环引用时，可以在导入的头部使用 `if typing.TYPE_CHECKING`， 且对类型注解使用双引号或单引号进行修饰

```bash

import typing

if typing.TYPE_CHECKING:  # 运行时不导入
    # For type annotation
    from typing import Any, Dict, List, Sequence  # NOQA
    from sphinx.application import Sphinx  # NOQA


class Parser(docutils.parsers.Parser):

    def set_application(self, app: "Sphinx") -> None:  # 同时采用引号
        pass

```

### 字符串

【**推荐**】 即使参数都是字符串, 也要使用%操作符或者格式化方法格式化字符串。不过也不能一概而论, 你需要在+和%之间权衡

```bash

# 更推荐
x = f'name: {name}; score: {n}'  # Python3.6+ 以上支持
x = 'name: {name}; score: {n}'.format(name=name, n=n)
x = 'name: {name}; score: {n}'.format(**{"name": name, "n": n})
x = 'name: %(name)s; score: %(n)d' % {"name": name, "n": n}

# 可接受
x = '%s, %s!' % (imperative, expletive)
x = '{}, {}!'.format(imperative, expletive)
x = 'name: %s; score: %d' % (name, n)
x = 'name: {}; score: {}'.format(name, n)

```

【**推荐**】 避免在循环中用+和+=操作符来累加字符串。 由于字符串是不可变的, 这样做会创建不必要的临时对象, 并且导致二次方而不是线性的运行时间。 作为替代方案, 你可以将每个子串加入列表, 然后在循环结束后用 .join
连接列表。 (
也可以将每个子串写入一个 io.StringIO 缓存中。) pylint:`consider-using-join`.

```bash
# Best practice:
items = ['<table>']
for last_name, first_name in employee_list:
    items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
items.append('</table>')
employee_table = ''.join(items)
# Anti-pattern:
employee_table = '<table>'
for last_name, first_name in employee_list:
    employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
employee_table += '</table>'
```

【**必须**】 如果要引用的字符串为多行时，需要使用双引号引用字符串。

【**推荐**】 检查前缀和后缀时，使用 .startswith() 和 .endswith() 代替字符串切片

```bash
# Best practice
if foo.startswith('bar'):
# Anti-pattern
if foo[:3] == 'bar':
```

### 命名

> module_name, package_name, ClassName, method_name, ExceptionName, function_name, GLOBAL_VAR_NAME, instance_var_name, function_parameter_name, local_var_name.


应该避免的名称：

- 单字符名称，除了计数器和迭代器。 -包/模块名中的连字符(-)。 -双下划线开头并结尾的名称(Python保留，例如__init__)

【**推荐))】 命名约定规则如下： pylint:`invalid-name`.

1. 所谓内部(Internal)表示仅模块内可用, 或者, 在类内是保护或私有的。
2. 用单下划线(_)开头表示模块变量或函数是protected的(使用from module import *时不会包含)。
3. 用双下划线(__)开头的实例变量或方法表示类内私有。
4. 将相关的类和顶级函数放在同一个模块里。不像Java，没必要限制一个类一个模块。
5. 对类名使用大写字母开头的单词(如CapWords, 即Pascal风格)，但是模块名应该用小写加下划线的方式(如lower_with_under.py)
   。尽管已经有很多现存的模块使用类似于CapWords.py这样的命名，但现在已经不鼓励这样做, 因为如果模块名碰巧和类名一致，这会让人困扰。

命名要求

- 变量名采用小写蛇形风格，例如 coupon_name、 user_last_name 等；

- 常量名采用大写蛇形风格，例如 COUPON_NAME、 USER_LAST_NAME 等；

- 函数名采用小写蛇形风格，并要求以动词开头，例如 take_last_name、 translate 等；

- 类名采用大驼峰命名风格，例如 Storage、 ImageDownload 等；

- 接口名采用大驼峰命名风格，例如 StorageInterface、 DownloadInterface 等；

- 包名采用小写蛇形命名风格，例如 file_storage、 components 等；

- 文件名采用小写蛇形命名风格，例如 urils.py、 remote_cache.conf 等；

- 项目名采用小写蛇形命名风格，例如 sequence、 translation_machine 等；

- 见名知意，要用完整词组表达含义，但词组单词数量不可超过 5 个；

- 不可自定义单词简写，例如 translate 简写为 trans;

- 不可使用语言或系统保留关键词，例如 def、 pass、 class、 id 等；

- 如无特殊情况，不建议使用拼音；

## 编码规范

### 三目运算符

【**必须**】 三目操作符判断，python 不支持三目运算符，但可使用如下方式，禁止使用复杂难懂的逻辑判断。

```bash

x = a if a >= b else b
x = a >= b and a or b
```

### None 条件的判断

【**必须**】 为提升可读性，在判断条件中应使用` is not`，而不使用` not ... is`。 pycodestyle:E714 `test for object identity should be 'is not'`.

```bash
# Best practice
if foo is not None:
# Anti-pattern
if not foo is None:
```

### lambda匿名函数

【**必须**】 使用 def 定义简短函数而不是使用 lambda。 pycodestyle:`E731 do not assign a lambda expression, use a def`.

使用def的方式有助于在trackbacks中打印有效的类型信息，明确使用f函数而不是一个lambda的调用。

### 条件表达式

【**推荐**】 函数或者方法在没有返回时要明确返回None。 pylint:`inconsistent-return-statements`.

```bash

# Best practice 
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None # 直接使用 return 也可

def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)
    
# Anti-pattern 
def foo(x):
    if x >= 0:
        return math.sqrt(x)

def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
    
```

【**推荐**】 对于未知的条件分支或者不应该进入的分支，建议抛出异常，而不是返回一个值（比如说`None` 或`False`）。

```bash
# Best practice 
def f(x):
    if x in ('SUCCESS',):
        return True
    else:
        raise MyException()  # 如果一定不会走到的条件，可以增加异常，防止将来未知的语句执行。
# Anti-pattern        
 def f(x):
    if x in ('SUCCESS',):
        return True
    return None
```

【**可选**】 if 与 else 尽量一起出现，而不是全部都是if子句。

```bash
# Best practice 
if condition:
    do_something()
else:
    # 增加说明注释
    pass

if condition:
    do_something()
# 这里增加注释说明为什么不用写else子句
# else:
#     pass


# Anti-pattern 
if condition:
    do_something()
if another_condition:  # 不能确定是否笔误为 elif ，还是开启全新一个if条件
    do_another_something()
else:
    do_else_something()
```

### True/False 布尔运算

【**必须**】 不要用` ==` 与 `True`、 `False` 进行布尔运算。 pylint:`singleton-comparison`.

```bash
#  Best practice
if greeting:
   pass

# Anti-pattern    
if greeting == True:
   pass

if greeting is True:  # Worse ?
   pass
      
```

【**必须**】 对序列（字符串、列表 、元组），空序列为 false 的情况。 pylint:`len-as-condition`.

```bash
# Best practice 
if not seq:
   pass

if seq:
   pass

# Anti-pattern    
if len(seq):
   pass

if not len(seq):
   pass
```

### 列表推导式

【**必须**】 禁止超过1个for语句或过滤器表达式，否则使用传统for循环语句替代。

```bash
# Best practice 
number_list = [1, 2, 3, 10, 20, 55]
odd = [i for i in number_list if i % 2 == 1]

result = []
for x in range(10):
    for y in range(5):
        if x * y > 10:
            result.append((x, y))
# Anti-pattern
result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]  # for 语句
```

【**推荐**】 列表推导式适用于简单场景。 如果语句过长，每个部分应该单独置于一行： 映射表达式， for语句， 过滤器表达式。

````bash
# Best practice 
fizzbuzz = []
for n in range(100):
    if n % 3 == 0 and n % 5 == 0:
        fizzbuzz.append(f'fizzbuzz {n}')
    elif n % 3 == 0:
        fizzbuzz.append(f'fizz {n}')
    elif n % 5 == 0:
        fizzbuzz.append(f'buzz {n}')
    else:
        fizzbuzz.append(n)


for n in range(1, 11):
    print(n)
# Anti-pattern 
# 条件过于复杂，应该采用for语句展开
fizzbuzz = [
    f'fizzbuzz {n}' if n % 3 == 0 and n % 5 == 0
    else f'fizz {n}' if n % 3 == 0
    else f'buzz {n}' if n % 5 == 0
    else n
    for n in range(100)
]


[print(n) for n in range(1, 11)]  # 无返回值
````

### 函数

【**必须**】 模块内部禁止定义重复函数声明。 pylint:`function-redefined`.

禁止重复的函数定义。

【**必须**】 函数参数中，不允许出现可变类型变量作为默认值。 pylint:`dangerous-default-value`.

```bash
# Best practice 
def f(x=0, y=None, z=None):
    if y is None:
        y = []
    if z is None:
        z = {}

# Anti-pattern 
def f(x=0, y=[], z={}):
    pass

def f(a, b=time.time()):
    pass
    
```

### lambda 不可赋值变量

Do not assign a lambda expression, use a def

```bash
  # Best practice 
  def flatten_list():
    return list(set(itertools.chain.from_iterable(x)))
    
  # Anti-pattern   
   flatten = lambda x: list(set(itertools.chain.from_iterable(x)))
```

### 用 `has` 或 `is` 前缀命名布尔元素

如果一个元素保存的是布尔值，is和has前缀提供一种自然的方式，使其在命名空间中的可读性更强

 ```bash
 class DB:
      is_connected = False
      has_cache = False
```

### 日志调试

用 logging.debug 取代用于 debug 和调试的 print 语句；

### 绝对路径

[**推荐**] 使用Path 替代 os.path

```bash
from pathlib import Path

```

导入外部文件时尽量使用相对路径，代码任何位置，包括注释中，不允许出现个人开发环境的绝对文件路径；

### 变量

【**必须**】 禁止定义了变量却不使用它。 pylint:`unused-variable`.

在代码里到处定义变量却没有使用它，不完整的代码结构看起来像是个代码错误。

即使没有使用，但是定义变量仍然需要消耗资源，并且对阅读代码的人也会造成困惑，不知道这些变量是要做什么的。

## 工具与配置

### isort

isort会把import分成标准库、第三方库、本地库三种，分别按字母排序。

### flake8

flake8 是一个结合了 pycodestyle，pyflakes，mccabe 检查 Python 代码规范的工具。

### pylint

pylint 是一个能够检查编码质量、编码规范的工具。

### black

black 是一个官方的 Python 代码格式化工具。 如果不想格式化部分代码，可以配套使用 # fmt: off/# fmt: on 临时关闭格式化。

```bash
# fmt: off
在这的代码不会被格式化
# fmt: on
```

### git hooks 自动化检查代码

[**必须**] 项目根目录存放此文件`pre-commit-config.yaml`模板.

提供`pre-commit-config.yaml` 文件封装的工具有： `isort`、 `black` 、`flake8` 和 `mypy`.

# Code Review

### 审阅的原则

- CodeReview是针对代码，不是针对人.

- CodeReview是一种学习，一种技术沉淀.

### 辅助工具

GitLab

### 审阅时间点

每次的Merge Request进行CodeReview.

### 组织类型

- 小组内review，通常是模块负责人或者项目负责人review，频率比较高，一天至少一次.
- 团队review，通常是整个团队review代码，团队负责人牵头，频率可以低一点，鉴于公司情况一周至少1次.

### 审阅的清单

- 设计：代码是否经过精心设计并适合你的系统？

- 功能：代码是否符合开发者意图？

- 复杂性：代码是否可以更简洁？未来其他开发者接手时，代码是否易于理解与易用？

- 命名：开发人员是否为变量、类、方法等选择了明确的名称？

- 注释：注释是否清晰有效？

- 风格：代码是否遵循了代码开发规范？

- 文档：开发人员是否也同步更新了相关文档？

总之，代码是否符合团队约定的代码风格规范、代码是否切合它所实现的业务、代码是否安全、代码性能、对后续开发者是否友好，即是否容易维护等.
