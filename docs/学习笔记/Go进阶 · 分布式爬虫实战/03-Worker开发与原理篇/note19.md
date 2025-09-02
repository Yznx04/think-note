# 19-从正则表达式到CSS选择器，四种网页文本处理手段

## strings

go提供了标准库Strings用于处理字符及其函数。常用的包括：

- func Contains(s, substr string) bool // 字符串s中是否包含子字符串substr, 返回bool类型
- func ContainsAny(s, chars string) bool // 字符串中是否包含chars中的任意字符，返回bool类型
- func ContainsRune(s string, r rune) bool // 字符串中是否包含Rune类型的值，返回bool类型
- func Fields(s string) []string // 将字符串以空白字符切分，返回一个字符切片
- func FieldsFunc(s string, f func(r rune) bool) []string // 将字符串以满足f(r) == true的字符分割，返回一个字符切片
- func Split(s, sep string) []string // 将s以sep为分隔符进行分割，分割后字符末尾去掉sep

标准库strconv包中还有很多类型之间相互转换的函数：

- func Atoi(s string) (int, error) // 字符串转化为十进制整数
- func ParseInt(s string, base int, bitSize int) (i int64, err error) // 字符串转化为某一进制的整数，例如八进制、十进制
- func Itoa(i int) string // 整数转换为字符串
- func FormatInt(i int64, base int) string // 某一进制的整数转换为字符串

字符串本质上是字符数组，所以，bytes标准库中有很多类似的函数。

## 字符编码

网络中，服务器将HTML内容以二进制的方式进行传输，需要考虑编码的问题，目前大部分网页都采取了UTF-8的编码方式，Go中默认的编码方式也是UTF-8,但是不排除
比较老的网页使用其他编码方式。

## 正则表达式

正则表达式是一种描述文本组成内容规律的表示方式，可以描述或者匹配符合相应规则的字符串。在文本编辑器、命令行工具、高级程序语言中，正则表达式被广泛用来
校验数据的有效性、搜索或者替换特定模式的字符串。

由于历史原因，正则表达式分为两个流派：POSIX流派和PCRE流派。其中POSIX又有两个流派：BRE标准、ERE标准。不同流派和标准对应了不同的特性和工具。

目前Linux和Mac在原生集成GNU套件（例如 grep命令时），遵从了POSIX流派，同时弱化了BRE和ERE之间的区别。

BRE和ERE之间的差别主要体现在一些语法字符是否需要转义上。其中BRE模式：

```
cat 1.log | grep 'd\{1, 3\}'
```

ERE模式：

```
cat 1.log | grep -E 'd{1, 3}'
```

另一种更加流行的是PCRE流派。PCRE标准是由perl这门语言衍生而来的，现阶段，大部分高级编程语言都使用了PCRE标准。Go中，正则表达式默认是PCRE标准，
不过Go也支持POSIX标准。PCRE示例

```
cat 1.log | grep -P '\d+'
```

正则表达式具有复杂、不易理解、消耗资源多的问题。


## XPath

XPath定义了一种遍历XML文档中节点层次结构并返回匹配元素的灵活方法。XML是一种可扩展标记语言，表示结构化信息的一种规范。

## CSS选择器

CSS（层叠式样式表）是一种定义HTML文档中元素样式的语言。在CSS文件中，我们可以定义一个或者多个HTML中的标签的路径，并指定这些标签的样式。在CSS中，
定义标签路径的方法被称为CSS选择器。

官方不支持CSS选择器，需要使用第三方库。

```
go get github.com/PuerkitoBio/goquery
```

