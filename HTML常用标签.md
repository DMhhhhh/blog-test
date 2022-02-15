# \<a\>: The Anchor element

The **\<a\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
(or *anchor* element),
with [its [href]{.underline} attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-href),
creates a hyperlink to web pages, files, email addresses, locations in
the same page, or anything else a URL can address.

Content within each \<a\> **should** indicate the link\'s destination.
If the href attribute is present, pressing the enter key while focused
on the \<a\> element will activate it.

**HTML \<a\> 元素**（或称锚元素）可以通过[它的 [href]{.underline} 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)创建通向其他网页、文件、同一页面内的位置、电子邮件地址或任何其他
URL
的超链接。\<a\> 中的内容**应该**应该指明链接的意图。如果存在[ [href]{.underline} 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)，当 \<a\> 元素聚焦时按下回车键就会激活它。

## [Attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attributes) [属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#%E5%B1%9E%E6%80%A7)

### [href](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-href)

The URL that the hyperlink points to. Links are not restricted to
HTTP-based URLs --- they can use any URL scheme supported by browsers:

-   Sections of a page with fragment URLs

-   Pieces of media files with media fragments

-   Telephone numbers with tel: URLs

-   Email addresses with mailto: URLs

-   While web browsers may not support other URL schemes, web sites can
    > with [[registerProtocolHandler()]{.underline}](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/registerProtocolHandler)

包含超链接指向的 URL 或 URL 片段。

