python re库二、函数详解

函数中使用参数标识：

参数

描述

pattern

string

要匹配的字符串。

flags

标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

函数中flags取值：            例：re.findall(compat,str,flags)

Flag

Meaning

DOTALL,S                    re.S          

Make.match any character, including newlines

使 . 匹配包括换行在内的所有字符

IGNORECASE,I

Do case-insensitive matches

使匹配对大小写不敏感

LOCALE,L                           

Do a locale-aware match

做本地化识别（locale-aware）匹配

MULTILINE,M                  

Multi-line matching, affecting^and$

多行匹配，影响 ^ 和 $

VERBOSE,X

Enable verbose REs, which can be organized more cleanly and understandably.

该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。

UNICODE,U

Makes several escapes like\w,\b,\sand\ddependent on the Unicode character database.

根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.

正则表达式的通配符表示含义：

模式字符串使用特殊的语法来表示一个正则表达式：

字母和数字表示他们自身。一个正则表达式模式中的字母和数字匹配同样的字符串。

多数字母和数字前加一个反斜杠时会拥有不同的含义。

标点符号只有被转义时才匹配自身，否则它们表示特殊的含义。

反斜杠本身需要使用反斜杠转义。

由于正则表达式通常都包含反斜杠，所以你最好使用原始字符串来表示它们。模式元素(如 r'\t'，等价于 '\\t')匹配相应的特殊字符。

下表列出了正则表达式模式语法中的特殊元素。如果你使用模式的同时提供了可选的标志参数，某些模式元素的含义会改变。

模式

描述

^

匹配字符串的开头

$

匹配字符串的末尾。

.

匹配除了换行符(\n)的任意字符，当re.DOTALL标记被指定时，则可以匹配包括换行符的任意字符。

[...]

用来表示一组字符,单独列出：[amk] 匹配 'a'，'m'或'k'

[^...]

不在[]中的字符：[^abc] 匹配除了a,b,c之外的字符。

re*

匹配0个或多个的表达式。

re+

匹配1个或多个的表达式。

re?

匹配0个或1个由前面的正则表达式定义的片段，非贪婪方式

re{ n}

re{ n,}

精确匹配n个前面表达式。

re{ n, m}

匹配 n 到 m 次由前面的正则表达式定义的片段，贪婪方式

a| b

匹配a或b

(re)

G匹配括号内的表达式，也表示一个组

(?imx)

正则表达式包含三种可选标志：i, m, 或 x 。只影响括号中的区域。

(?-imx)

正则表达式关闭 i, m, 或 x 可选标志。只影响括号中的区域。

(?: re)

类似 (...), 但是不表示一个组

(?imx: re)

在括号中使用i, m, 或 x 可选标志

(?-imx: re)

在括号中不使用i, m, 或 x 可选标志

