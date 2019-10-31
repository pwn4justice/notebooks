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



PASS

PASS

PASS





<br/>

## DTD

DTD - 文档类型定义，可被成行的声明在 XML 文档中，也可以独立出来，作为一个外部引用

<br />

### DTD 包含哪些内容（怎么造出一个 DTD）

**1. 声明元素**

形如：

`<!ELEMENT 元素名称 catagory>` <br/>或者 `<!ELEMENT 元素名称 (元素内容)>`

的方式可以声明一个**元素**（Element）：<br />如果想声明一个**空元素**，可以使用：`<!ELEMENT br EMPTY>`，在 XML 文档里使用空元素就像：`<br />`，<br/>如果想声明一个**只有PCDATA的元素**，可以使用：`<!ELEMENT 元素名 (#PCDATA)>`，<br />如果想声明一个**带有任何内容的元素**，可以使用：`<!ELEMENT 元素名 ANY>`，<br />如果想声明一个**带有子元素（序列）的元素**，可以使用：`<!ELEMENT 元素名 (child1 [, ...])>`，当子元素按照由逗号分隔开的序列进行声明时，这些子元素必须按照相同的顺序出现在文档中。<br/>如果想声明**只出现一次的元素**，可以使用：`<!ELEMENT 元素名 (child-name)>`，<br />如果想声明**最少出现一次的元素**，可以使用：`<ELEMENT 元素名 (child-name+)>`，<br />如果想声明**出现0次或多次的元素**，可以使用：`<ELEMENT 元素名 (child-name*)>`，<br/>如果想声明**出现0次或1次的元素**，可以使用：`<ELEMENT 元素名 (child-name?)>`，<br />如果想声明**非../即..的元素**，可以使用：`<ELEMENT 元素名 (a,b,(c|d))>`，<br />如果想声明**混合型的内容**，可以使用：`<ELEMENT 元素名 (#PCDATA|a|b)*>`

<br />

**2.声明属性**

语法：

```dtd
<!ATTLIST 元素名 属性名 属性类型 属性值>
```

如：

```dtd
<!ATTLIST note checked CDATA "checked">
会检测：
<note checked="checked"/>
```

**属性类型**有下：

```
CDATA
(a|b|c...)		此值是枚举列表中的一个值
ID
IDREF			值为另外一个元素的 id
IDREFS			值为其他 id 的列表
NMTOKEN			值为合法的 XML 名称
NMTOKENS		值为合法的 XML 名称的列表
ENTITY			值是一个实体
ENTITIES		值是一个实体列表
NOTATION		此值是符号的名称
xml:			值是一个预定义的 XML 值
```

**属性值**有下：

```
值				属性的默认值
#REQUIRED		 属性值是必须的
#IMPLIED		 属性不是必须的
#FIXED value	属性是固定的
```

**默认的属性值**：

```dtd
DTD:
<!ELEMENT my_element EMPTY>
<!ATTLIST my_element my_attr CDATA "0">

合法的 XML：
<my_element my_attr="100" />		如果没有设置，则默认值是 0
```

**#REQUIRED**

```dtd
<!ATTLIST my_element my_attr attr_type #REQUIRED>
```

实例：

```dtd
DTD:
<!ELEMENT person EMPTY>
<!ATTLIST person name CDATA #REQUIRED>

合法的 XML：
<person name="jack" />

非法的 XML：
<person />
```

**#IMPLIED**

```dtd
<!ATTLIST my_element my_attr attr_type #IMPLIED>
```

实例：

```dtd
DTD:
<!ELEMENT contact EMPTY>
<!ATTLIST contact fax CDATA #IMPLIED>

合法的 XML：
<contact fax="555-123455" />
<contact />
```

**#FIXED**

```dtd
<!ATTLIST my_element my_attr attr_type #FIXED "value">
```

实例：

```dtd
DTD:
<!ELEMENT sender EMPTY>
<!ATTLIST sender company CDATA #FIXED "Apple.Inc">

合法 XML：
<sender company="Apple.Inc" />

非法 XML：
<sender company="Microsoft" />
```

**列举属性值**

```dtd
<!ATTLIST my_element my_attr attr_type (v1|v2|v3..) default-value>
```

实例：

```dtd
DTD:
<!ELEMENT payment EMPTY>
<!ATTLIST payment type (check|cash) "cash">			<!-- 默认采用现金支付 -->

XML:
<payment type="check" />    or
<payment type="cash" />     or
?? <payment />	?? --- Doubt on that...
```

<br />

**3.属性和子元素如何取舍？**

大多数情况下，应该避免使用属性。一般属性具有以下问题：

1. 属性不能包含多个值（子元素可以）
2. 属性不容易扩展（为以后需求的变化）
3. 属性无法描述结构（子元素可以）
4. 属性更难以操纵程序代码
5. 属性值是不容易测试，针对DTD

例外情况：

有时我指定的 ID 应用了元素。这些 ID 应用可在HTML中的很多相同的情况下可作为 NAME 或者 ID 属性来访问 XML 元素，如：

