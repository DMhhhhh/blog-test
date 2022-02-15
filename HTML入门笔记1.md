# 全局属性 Global attributes

**全局属性**是所有HTML元素共有的属性;
它们可以用于所有元素，即使属性可能对某些元素不起作用。

我们可以在所有的HTML元素上指定全局属性，甚至是在标准里没有指定的元素。这意味着任何非标准元素仍必须能够应用这些属性，即使使用这些元素意味着文档不再是html5兼容的。例如，虽然\<foo\>不是一个有效的HTML元素，但是html5兼容的浏览器隐藏了标记为\<foo
hidden\>\...\<foo\>的内容。

**Global attributes** are attributes common to all HTML elements; they
can be used on all elements, though they may have no effect on some
elements.

Global attributes may be specified on all [HTML
elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element), *even
those not specified in the standard*. That means that any non-standard
elements must still permit these attributes, even though using those
elements means that the document is no longer HTML5-compliant. For
example, HTML5-compliant browsers hide content marked as \<foo
hidden\>\...\</foo\>, even though \<foo\> is not a valid HTML element.

[**class**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes#attr-class)

一个以空格分隔的元素的类名（classes ）列表，它允许 CSS 和 Javascript
通过类选择器 ([[class
selectors]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Class_selectors)) 或DOM方法( [document.getElementsByClassName]{.underline})来选择和访问特定的元素。

A space-separated list of the classes of the element. Classes allows CSS
and JavaScript to select and access specific elements via the [class
selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors) or
functions like the
method [[Document.getElementsByClassName()]{.underline}](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName).

[**contenteditable**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-contenteditable)

An enumerated attribute indicating if the element should be editable by
the user. If so, the browser modifies its widget to allow editing. The
attribute must take one of the following values:

-   true or the *empty string*, which indicates that the element must be
    editable;

-   false, which indicates that the element must not be editable.

一个枚举属性（enumerated
attribute），表示元素是否可被用户编辑。 如果可以，浏览器会调整元素的部件（widget）以允许编辑。

-   true 或者空字符串，表明元素是可被编辑的；

-   false，表明元素不能被编辑。

[**hidden**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-hidden)

A Boolean attribute indicates that the element is not yet, or is no
longer, *relevant*. For example, it can be used to hide elements of the
page that can\'t be used until the login process has been completed. The
browser won\'t render such elements. This attribute must not be used to
hide content that could legitimately be shown.

布尔属性表示该元素尚未或不再*相关*。例如，它可用于隐藏在登录过程完成之前无法使用的页面元素。浏览器不会呈现此类元素。不得使用此属性隐藏可合法显示的内容

[**id**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-id)

Defines a unique identifier (ID) which must be unique in the whole
document. Its purpose is to identify the element when linking (using a
fragment identifier), scripting, or styling (with CSS).

定义唯一标识符（ID），该标识符在整个文档中必须是唯一的。
其目的是在链接（使用片段标识符），脚本或样式（使用CSS）时标识元素。

[**style**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-style)

Contains [[CSS]{.underline}](https://developer.mozilla.org/en-US/docs/Web/CSS) styling
declarations to be applied to the element. Note that it is recommended
for styles to be defined in a separate file or files. This attribute and
the [[\<style\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style) element
have mainly the purpose of allowing for quick styling, for example for
testing purposes.

含要应用于元素的[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)样式声明。
请注意，建议在单独的文件中定义样式。
该属性和[[\<style\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/style)元素主要用于快速样式化，例如用于测试目的。

[**tabindex**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-tabindex)

An integer attribute indicating if the element can take input focus
(is *focusable*), if it should participate to sequential keyboard
navigation, and if so, at what position. It can take several values:

-   a *negative value* means that the element should be focusable, but
    should not be reachable via sequential keyboard navigation;

-   0 means that the element should be focusable and reachable via
    sequential keyboard navigation, but its relative order is defined by
    the platform convention;

-   a *positive value* means that the element should be focusable and
    reachable via sequential keyboard navigation; the order in which the
    elements are focused is the increasing value of
    the [**[tabindex]{.underline}**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-tabindex).
    If several elements share the same tabindex, their relative order
    follows their relative positions in the document.

整数属性，指示元素是否可以获取输入焦点（可聚焦），是否应该参与顺序键盘导航，如果是，则表示哪个位置。它可能需要几个值：

-   负值表示该元素应该是可聚焦的，但不应通过顺序键盘导航到达;

-   0 表示元素应通过顺序键盘导航可聚焦和可到达，但其相对顺序由平台约定定义;

-   正值意味着元素应该可以通过顺序键盘导航进行聚焦和访问;元素聚焦的顺序是[**[tabindex]{.underline}**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes#attr-tabindex)的增加值。如果多个元素共享相同的tabindex，则它们的相对顺序遵循它们在文档中的相对位置。

[**title**](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-title)

Contains a text representing advisory information related to the element
it belongs to. Such information can typically, but not necessarily, be
presented to the user as a tooltip.

包含表示与其所属元素相关信息的文本。
这些信息通常可以作为提示呈现给用户,但不是必须的。

# 常用的内容标签

# \<q\>: The Inline Quotation element

The **\<q\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
indicates that the enclosed text is a short inline quotation. Most
modern browsers implement this by surrounding the text in quotation
marks. This element is intended for short quotations that don\'t require
paragraph breaks; for long quotations use
the [\<blockquote\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote) element.

*HTML引用标签* (**\<q\>**)表示一个封闭的并且是短的行内引用的文本.
这个标签是用来引用短的文本，所以请不要引入换行符;
对于长的文本的引用请使用 [[\<blockquote\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/blockquote) 替代.

# \<blockquote\>: The Block Quotation element

The **\<blockquote\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
indicates that the enclosed text is an extended quotation. Usually, this
is rendered visually by indentation
(see [Notes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote#usage_notes) for
how to change it). A URL for the source of the quotation may be given
using the **cite** attribute, while a text representation of the source
can be given using
the [\<cite\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/cite) element.

**HTML \<blockquote\> 元素**（或者 HTML
块级引用元素），代表其中的文字是引用内容。通常在渲染时，这部分的内容会有一定的缩进（[**注**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/blockquote#Notes) 中说明了如何更改）。若引文来源于网络，则可以将原内容的出处
URL 地址设置到 cite
特性上，若要以文本的形式告知读者引文的出处时，可以通过 [[\<cite\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/cite) 元素。

[[\<code\>]{.underline}](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/code)

For marking up generic pieces of computer code.

用于标记计算机通用代码。

[[\<pre\>]{.underline}](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/pre)

For retaining whitespace (generally code blocks) --- if you use
indentation or excess whitespace inside your text, browsers will ignore
it and you will not see it on your rendered page. If you wrap the text
in \<pre\>\</pre\> tags however, your whitespace will be rendered
identically to how you see it in your text editor.

用于保留空白字符（通常用于代码块）------如果您在文本中使用缩进或多余的空白，浏览器将忽略它，您将不会在呈现的页面上看到它。但是，如果您将文本包含在\<pre\>\</pre\>标签中，那么空白将会以与你在文本编辑器中看到的相同的方式渲染出来。

# \<em\>: The Emphasis element

The **\<em\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
marks text that has stress emphasis. The \<em\> element can be nested,
with each level of nesting indicating a greater degree of emphasis.

**HTML 着重元素** (**\<em\>**)
标记出需要用户着重阅读的内容， \<em\> 元素是可以嵌套的，嵌套层次越深，则其包含的内容被认定为越需要着重阅读。

# \<strong\>: The Strong Importance element

The **\<strong\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
indicates that its contents have strong importance, seriousness, or
urgency. Browsers typically render the contents in bold type.

Strong 元素 (\<strong\>)表示文本十分重要，一般用粗体显示。

# \<br\>: The Line Break element

The **\<br\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
produces a line break in text (carriage-return). It is useful for
writing a poem or an address, where the division of lines is
significant.

**HTML \<br\>
元素**在文本中生成一个换行（回车）符号。此元素在写诗和地址时很有用，这些地方的换行都非常重要。

# \<hr\>: The Thematic Break (Horizontal Rule) element

The **\<hr\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
represents a thematic break between paragraph-level elements: for
example, a change of scene in a story, or a shift of topic within a
section.

Historically, this has been presented as a horizontal rule or line.
While it may still be displayed as a horizontal rule in visual browsers,
this element is now defined in semantic terms, rather than
presentational terms, so if you wish to draw a horizontal line, you
should do so using appropriate CSS.

**HTML \<hr\> 元素**表示段落级元素之间的主题转换（例如，一个故事中的场景的改变，或一个章节的主题的改变）。

在HTML的早期版本中，它是一个水平线。现在它仍能在可视化浏览器中表现为水平线，但目前被定义为语义上的，而不是表现层面上。所以如果想画一条横线，请使用适当的css样式来修饰。

# \<a\>: The Anchor element

The **\<a\>** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element
(or *anchor* element),
with [its href attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-href),
creates a hyperlink to web pages, files, email addresses, locations in
the same page, or anything else a URL can address.

Content within each \<a\> **should** indicate the link\'s destination.
If the href attribute is present, pressing the enter key while focused
on the \<a\> element will activate it.

**HTML \<a\> 元素**（或称锚元素）可以通过[它的 [href]{.underline} 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)创建通向其他网页、文件、同一页面内的位置、电子邮件地址或任何其他
URL
的超链接。\<a\> 中的内容**应该**应该指明链接的意图。如果存在[ [href]{.underline} 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)，当 \<a\> 元素聚焦时按下回车键就会激活它。