(?#...)

注释.

(?= re)

前向肯定界定符。如果所含正则表达式，以 ... 表示，在当前位置成功匹配时成功，否则失败。但一旦所含表达式已经尝试，匹配引擎根本没有提高；模式的剩余部分还要尝试界定符的右边。

(?! re)

前向否定界定符。与肯定界定符相反；当所含表达式不能在字符串当前位置匹配时成功

(?> re)

匹配的独立模式，省去回溯。

\w

匹配字母数字及下划线，等价于'[A-Za-z0-9_]'。

\W

匹配非字母数字及下划线，等价于 '[^A-Za-z0-9_]'。

\s

匹配任意空白字符，等价于 [\t\n\r\f].

\S

匹配任意非空字符，等价于 [^ \f\n\r\t\v]。

\d

匹配任意数字，等价于 [0-9].

\D

匹配任意非数字，等价于 [^0-9]。

\A

匹配字符串开始

\Z

匹配字符串结束，如果是存在换行，只匹配到换行前的结束字符串。c

\z

匹配字符串结束

\G

匹配最后匹配完成的位置。

\b

匹配一个单词边界，也就是指单词和空格间的位置。例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。

\B

匹配非单词边界。'er\B' 能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'。

\n, \t, 等.

匹配一个换行符。匹配一个制表符。等

\1...\9

匹配第n个分组的内容。

\10

匹配第n个分组的内容，如果它经匹配。否则指的是八进制字符码的表达式。

2.2、常用函数

以下是re模块常用的七个函数：

函数名

含义

实例

re.compile()

将正则表达式模式编译成一个正则表达式对象，它可以用于匹配使用它的match ()和search ()方法，如下所述。

可以通过指定flags值修改表达式的行为。值可以是任何以下变量，使用组合OR（|运算符）。

但使用re.compile()和保存所产生的正则表达式对象重用效率更高时该表达式会在单个程序中多次使用。

语法：compile(pattern, flags=0)

\>>> s = '[a-z]+\d*'

\>>> a = re.compile(s)

\>>> a

<_sre.SRE_Pattern object at 0x0000000003308738>

\>>> type(a)



\>>> b = a.match('a123')

\>>> b.group()

'a123'

等价于：

\>>> b = re.match('[a-z]+\d*', 'a123')

\>>> b.group()

'a123'

re.escape()

返回的字符串与所有非字母数字带有反斜杠；这是有用的如果你想匹配一个任意的文本字符串，在它可能包含正则表达式元字符

简单理解：把字符串按照可能会是正则表达式来理解，这样就需要把特殊字符都转义。这样才能方便匹配时精确匹配每个字符。

字符'[a-z]'这个字符串可以看作是正则表达式的模式，这样就不能作为被匹配的字符串。如果想把这个字符串作为被匹配的模式就需要转义这些特殊字符。print(re.escape('[a-z]'))



a\-za\-z



语法：escape(pattern)

\>>> s = 'abc.|123'

\>>> print s

abc.|123

\>>> print(re.escape(s))

abc\.\|123

re.findall()

作为一个字符串列表，在字符串中，返回所有非重叠匹配的模式。该字符串是从左到右扫描的，匹配按照发现的顺序返回。如果一个或多个组是本模式中，返回一个列表的群体 ；如果该模式具有多个组，这将是元组的列表。空匹配包含在结果中，除非他们接触到另一场匹配的开头。

返回一个匹配的所有内容的列表。如果没有匹配内容则返回空列表。

在 1.5.2 版本新。

2.4 版本中的更改：添加可选的标志参数。

语法：findall(pattern, string, flags=0)

\>>> a = 'abc,123.abc.123'

\>>> s = '[a-z]+'

\>>> r = re.findall(s,a)

\>>> r

['abc', 'abc']

re.match()

如果在字符串的开头的零个或更多字符匹配这个正则表达式，将返回相应的作法实例。返回没有如果，则该字符串与模式不匹配请注意这是不同于零长度匹配。

简单理解：就是从字符串的开始做正则匹配。能匹配到的最大位置返回。返回的对象用group/groups方法读取。可以不匹配到字符串的末尾。但是字符串的开始必须匹配，否则返回空字符串。

语法：match(pattern, string, flags=0)

\>>> s = '[a-z]*'

\>>> a = 'test123'

\>>> b = re.match(s,a)

\>>> b.group()

'test'

\>>> a = '123abc'

\>>> b = re.match(s,a)

\>>> b.group()

''

re.search()

扫描字符串寻找第一个匹配位置，在此正则表达式产生的匹配，并返回相应的MatchObject实例。如果没有字符串中的位置匹配模式返回空 。

可选的第二个参数pos给索引在字符串中搜索在哪里开始；它将默认为0。这并不完全等于切片的字符串 ；' ^'模式字符匹配在真正开始的字符串和位置刚换行，但不是一定是在开始搜索的索引。

可选参数endpos限制了多远的字符串将被搜索 ；它将，如果字符串是endpos个字符长，因此，只有从pos到字符endpos - 1将搜索匹配项。如果endpos小于pos，没有比赛会发现，否则，如果rx是已编译的正则表达式对象，rx.search（字符串，0，50)相当于rx.search（字符串[：50]，0)。

注意：如果查找字符时用*则会默认匹配0个对应的字符。这样就会返回空字符串。

语法：search(pattern, string, flags=0)

\>>> s = '\d*'

\>>> a = 'abc123,31'

\>>> s = re.search(s,a)

\>>> s.group()

''

\>>> s.span()

(0, 0)

\>>> s = '\d+'

\>>> s = re.search(s,a)

\>>> s.span()

(3, 6)

\>>> s.group()

'123'

re.split()

将字符串拆分的模式的匹配项。如果在模式中使用捕获括号，则然后也作为结果列表的一部分返回的文本模式中的所有组。如果maxsplit不为零，顶多maxsplit分裂发生，并且该字符串的其余部分将作为列表的最后一个元素返回。（不兼容性说明： 在原始的Python 1.5版本中，maxsplit被忽略。这已被固定在以后的版本。）