```xml
<messages>
<note id="p501">
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>

<note id="p502">
  <to>Jani</to>
  <from>Tove</from>
  <heading>Re: Reminder</heading>
  <body>I will not!</body>
</note>
</messages>
```

<br />

**4.声明实体**

DTD 中的实体（不是 XML 中的实体哦），相当于一个**变量**，用于定义引用普通文本或特殊字符的快捷方式。

**内部实体声明：**

```dtd
<!ENTITY 实体名称 "实体的值">
```

实例：

```dtd
DTD:
<!ENTITY writer "J.K.Rolling">
<!ENTITY bookname "Harry Potter">

XML 实例：
<book>&writer;&bookname;</book>
```

**外部实体声明：**

```dtd
<!ENTITY 实体名称 SYSTEM "URI/URL">
```

实例：

```dtd
<!ENTITY writer SYSTEM "http://www.logan.com/entities.dtd">
<!ENTITY copyright SYSTEM "http://www.logan.com/entities.dtd">

XML:
<author>&writer;&copyright;</author>
```



<br />

## DTD 怎么和 XML 文件联系起来

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



<br/>

## DTD 的几种不同实例

1. 由 David Moisan 创造。拷贝自：` http://www.davidmoisan.org/`

```dtd
<!DOCTYPE TVSCHEDULE [

<!ELEMENT TVSCHEDULE (CHANNEL+)>
<!ELEMENT CHANNEL (BANNER,DAY+)>
<!ELEMENT BANNER (#PCDATA)>
<!ELEMENT DAY (DATE,(HOLIDAY|PROGRAMSLOT+)+)>
<!ELEMENT HOLIDAY (#PCDATA)>
<!ELEMENT DATE (#PCDATA)>
<!ELEMENT PROGRAMSLOT (TIME,TITLE,DESCRIPTION?)>
<!ELEMENT TIME (#PCDATA)>
<!ELEMENT TITLE (#PCDATA)> 
<!ELEMENT DESCRIPTION (#PCDATA)>

<!ATTLIST TVSCHEDULE NAME CDATA #REQUIRED>
<!ATTLIST CHANNEL CHAN CDATA #REQUIRED>
<!ATTLIST PROGRAMSLOT VTR CDATA #IMPLIED>
<!ATTLIST TITLE RATING CDATA #IMPLIED>
<!ATTLIST TITLE LANGUAGE CDATA #IMPLIED>
]>
```



2. 拷贝自：`http://www.vervet.com/`

```dtd
<!DOCTYPE NEWSPAPER [

<!ELEMENT NEWSPAPER (ARTICLE+)>
<!ELEMENT ARTICLE (HEADLINE,BYLINE,LEAD,BODY,NOTES)>
<!ELEMENT HEADLINE (#PCDATA)>
<!ELEMENT BYLINE (#PCDATA)>
<!ELEMENT LEAD (#PCDATA)>
<!ELEMENT BODY (#PCDATA)>
<!ELEMENT NOTES (#PCDATA)>

<!ATTLIST ARTICLE AUTHOR CDATA #REQUIRED>
<!ATTLIST ARTICLE EDITOR CDATA #IMPLIED>
<!ATTLIST ARTICLE DATE CDATA #IMPLIED>
<!ATTLIST ARTICLE EDITION CDATA #IMPLIED>

<!ENTITY NEWSPAPER "Vervet Logic Times">
<!ENTITY PUBLISHER "Vervet Logic Press">
<!ENTITY COPYRIGHT "Copyright 1998 Vervet Logic Press">

]>
```



3. 拷贝自：` http://www.vervet.com/`

```dtd
<!DOCTYPE CATALOG [

<!ENTITY AUTHOR "John Doe">
<!ENTITY COMPANY "JD Power Tools, Inc.">
<!ENTITY EMAIL "jd@jd-tools.com">

<!ELEMENT CATALOG (PRODUCT+)>

<!ELEMENT PRODUCT
(SPECIFICATIONS+,OPTIONS?,PRICE+,NOTES?)>
<!ATTLIST PRODUCT
NAME CDATA #IMPLIED
CATEGORY (HandTool|Table|Shop-Professional) "HandTool"
PARTNUM CDATA #IMPLIED
PLANT (Pittsburgh|Milwaukee|Chicago) "Chicago"
INVENTORY (InStock|Backordered|Discontinued) "InStock">

<!ELEMENT SPECIFICATIONS (#PCDATA)>
<!ATTLIST SPECIFICATIONS
WEIGHT CDATA #IMPLIED
POWER CDATA #IMPLIED>

<!ELEMENT OPTIONS (#PCDATA)>
<!ATTLIST OPTIONS
FINISH (Metal|Polished|Matte) "Matte"
ADAPTER (Included|Optional|NotApplicable) "Included"
CASE (HardShell|Soft|NotApplicable) "HardShell">

<!ELEMENT PRICE (#PCDATA)>
<!ATTLIST PRICE
MSRP CDATA #IMPLIED
WHOLESALE CDATA #IMPLIED
STREET CDATA #IMPLIED
SHIPPING CDATA #IMPLIED>

<!ELEMENT NOTES (#PCDATA)>

]>
```



