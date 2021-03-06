# URI 和 URL

**[URI](https://tools.ietf.org/html/rfc3986) **: Uniform Resource Identifier - 统一资源标识符

> URI是一系列紧凑字符组成的，它用来标识一个抽象或者物理资源。
> 
> 例如身份证号，它可以标识一个独一无二的人。

**[URL](https://tools.ietf.org/html/rfc1738) **: Uniform Resource Locators - 统一资源定位符

> URL是用来定位和访问因特网上资源的。

URL是URI的子集。



## URI 语法及编码



### URI语法

```text
URI         = scheme ":" hier-part [ "?" query ] [ "#" fragment ]

hier-part   = "//" authority path-abempty
                / path-absolute
                / path-rootless
                / path-empty
```



### URI编码

通常如果一样东西需要编码，那么就说明这样东西并不适合传输。原因多种多样，如size过大，包含隐私数据，**对于URI来说，之所以要进行编码，是因为URI中有些字符会引起歧义**。例如URL参数字符串中使用key=value键值对这样的形式来传参，键值对之间以&符号分隔，如/s?q=abc&ie=utf-8。如果你的value字符串中包含了=或者&，那么势必会造成接收URL的服务器解析错误，因此必须将引起歧义的&和=符号进行转义，也就是对其进行编码。又如，URL的编码格式采用的是ASCII码，而不是Unicode，这也就是说你不能在URL中包含任何非ASCII字符，例如中文。否则如果客户端浏览器和服务端浏览器支持的字符集不同的情况下，中文可能会造成问题。**URI编码的原则就是使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。**

RFC3986文档规定，URI中只允许包含下面几种字符：

- 英文字母（a-zA-Z）

- 数字（0-9）

- 中横线(`“-”`)、下划线(`“_”`)、英文句号(`“.”`)、英文波浪号(`“~”`) 四个特殊字符

- 保留字符(`":" / "/" / "?" / "#" / "[" / "]" / "@" "!" / "$" / "&" / "'" / "(" / ")" / "*" / "+" / "," / ";" / "="`)

百分比编码机制用于表示数据中的一个字节（八比特） 该八位位组的相应字符在 允许的集合，或被用作定界符或在定界符之内 零件。

百分比编码由`三元组`组成，即百分号“％” 加上后跟两个代表该一个字节数值的十六进制数字。例如，“％20”表示二进制码 “ 00100000”，在US-ASCII中对应于空格字符（SP）。

```palin
pct-encoded = "%" HEXDIG HEXDIG
```

 十六进制大写字母"A~F"等效于小写字母"a~f"。如果两个URI 仅在百分比编码中使用的十六进制数字大小写不同，那么它们是同一个URI。为了保持一致，应该使用大写字母。





参考文章:

[url 编码（percentcode 百分号编码） - 海王 - 博客园](https://www.cnblogs.com/leaven/archive/2012/07/12/2588746.html)