语法：split(pattern, string, maxsplit=0, flags=0)

\>>> text = """Ross McFluff: 834.345.1254 155 Elm Street

... Ronald Heathmore: 892.345.3428 436 Finley Avenue

... Frank Burger: 925.541.7625 662 South Dogwood Way

... Heather Albrecht: 548.326.4584 919 Park Place"""

\>>> entries = re.split("\n+", text)

\>>> entries

['Ross McFluff: 834.345.1254 155 Elm Street',

'Ronald Heathmore: 892.345.3428 436 Finley Avenue',

'Frank Burger: 925.541.7625 662 South Dogwood Way',

'Heather Albrecht: 548.326.4584 919 Park Place']

\>>> [re.split(":? ", entry, 3) for entry in entries]

[['Ross', 'McFluff', '834.345.1254', '155 Elm Street'],

['Ronald', 'Heathmore', '892.345.3428', '436 Finley Avenue'],

['Frank', 'Burger', '925.541.7625', '662 South Dogwood Way'],

['Heather', 'Albrecht', '548.326.4584', '919 Park Place']]

\>>> [re.split(":? ", entry, 4) for entry in entries]

[['Ross', 'McFluff', '834.345.1254', '155', 'Elm Street'],

['Ronald', 'Heathmore', '892.345.3428', '436', 'Finley Avenue'],

['Frank', 'Burger', '925.541.7625', '662', 'South Dogwood Way'],

['Heather', 'Albrecht', '548.326.4584', '919', 'Park Place']]

re.sub()

Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.如果pattern没有被找到，string不变。repl可以是一个字符串或一个函数；如果是一个字符串,任何反斜杠转义都会实现。那就是，\n会转化成一个换行符，\r会转化成一个回车，等等。 未知的转义字符例如\j不做处理。

简单理解：按照规则pattern匹配字符串string，匹配的字符串按照规则repl来替换。替换后和原来字符串组合返回。repl可以使字符串也可以是函数。

语法：sub(pattern, repl, string, count=0, flags=0)

\>>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\s∗\s∗:',

...r'static PyObject*\npy_\1(void)\n{',

...'def myfunc():')

'static PyObject*\npy_myfunc(void)\n{'

\>>> def dashrepl(matchobj):

...if matchobj.group(0) == '-': return ' '

...else: return '-'

\>>> re.sub('-{1,2}', dashrepl, 'pro----gram-files')

'pro--gram files'

\>>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)

'Baked Beans & Spam'

2.2、函数汇总

注意：python3中新增一个函数：

re.fullmatch()，这个函数和re.match()的不同之处是需要全部匹配才能返回字符串。如果没有全部匹配则返回空。

序号

函数名

作用

实例

1

re.DEBUG

显示正则表达式的调试信息

\>>> s = '\d\W'

\>>> r = re.compile(s, re.DEBUG)

in

category category_digit

in

category category_not_word

2

re.DOTALL

使'.'特殊字符匹配任何字符，包括换行 ；如果没有此标志，'.'将匹配除换行符的任何内容。

\>>> s = '.*'

\>>> r = re.match(s,'a.123\nabc')

\>>> r.group()

'a.123'

\>>> r = re.match(s,'a.123\nabc',re.DOTALL)

\>>> r.group()

'a.123\nabc'

3

re.I

测试和re.IGNORECASE作用相同是re.IGNORECASE的简写模式

\>>> r = re.match('a*','aA',re.I)

\>>> r.group()

'aA'

4

re.IGNORECASE

执行不区分大小写的匹配 ；如[A-Z]表达式将太匹配小写字母。这不被受当前的区域设置。

\>>> r = re.match('a*','aA',re.IGNORECASE)

\>>> r.group()

'aA'

5

re.L

和re.LOCALE作用相同。是re.LOCALE简写模式

6

re.LOCALE

使用当前环境的\w, \W, \b, \B, \s and \S

7

re.M

8

re.MULTILINE

当指定时，模式字符' ^'匹配字符串的开头以及每个行的开头（紧接每个换行符）； 模式字符'$'匹配字符串的末尾以及每一行的结尾（紧靠每个换行符之前）。

默认情况下，'^'只匹配字符串的开始，'$'只匹配字符串的末尾和字符串末尾换行符（如果有的话）之前的位置

9

