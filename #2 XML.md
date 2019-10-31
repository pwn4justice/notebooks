# #2 XML

## XML - eXtensible Markup Language 可扩展标记语言

- 和 HTML 很相似，但 HTML **相当于** 其子集（用XML甚至可以创造出一个HTML语言来）

- 功能：传输、存储数据；不像 HTML 用来显示给用户的

- 应用很广泛，虽然直接与用户打交道不多

- 优点：

    - 以纯文本格式进行存储，因此是独立于软件和硬件的
    - 对不同的应用程序有很好的兼容性
    - 使得平台变更也很容易
    - 能创建新的其他语言，如：
        - RSS
        - XHTML
        - WSDL
        - WAP和WML、OWL等

- 组成：

    - 元素（根元素，子元素...）
    - 实体（特殊字符**转义**成实体）
    - 属性
    - 文本
        - PCDATA（要被解析的文本，将被解析起检查实体及标记，文本中的标签会被当作标记处理，实体会被展开，所以不应该包含任何 & < > 等字符，需要用 `&amp;` 等来替代）
        - CDATA（字符文本，不解析，不会被执行）

- 语法规则：

    - 必须包含一个根元素
    - XML 声明必须放在首行（如果存在的话）：`<?xml version="1.0" encoding="utf-8"?>`
    - 所有元素都得有关闭标签，XML 声明不用，因为它不是文档的一部分
    - 标签大小写敏感
    - 标签必须正确嵌套
    - 属性值必须加引号（要么单引号，要么双引号，要么用实体转义：`&amp;`  `&lt;`  `&gt;`  这些）
        - 还有：`'` : `&apos;`  和 `"` : `&quot;` 
        - 注释：`<!-- This is a comment -->`
    - XML 中空格不像 HTML 中那样被吃掉
    - XML 会以 LF 来换行，和 Unix 系统一致

- 命名规则：和常见编程语言的变量命名差不多，最好不要太长，也不要包含：-、.、: 等这些符号

- XML 的元素可以"扩展"：意味着当此 XML 被使用时，依然可以增添子元素什么的，不对正在运行的程序产生影响

- 属性，最好包含的是"元数据"，就是一些程序中不太会用到的数据，如果没有这样的数据，最好都写成子元素的形式

- 一个良好的范例：(越具体的话，解析越方便)

    ```
    <note>
    <date>
    <day>10</day>
    <month>01</month>
    <year>2008</year>
    </date>
    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend!</body>
    </note>
    ```

- XML 的验证：使用 DTD 验证，如果通过则称为“合法”的或“形式良好”的 XML

- XML 语法没有通过浏览器验证的话，即产生了错误，是会被终止，拒绝显示的

- 可以直接通过浏览器或者文本编辑软件打开、查看 XML 文件，当一个错误的 XML 被打开时，浏览器会报错，不显示，但可以通过查看页面源代码的形式来查看

- 可以像 CSS 美化 HTML 那样来用 CSS 美化 XML

    - 加上：`<?xml-stylesheet type="text/css" herf="xxx.css"?>`
    - 此法不常用，推荐的是使用 XSLT 来（美化）显示 XML

- XSLT：eXtensible Stylesheet Language Transformations，比 CSS 完善，会在浏览器显示 XML 之前将其转换为 HTML，但是不同的 XSLT 实现可能不同，所以为了避免不用浏览器产生不同结果，可以在服务器上进行 XSLT 转换



<br />

## XML DOM









<br/>

## DTD

DTD - 文档类型定义，可被成行的声明在 XML 文档中，也可以独立出来，作为一个外部引用

### 当包含在 XML 文件中时

声明语法如下：

```xml
<!DOCTYPE root-element [
...
element-declarations
...
]>
```

一个实例：

```xml
<?xml version="1.0"?>
<!DOCTYPE note [
<!ELEMENT note (to, from, heading, body)>		<!-- 元素定义，以下的子元素必须按括号里的顺序声明 -->
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
]>

<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

### 当在外部文件定义时

语法：

```xml
<!DOCTYPE root-element SYSTEM "filename.dtd">
```

实例：

```xml
<?xml version="1.0"?>
<!DOCTYPE note SYSTEM "note.dtd">
<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

而 note.dtd 文件内容如下：

```dtd
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
```