URL
片段是哈希标记（#）前面的名称，哈希标记指定当前文档中的内部目标位置（HTML
元素的 ID）。URL 不限于基于
Web（HTTP）的文档，也可以使用浏览器支持的任何协议。例如，在大多数浏览器中正常工作的[[file:]{.underline}](https://en.wikipedia.org/wiki/File_URI_scheme)、ftp:和mailto：。

#### Web address 网址

#### Path 路径

##### [A quick primer on URLs and paths](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#a_quick_primer_on_urls_and_paths) 统一资源定位符(URL)与路径(path)快速入门

A URL, or Uniform Resource Locator is a string of text that defines
where something is located on the Web. For example, Mozilla\'s English
homepage is located at https://www.mozilla.org/en-US/.

URLs use paths to find files. Paths specify where the file you\'re
interested in is located in the filesystem. Let\'s look at an example of
a directory structure, see
the [creating-hyperlinks](https://github.com/mdn/learning-area/tree/master/html/introduction-to-html/creating-hyperlinks) directory.

统一资源定位符（英文：**U**niform **R**esource **L**ocator，简写：URL）是一个定义了在网络上的位置的一个文本字符串。例如
Mozilla 的中文主页定位在 https://www.mozilla.org/zh-CN/.

URL使用路径查找文件。路径指定文件系统中您感兴趣的文件所在的位置。看一下一个简单的目录结构的例子（源码可查看 [创建超链接（creating-hyperlinks](https://github.com/roy-tian/learning-area/tree/master/html/introduction-to-html/creating-hyperlinks)）。）

![A simple directory structure. The parent directory is called
creating-hyperlinks and contains two files called index.html and
contacts.html, and two directories called projects and pdfs, which
contain an index.html and a project-brief.pdf file,
respectively](media/image1.png){width="5.768055555555556in"
height="3.582638888888889in"}

**Same directory**: If you wanted to include a hyperlink
inside index.html (the top level index.html) pointing to contacts.html,
you would specify the filename that you want to link to, because it\'s
in the same directory as the current file. The URL you would use
is contacts.html

**指向当前目录：**如果index.html（目录顶层的index.html）想要包含一个超链接指向contacts.html，你只需要指定想要链接的文件名，因为它与当前文件是在同一个目录的.
所以你应该使用的URL是contacts.html

**Moving down into subdirectories**: If you wanted to include a
hyperlink inside index.html (the top level index.html) pointing
to projects/index.html, you would need to go down into
the projects directory before indicating the file you want to link to.
This is done by specifying the directory\'s name, then a forward slash,
then the name of the file. The URL you would use is projects/index.html

**指向子目录：**如果index.html （目录顶层index.html）想要包含一个超链接指向 projects/index.html，您需要先进入projects/项目目录，然后指明要链接到的文件index.html。 通过指定目录的名称，然后是正斜杠，然后是文件的名称。因此您要使用的URL是projects/index.html

**Moving back up into parent directories**: If you wanted to include a
hyperlink inside projects/index.html pointing to pdfs/project-brief.pdf,
you\'d have to go up a directory level, then back down into
the pdf directory. To go up a directory, use two dots --- .. --- so the
URL you would use is ../pdfs/project-brief.pdf

**指向上级目录： **如果你想在projects/index.html中包含一个指向pdfs/project-brief.pdf的超链接，你必须先返回上级目录，然后再回到pdf目录。"返回上一个目录级"使用两个英文点号表示 --- .. ---
所以你应该使用的URL是 ../pdfs/project-brief.pdf

#### 伪协议

**JavaScrip伪协议**

javascript:; 什么都不会发生

**Email addresses** **邮箱地址**

mailto:

**Telephone numbers 电话号码**

tel:

#### [Document fragments](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#document_fragments) [文档片段](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#%E6%96%87%E6%A1%A3%E7%89%87%E6%AE%B5)

It\'s possible to link to a specific part of an HTML document, known as
a **document fragment**, rather than just to the top of the document. To
do this you first have to assign
an [[id]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-id) attribute
to the element you want to link to. It normally makes sense to link to a
specific heading, so this would look something like the following:

超链接除了可以链接到文档外，也可以链接到HTML文档的特定部分（被称为**文档片段**）。要做到这一点，你必须首先给要链接到的元素分配一个[id](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes#attr-id)属性。例如，如果你想链接到一个特定的标题，可以这样做：

\<h2 id=\"Mailing_address\"\>Mailing address\</h2\>

Then to link to that specific id, you\'d include it at the end of the
URL, preceded by a hash/pound symbol (#), for example:

然后链接到那个特定的id，您可以在URL的结尾使用一个井号指向它，例如：

\<p\>Want to write us a letter? Use our \<a
href=\"contacts.html#Mailing_address\"\>mailing address\</a\>.\</p\>

### [target](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-target)

Where to display the linked URL, as the name for a *browsing context* (a
tab, window,
or [[\<iframe\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)).
The following keywords have special meanings for where to load the URL:

该属性指定在何处显示链接的资源。
取值为标签（tab），窗口（window），或框架（iframe）等浏览上下文的名称或其他关键词。以下关键字具有特殊的意义:

-   \_self: the current browsing context. (Default)

> 当前页面加载，即当前的响应到同一HTML5浏览上下文。此值是默认的，如果没有指定属性的话。

-   \_blank: usually a new tab, but users can configure browsers to open
    > a new window instead.

> 新窗口打开，即到一个新的未命名的HTML5浏览器上下文

-   \_parent: the parent browsing context of the current one. If no
    > parent, behaves as \_self.

> 加载响应到当前的HTML5浏览上下文的父浏览上下文。如果没有parent框架或者浏览上下文，此选项的行为方式与 \_self 相同。

-   \_top: the topmost browsing context (the \"highest\" context that's
    > an ancestor of the current one). If no ancestors, behaves
    > as \_self.

> HTML5中：加载响应进入顶层浏览上下文（即，浏览上下文，它是当前的一个的祖先，并且没有parent）。如果没有parent框架或者浏览上下文，此选项的行为方式相同_self

**Note:** Setting target=\"\_blank\" on \<a\> elements implicitly
provides the same rel behavior as
setting [[rel=\"noopener\"]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/noopener) which
does not set window.opener. See [[browser
compatibility]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#browser_compatibility) for
support status.

**注意：**在 \<a\> 元素上使用 target=\"\_blank\" 隐式提供了与使用 [[rel=\"noopener\"]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/noopener) 相同的 rel 行为，即不会设置 window.opener。

# \<img\>: The Image Embed element

The **\<img\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
embeds an image into the document.

**HTML \<img\> 元素**将一份图像嵌入文档。

## 作用

发出get请求，展示一张图片

## [Attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attributes) [属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#%E5%B1%9E%E6%80%A7)

### [alt](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img#attr-alt)

Defines an alternative text description of the image.

定义了图像的备用文本描述。

**Note:** Browsers do not always display images. There are a number of
situations in which a browser might not display images, such as:
**注意：**浏览器并非总是会显示图像。比如：

-   Non-visual browsers (such as those used by people with visual
    impairments) 非可视化浏览器（Non-visual
    browsers）（比如有视力障碍的人使用的音频浏览器）

-   The user chooses not to display images (saving bandwidth, privacy
    reasons)
    用户选择不显示图像（比如为了节省带宽，或出于隐私等考虑不加载包括图片在内的第三方资源文件）

```{=html}
<!-- -->
```
-   The image is invalid or an [unsupported
    type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#supported_image_formats)图像文件无效，或是使用了[不支持的格式](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img#supported_image_formats)

In these cases, the browser may replace the image with the text in the
element\'s alt attribute. For these reasons and others, provide a useful
value for alt whenever possible.

在这些情况下，浏览器很可能会将图像替换为图像所属 \<img\> 元素的 alt 属性所提供的文本。基于上面罗列的原因，以及更多尚未列出的原因，建议尽可能地通过 alt 属性提供一些有用的信息。

### [height](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-height)

The intrinsic height of the image, in pixels. Must be an integer without
a unit.
图像的高度，在 [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 中的单位是
CSS 像素

### [width](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-width)

The intrinsic width of the image in pixels. Must be an integer without a
unit.
图像的宽度，在 [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 中单位是
CSS 像素

### [src](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-src)

The image [URL](https://developer.mozilla.org/en-US/docs/Glossary/URL).
Mandatory for the \<img\> element.
On [browsers](https://developer.mozilla.org/en-US/docs/Glossary/Browser) supporting srcset, src is
treated like a candidate image with a pixel density descriptor 1x,
unless an image with this pixel density descriptor is already defined
in srcset, or unless srcset contains w descriptors.

图像的 [URL](https://developer.mozilla.org/zh-CN/docs/Glossary/URL)，这个属性对 \<img\> 元素来说是必需的。在支持 srcset 的浏览器中，src 被当做拥有一个像素密度的描述符 1x 的候选图像处理，除非一个图像拥有这个像素密度描述符已经被在 srcset 或者 srcset 包含 w 描述符中定义了。

## 事件

### onload/onerror 

监听图片是否加载成功

## 响应式

max-width:100%

# \<table\>: The Table element

The **\<table\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
represents tabular data --- that is, information presented in a
two-dimensional table comprised of rows and columns of cells containing
data.

**HTML**的 **table **元素表示表格数据 --- 即通过二维数据表表示的信息。

## 相关标签

### \<table\>

The content of every table is enclosed by these two tags
: [**\<table\>\</table\>**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)

每一个表格的内容都包含在这两个标签中
: [**\<table\>\</table\>**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)

### \<thead\>

-   The \<thead\> element must wrap the part of the table that is the
    header --- this is usually the first row containing the column
    headings, but this is not necessarily always the case. If you are
    using [[\<col\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/col)/[[\<colgroup\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/colgroup) element,
    the table header should come just below those.

> \<thead\> 需要嵌套在 table
> 元素中，放置在头部的位置，因为它通常代表第一行，第一行中往往都是每列的标题，但是不是每种情况都是这样的。如果你使用了 [[\<col\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/col)/[[\<colgroup\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/colgroup) 元素，那么 \<thead\>元素就需要放在它们的下面。

### \<tbody\>

The \<tbody\> element needs to wrap the other parts of the table content
that aren\'t in the table header or footer. It will appear below the
table header or sometimes footer, depending on how you decided to
structure it.

 \<tbody\> 需要嵌套在 table
元素中，放置在 \<thead\>的下面或者是 \<tfoot\> 的下面，这取决于你如何设计你的结构。(\<tfoot\>放在\<thead\>下面也可以生效.)

### \<tfoot\>

The \<tfoot\> element needs to wrap the part of the table that is the
footer --- this might be a final row with items in the previous rows
summed, for example. You can include the table footer right at the
bottom of the table as you\'d expect, or just below the table header
(the browser will still render it at the bottom of the table).

\<tfoot\> 需要嵌套在 table 元素中，放置在底部
(页脚)的位置，一般是最后一行，往往是对前面所有行的总结，比如，你可以按照预想的方式将\<tfoot\>放在表格的底部，或者就放在 \<thead\> 的下面。(浏览器仍将它呈现在表格的底部)

### \<td\> The Table Data Cell element

The smallest container inside a table is a table cell, which is created
by
a [**\<td\>**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) element
(\'td\' stands for \'table data\'). 

在表格中，最小的内容容器是单元格,
是通过 [**\<td\>**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) 元素创建的
(\'td\' 代表 \'table data\')

### \<tr\> The Table Row element

The **\<tr\>**[HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
defines a row of cells in a table. The row\'s cells can then be
established using a mix
of [[\<td\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) (data
cell)
and [[\<th\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th) (header
cell) elements.

**HTML \<tr\> 元素**定义表格中的行。同一行可同时出现[[\<td\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/td) 和[[\<th\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th) 元素.

### \<th\> The Table Header element

The **\<th\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
defines a cell as header of a group of table cells. The exact nature of
this group is defined by
the [**scope**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th#attr-scope) and [**headers**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th#attr-headers) attributes.

**HTML \<th\> 元素**定义表格内的表头单元格。这部分特征是由 [**scope**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th#attr-scope) and [**headers**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th#attr-headers) 属性准确定义的。

## 相关样式

### table-layout

The **table-layout** CSS property sets the algorithm used to lay
out [\<table\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) cells,
rows, and columns.

**table-layout **CSS属性定义了用于布局表格*单元格*，*行*和*列*的算法。

#### [Values](https://developer.mozilla.org/en-US/docs/Web/CSS/table-layout#values)

**auto**

By default, most browsers use an automatic table layout algorithm. The
widths of the table and its cells are adjusted to fit the
content.大多数浏览器采用自动表格布局算法对表格布局。表格及单元格的宽度取决于其包含的内容。

**fixed**

Table and column widths are set by the widths of table and col elements
or by the width of the first row of cells. Cells in subsequent rows do
not affect column widths.
表格和列的宽度通过表格的宽度来设置，某一列的宽度仅由该列首行的单元格决定。在当前列中，该单元格所在行之后的行并不会影响整个列宽。

### border-collapse

The **border-collapse** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property
sets whether cells inside
a [\<table\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) have
shared or separate borders.

**border-collapse** [CSS](https://developer.mozilla.org/zh-CN/docs/Web/CSS) 属性是用来决定表格的边框是分开的还是合并的。在分隔模式下，相邻的单元格都拥有独立的边框。在合并模式下，相邻单元格共享边框。

#### [Values](https://developer.mozilla.org/en-US/docs/Web/CSS/border-collapse#values)

**collapse**

Adjacent cells have shared borders (the collapsed-border table rendering
model).相邻的单元格共用同一条边框（采用 collapsed-border
表格渲染模型）。

**separate**

Adjacent cells have distinct borders (the separated-border table
rendering model). 默认值。每个单元格拥有独立的边框（采用
separated-border 表格渲染模型）。

### border-spacing

The **border-spacing** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property
sets the distance between the borders of
adjacent [\<table\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) cells.
This property applies only
when [border-collapse](https://developer.mozilla.org/en-US/docs/Web/CSS/border-collapse) is separate.

border-spacing 属性指定相邻单元格边框之间的距离（只适用于 [边框分离模式](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-collapse) ）。相当于
HTML
中的 cellspacing 属性，但是第二个可选的值可以用来设置不同于水平间距的垂直间距。

border-spacing:0
