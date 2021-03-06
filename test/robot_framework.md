# Robot Framework




## 变量
### 定义变量

3种变量类型

* 标量scalars - ${SCALAR}
* 列表lists - @{LIST}
* 字典dictionaries - &{DICT}

另外，环境变量可以直接使用语法 %{ENV_VAR} 进行访问

变量和关键字一样，大小写敏感;空格和下划线会被忽略


建议:
* 全局变量使用大写，如${PATH} or ${TWO WORDS}
* 只在某用例或关键字中使用的变量使用小写，如 ${my var} or ${myVar}


标量

* 标量变量${EXAMPLE}， 值以"as-is"的方式被直接使用


列表

* @{NAME}[index]访问列表中的单个元素
* 列表变量@{EXAMPLE}, 单个的list item被分别传递给关键字

字典

* 字典变量&{EXAMPLE}, 单个的dict item被分别以命名参数形式()传递给关键字
* &{NAME}[key]访问字典中的单个元素

环境变量

* %{ENV_VAR_NAME}直接访问环境变量
* 环境变量都被认为为字符串
* 环境变量在测试执行之前，在操作系统中被设置，在执行过程中一直可用
* 环境变量是全局的，在一个用例中被设置，后续执行的用例都可以使用
* 对于环境变量的改变，在测试结束后将失效


Syntax for variable definition is quite simple, as seen in this variable table:

```
*** Variables ***
${USERNAME}               janedoe
${PASSWORD}               J4n3D0e
${NEW PASSWORD}           e0D3n4J1. . 
${DATABASE FILE}          ${TEMPDIR}${/}robotframework-quickstart-db.txt
${PWD INVALID LENGTH}     Password must be 7-12 characters long
${PWD INVALID CONTENT}    Password must be a combination of lowercase and uppercase letters and numbers


```


Variables can also be given from the command line which is useful if the tests need to be executed in different environments.

```
robot --variable USERNAME:johndoe --variable PASSWORD:J0hnD0e QuickStart.rst

```


Robot Framework has its own variables that can be used as scalars, lists or dictionaries using syntax 
```${SCALAR}, @{LIST} and &{DICT}```, respectively. In addition to this, environment variables can be used directly with syntax %{ENV_VAR}.



### Setting variables in command line
```
--variable EXAMPLE:value
--variable HOST:localhost:7272 --variable USER:robot
--variable ESCAPED:Qquotes_and_spacesQ --escape quot:Q --escape space:_
```



## Organizing test cases

测试用例的组织层次结构如下:
1. 在测试用例文件(test case file)中建立测试用例2. 一个测试文件自动的建成一个包含了这些测试用例的测试集(test suite)3. 一个包含多个测试用例文件(test case file)的目录构成更高级的测试集，即这个测试集目录包含多个子测试集，而子测试集即是由测试文件创建而来。4. 一个测试集目录可以包 其他测试集目录，这种层次结构可以满足层嵌套的需要5. 测试集目录可以有一个特殊的初始文件(initialization file) 

此外，还有:
1. 测试库(Test libraries)包含最低级的关键字(keywords)2. 资源文件(Resource files)包含变量和更高层次的用户自定义关键字   
3. 变量文件(Variable files)可以提供比资源文件更灵活的方式创建变量

### 初始化文件
A test suite created from a directory can have similar settings as a suite created from a test case file. Because a directory alone cannot have that kind of information, it must be placed into a special test suite initialization file. An initialization file name must always be of the format \__init__.ext, where the extension must be one of the supported file formats (for example, __init__.robot or __init__.html). The name format is borrowed from Python, where files named in this manner denote that a directory is a module.

Initialization files have the same structure and syntax as test case files, except that they cannot have test case tables and not all settings are supported. Variables and keywords created or imported in initialization files are not available in the lower level test suites. If you need to share variables or keywords, you can put them into resource files that can be imported both by initialization and test case files.
在初始文件中引入或创建的变量和关键字在低级 的测试集中是不可用的，如果引入的资源文件需要在低 级 的测试集中共享的话，资源文件是可以使用的。

The main usage for initialization files is specifying test suite related settings similarly as in test case files, but setting some test case related settings is also possible. 

```
*** Settings ***
Documentation    Example suite
Suite Setup      Do Something    ${MESSAGE}
Force Tags       example
Library          SomeLibrary

*** Variables ***
${MESSAGE}       Hello, world!

*** Keywords ***
Do Something
    [Arguments]    ${args}
    Some Keyword    ${arg}
    Another Keyword

```

### 资源文件
资源文件是在设置表格中被引入的。资源文件的路径放在设置名称的后面。假如使用绝对路径，资源文件可以被直接使用。否则，首先是在导入该资源的文件的所在目录去搜索相关 的路径，假如没找到，然后在 PYTHONPATH 路径下搜索。这个路径可以包 变量，建议使用操作系统无 关的路径(例如:${RESOURCES}/login_resources.html 或${RESOURCE_PATH})。这样，路径中的斜杠(/) 在 Windows 中自动转变为反斜杠(\)。

资源文件的高层架构同测试用例文件是相同的，但是，它不包括测试用例表格。资源文件中的设置表格可以仅引入设置((Library, Resource, Variables)和注释。变量表格和关键字表格同测试用例文件中一样使用。假如多个资源文件包 多个相同名称的用户关键字，则他们的使用必须在关键字前面加上资源文件名称(例 如:myresources.Some Keyword 和 common.Some Keyword)。而且，假如资源文件包 相同的变量，则第一 个引入的将被使用。


### Setups and teardowns

1. Test Setup
2. Test Teardown
3. Suite Setup
4. Suite Teardown

### Using tags
1. Force Tags
2. Default Tags
3. [Tags]


### 关键字
位于第一列的用户关键字名称同测试用例名称类似。用户关键字可以通过关键字创建，可以是测试库中的关键字也可以是其它的用户关键字。关键字名称通常在第二列中，但是当设置关键 字返回值时，他们在其后的列中

|Keyword|Action|Argument|Argument|
| --- | --- | ---| ---|
|Title Shoule Start With| [Argument]|${expected}='default'|
||${title}=|GetTitle|
||Should Start With|${title}|${expected}|

```
	[Documentation]: 用于关键字的注释	[Arguments]:指明用户关键字的参数。	[Return]:指明用户关键字的返回值	[Timeout]:  设置用户关键字的可能超时。超时将在它们自己的章节中介绍

```

* 参数添加默认值：即在等号(=)后跟默认的值。例如:${arg}=default。 这里可以有多个参数有默认值，但是他们必须在正常位置参数后面；
* 可变数量参数：@{ varargs }。这种语法可以同位置参数和默认值参数组合使用，在最后的列表变量会获取剩余的没有被匹配的参数。
* 关键字名称嵌入参数：使用嵌入式参数只需要关键字的名字如 Select ${animal} from list 即可。使用嵌入式参数的关键字不能有任何的普通参数(使用[Arguments]设置的)。嵌入式参数不支持默认值，但与传统参数一样支持可变数量参数。


用户关键字也可以返回值。返回值使用[Return]定义。该值可以赋给测试用例中的变量或其他关键字。用户关键字也可以返回多个值，可以一次性赋给多个标量变量或一个列表变量或标量变量和列表变 量。返回多个值是将指定的值放在[Return]后面的不同单元格。

测试用例文件和测试集初始化文件中的用户关键字和变量只能在创建它们的文件中使用，但是资源文件提 供了共享他们的机制。由于资源文件很接近于测试用例文件，因此很容易创建它们。