re.S

作用和re.DOTALL相同。使'.'特殊字符匹配任何字符，包括换行 ；如果没有此标志，'.'将匹配除换行符的任何内容。

\>>> s = '.*'

\>>> r = re.match(s,'a.123\nabc')

\>>> r.group()

'a.123'

\>>> r = re.match(s,'a.123\nabc',re.S)

\>>> r.group()

'a.123\nabc'

10

re.Scanner

11

re.T

12

re.TEMPLATE

13

re.U

和re.UNICODE作用相同

14

re.UNICODE

使得\w, \W, \b, \B, \d, \D, \s和\S取决于UNICODE定义的字符属性

15

re.VERBOSE

此标志允许您编写正则表达式，看起来更好。在模式中的空白将被忽略，除非当在字符类或者前面非转义反斜杠，和，当一条线包含一个'#'既不在字符类中或由非转义反斜杠，从最左侧的所有字符之前，这种'#'通过行末尾将被忽略。

这意味着两个以下正则表达式匹配的对象，一个十进制数是相同的功能：

a = re.compile(r"""\d +# the integral part

\.# the decimal point

\d *# some fractional digits""", re.X)

b = re.compile(r"\d+\.\d*")

16

re.X

17

re._MAXCACHE

18

re.__all__

19

re.__class__()

20

re.__delattr__()

21

re.__dict__

22

re.__doc__

23

re.__file__

24

re.__format__()

25

re.__getattribute__()

26

re.__hash__()

27

re.__init__()

28

re.__name__

29

re.__new__()

30

re.__package__

31

re.__reduce__()

32

re.__reduce_ex__()

33

re.__repr__()

34

re.__setattr__()

35

re.__sizeof__()

36

re.__str__()

37

re.__subclasshook__()

38

re.__version__

39

re._alphanum

40

re._cache

41

re._cache_repl

42

re._compile()

43

re._compile_repl()

44

re._expand()

45

re._locale

46

re._pattern_type()

47

re._pickle()

48

re._subx()

49

re.compile()

将正则表达式模式编译成一个正则表达式对象，它可以用于匹配使用它的match ()和search ()方法，如下所述。

可以通过指定flags值修改表达式的行为。值可以是任何以下变量，使用组合OR（|运算符）。

但使用re.compile()和保存所产生的正则表达式对象重用效率更高时该表达式会在单个程序中多次使用。

语法：compile(pattern, flags=0)

\>>> s = '[a-z]+\d*'

\>>> a = re.compile(s)

\>>> a

<_sre.SRE_Pattern object at 0x0000000003308738>

\>>> type(a)



\>>> b = a.match('a123')

\>>> b.group()

'a123'

等价于：

\>>> b = re.match('[a-z]+\d*', 'a123')

\>>> b.group()

'a123'

50

re.copy_reg

帮助提供pickle/cPickle的可扩展性。

51

re.error()

正则表达式异常，当一个字符串传递给这里的函数之一时引发的异常不是有效的正则表达式 （例如，它可能包含不匹配的括号） 或其他一些错误在编译或匹配过程中发生的时。如果一个字符串包含不匹配的一种模式，它永远不会是一个错误。

52

re.escape()

返回的字符串与所有非字母数字带有反斜杠；这是有用的如果你想匹配一个任意的文本字符串，在它可能包含正则表达式元字符

简单理解：把字符串按照可能会是正则表达式来理解，这样就需要把特殊字符都转义。这样才能方便匹配时精确匹配每个字符。

字符'[a-z]'这个字符串可以看作是正则表达式的模式，这样就不能作为被匹配的字符串。如果想把这个字符串作为被匹配的模式就需要转义这些特殊字符。print(re.escape('[a-z]'))



a\-za\-z



语法：escape(pattern)

\>>> s = 'abc.|123'

\>>> print s

abc.|123

\>>> print(re.escape(s))

abc\.\|123

53

re.findall()

作为一个字符串列表，在字符串中，返回所有非重叠匹配的模式。该字符串是从左到右扫描的，匹配按照发现的顺序返回。如果一个或多个组是本模式中，返回一个列表的群体 ；如果该模式具有多个组，这将是元组的列表。空匹配包含在结果中，除非他们接触到另一场匹配的开头。

返回一个匹配的所有内容的列表。如果没有匹配内容则返回空列表。

在 1.5.2 版本新。

2.4 版本中的更改：添加可选的标志参数。

语法：findall(pattern, string, flags=0)

\>>> a = 'abc,123.abc.123'

\>>> s = '[a-z]+'

\>>> r = re.findall(s,a)

\>>> r

['abc', 'abc']

54

re.finditer()

返回一个迭代器符合MatchObject情况 在RE模式字符串中的所有非重叠的匹配。该字符串是扫描的左到右，和按发现的顺序返回匹配。空匹配包含在结果中，除非他们接触的另一个匹配的开头。

新版本2.2中的。

2.4版本中的更改：添加可选的标志参数。

\>>> a = 'testestest'

\>>> s = 'test'

\>>> r = re.finditer(s,a)

\>>> c = r.next()

\>>> c.group()

'test'

\>>> c = r.next()

\>>> c.group()

'test'

\>>> c = r.next()

Traceback (most recent call last):

File "", line 1, in

StopIteration

\>>> text = "He was carefully disguised but captured quickly by police."

\>>> for m in re.finditer(r"\w+ly", text):

...print '%02d-%02d: %s' % (m.start(), m.end(), m.group(0))

07-16: carefully

40-47: quickly

55

re.match()

如果在字符串的开头的零个或更多字符匹配这个正则表达式，将返回相应的作法实例。返回没有如果，则该字符串与模式不匹配请注意这是不同于零长度匹配。

简单理解：就是从字符串的开始做正则匹配。能匹配到的最大位置返回。返回的对象用group/groups方法读取。可以不匹配到字符串的末尾。但是字符串的开始必须匹配，否则返回空字符串。

语法：match(pattern, string, flags=0)

\>>> s = '[a-z]*'

\>>> a = 'test123'

\>>> b = re.match(s,a)

\>>> b.group()

'test'

\>>> a = '123abc'

\>>> b = re.match(s,a)

\>>> b.group()

''

56

re.purge()

清除正则表达式缓存。

57

re.search()

扫描字符串寻找第一个匹配位置，在此正则表达式产生的匹配，并返回相应的MatchObject实例。如果没有字符串中的位置匹配模式返回空 。

可选的第二个参数pos给索引在字符串中搜索在哪里开始；它将默认为0。这并不完全等于切片的字符串 ；' ^'模式字符匹配在真正开始的字符串和位置刚换行，但不是一定是在开始搜索的索引。

可选参数endpos限制了多远的字符串将被搜索 ；它将，如果字符串是endpos个字符长，因此，只有从pos到字符endpos - 1将搜索匹配项。如果endpos小于pos，没有比赛会发现，否则，如果rx是已编译的正则表达式对象，rx.search（字符串，0，50)相当于rx.search（字符串[：50]，0)。

注意：如果查找字符时用*则会默认匹配0个对应的字符。这样就会返回空字符串。

语法：search(pattern, string, flags=0)

\>>> s = '\d*'

\>>> a = 'abc123,31'

\>>> s = re.search(s,a)

\>>> s.group()

''

\>>> s.span()

(0, 0)

\>>> s = '\d+'

\>>> s = re.search(s,a)

\>>> s.span()

(3, 6)

\>>> s.group()

'123'

58

re.split()

将字符串拆分的模式的匹配项。如果在模式中使用捕获括号，则然后也作为结果列表的一部分返回的文本模式中的所有组。如果maxsplit不为零，顶多maxsplit分裂发生，并且该字符串的其余部分将作为列表的最后一个元素返回。（不兼容性说明： 在原始的Python 1.5版本中，maxsplit被忽略。这已被固定在以后的版本。）

语法：split(pattern, string, maxsplit=0, flags=0)

\>>> text = """Ross McFluff: 834.345.1254 155 Elm Street

... Ronald Heathmore: 892.345.3428 436 Finley Avenue

... Frank Burger: 925.541.7625 662 South Dogwood Way

... Heather Albrecht: 548.326.4584 919 Park Place"""

\>>> entries = re.split("\n+", text)

\>>> entries

['Ross McFluff: 834.345.1254 155 Elm Street',

'Ronald Heathmore: 892.345.3428 436 Finley Avenue',

'Frank Burger: 925.541.7625 662 South Dogwood Way',

'Heather Albrecht: 548.326.4584 919 Park Place']

\>>> [re.split(":? ", entry, 3) for entry in entries]

[['Ross', 'McFluff', '834.345.1254', '155 Elm Street'],

['Ronald', 'Heathmore', '892.345.3428', '436 Finley Avenue'],

['Frank', 'Burger', '925.541.7625', '662 South Dogwood Way'],

['Heather', 'Albrecht', '548.326.4584', '919 Park Place']]

\>>> [re.split(":? ", entry, 4) for entry in entries]

[['Ross', 'McFluff', '834.345.1254', '155', 'Elm Street'],

['Ronald', 'Heathmore', '892.345.3428', '436', 'Finley Avenue'],

['Frank', 'Burger', '925.541.7625', '662', 'South Dogwood Way'],

['Heather', 'Albrecht', '548.326.4584', '919', 'Park Place']]

59

re.sre_compile

60

re.sre_parse

61

re.sub()

Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.如果pattern没有被找到，string不变。repl可以是一个字符串或一个函数；如果是一个字符串,任何反斜杠转义都会实现。那就是，\n会转化成一个换行符，\r会转化成一个回车，等等。 未知的转义字符例如\j不做处理。

简单理解：按照规则pattern匹配字符串string，匹配的字符串按照规则repl来替换。替换后和原来字符串组合返回。repl可以使字符串也可以是函数。

语法：sub(pattern, repl, string, count=0, flags=0)

\>>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\s∗\s∗:',

...r'static PyObject*\npy_\1(void)\n{',

...'def myfunc():')

'static PyObject*\npy_myfunc(void)\n{'

\>>> def dashrepl(matchobj):

...if matchobj.group(0) == '-': return ' '

...else: return '-'

\>>> re.sub('-{1,2}', dashrepl, 'pro----gram-files')

'pro--gram files'

\>>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)

'Baked Beans & Spam'

62

re.subn()

执行相同的操作，如sub()，但返回一个元组（new_string，number_of_subs_made)。

2.7版本中的更改：添加可选的标志参数。

语法：subn(pattern, repl, string, count=0, flags=0)

63

re.sys

64

re.template()

2.3、函数返回的MatchObject对象的内置函数

search、match返回对象是MatchObject或者是None。

findall返回对象是列表。列表每个元素都是一个可以匹配的一段子串。

如果是MatchObject则这个对象的内置函数包括：

序号

函数名

作用

1

re.__class__()

2

re.__copy__()

3

re.__deepcopy__()

4

re.__delattr__()

5

re.__doc__

6

re.__format__()

7

re.__getattribute__()

8

re.__hash__()

9

re.__init__()

10

re.__new__()

11

re.__reduce__()

12

re.__reduce_ex__()

13

re.__repr__()

14

re.__setattr__()

15

re.__sizeof__()

16

re.__str__()

17

re.__subclasshook__()

18

re.end()

返回这个对象的内容长度

19

re.endpos

20

re.expand()

21

re.group()

返回对象匹配的内容，这是所有内容。如果匹配的正则表达式分组了，那么这个函数返回的值就是元组，元组每个元素都是匹配的一个子串

22

re.groupdict()

23

re.groups()

如果匹配的正则表达式分组了，那么可以用这个函数返回指定组名的字符串。默认时组0

24

re.lastgroup

最后一个分组内容

25

re.lastindex

26

re.pos

27

re.re

28

re.regs

29

re.span()

返回这个对象匹配的字符串在源字符串的起始和结束的索引值，以元组形式返回

30

re.start()

返回匹配结果的内容匹配到源字符串的起始位置的索引值，返回整型

31

re.string

返回源字符串。

三、注意事项

3.1、match、fullmatch、findall、finditer、search

match是根据传入的正则表达式匹配对应的字符串。并且是从开始字符匹配。匹配到字符不能匹配的位置然后返回匹配的对象。返回的对象是MatchObject或者空。

fullmatch，和match的区别是fullmatch必须是目标字符串从开始到结束全部都匹配这个传入的正则表达式才可以返回匹配对象。否则返回空。返回的对象也是MatchObject对象。

findall，从字符串中从前向后依次查找匹配正则表达式的子串。最后把多个匹配的子串用列表形式返回。列表的每个元素是一个匹配的子串。

finditer，和findall功能相同。但是finditer返回的是一个可迭代对象。可以用next()方法读取。然后再用group方法读取匹配的内容。

search，是从前向后依次扫描整个字符串。返回第一个匹配的子串。匹配位置不一定是开始字符。但是如果用*来表示0-n次重复时需要测试。有时候会返回空字符串。