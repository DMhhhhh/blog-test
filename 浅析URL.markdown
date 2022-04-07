# 浅析URL

## URL 包含哪几部分，每部分分别有什么作用

![完整网址](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)

### Scheme

![方案](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-protocol@x2_update.png)

The first part of the URL is the scheme, which indicates the
**protocol** that the browser must use to request the resource (a
protocol is a set method for exchanging or transferring data around a
computer network). Usually for websites the protocol is HTTPS or HTTP
(its unsecured version). Addressing web pages requires one of these two,
but browsers also know how to handle other schemes such as mailto: (to
open a mail client)
URL的第一部分是scheme，它表示浏览器必须用来请求资源的**协议**（协议是一套在计算机网络上交换或传输数据的方法）。通常对于网站，协议是
HTTPS 或
HTTP（其不安全的版本）。Web需要它们二者之一，但浏览器也知道如何处理其他协议，比如mailto:（打开邮件客户端）

### Authority

![权威](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-authority.png)

Next follows the authority, which is separated from the scheme by the
character pattern `://`. If present the authority includes both the
**domain** (e.g. www.example.com) and the **port** (80), separated by a
colon:

接下来是authority，它通过字符`://`与scheme分开。如果存在，则authority包括**域名**（例如www.example.com）和**端口**（80），用冒号分隔：

-   The domain indicates which Web server is being requested. Usually
    this is a domain name, but an IP address may also be used (but this
    is rare as it is much less convenient).域名表示正在请求哪个 Web
    服务器。通常这是一个域名，但也可以使用[IP
    地址](https://developer.mozilla.org/en-US/docs/Glossary/IP_Address)（但这种情况很少见，因为它不太方便）。

-   The port indicates the technical \"gate\" used to access the
    resources on the web server. It is usually omitted if the web server
    uses the standard ports of the HTTP protocol (80 for HTTP and 443
    for HTTPS) to grant access to its resources. Otherwise it is
    mandatory.端口表示用于访问 Web 服务器上的资源的技术"门"。如果 Web
    服务器使用 HTTP 协议的标准端口（HTTP 为 80，HTTPS 为
    443）来授予对其资源的访问权限，则通常省略它。否则是强制性的。

### Path to resource

![Path to the file](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-path@x2.png)

`/path/to/myfile.html` is the **path** to the resource on the Web server.
In the early days of the Web, a path like this represented a physical
file location on the Web server. Nowadays, it is mostly an abstraction
handled by Web servers without any physical reality.

是网络服务器上资源的**路径**。在Web的早期阶段，像这样的路径表示Web服务器上的物理文件位置。如今，它主要是由没有任何物理现实的Web服务器处理的抽象概念。

### Parameters

![Parameters](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-parameters@x2.png)

`?key1=value1&key2=value2` are extra **parameters** provided to the Web
server. Those parameters are a list of key/value pairs separated with
the & symbol. The Web server can use those parameters to do extra stuff
before returning the resource. Each Web server has its own rules
regarding parameters, and the only reliable way to know if a specific
Web server is handling parameters is by asking the Web server owner.

是提供给网络服务器的额外**参数**。
这些参数是用 & 符号分隔的键/值对列表。在返回资源之前，Web服务器可以使用这些参数来执行额外的操作。每个Web服务器都有自己关于参数的规则，唯一可靠的方式来知道特定Web服务器是否处理参数是通过询问Web服务器所有者

### Anchor

![Anchor](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-anchor@x2.png)

`#SomewhereInTheDocument` is an anchor to another part of the resource
itself. An anchor represents a sort of \"bookmark\" inside the resource,
giving the browser the directions to show the content located at that
\"bookmarked\" spot. On an HTML document, for example, the browser will
scroll to the point where the anchor is defined; on a video or audio
document, the browser will try to go to the time the anchor represents.
It is worth noting that **the part after the #, also known as
the fragment identifier, is never sent to the server with the request.**

是资源其他部分的锚点.
锚点表示资源中的一种"书签"，给浏览器显示位于该"加书签"位置的内容的方向。例如，在HTML文档上，浏览器将滚动到定义锚点的位置;在视频或音频文档上，浏览器将尝试转到锚代表的时间。值得注意的是，**＃后面的部分（也称为片段标识符）从来没有发送到请求的服务器。**

## DNS 的作用是什么，nslookup 命令怎么用

### How does a DNS request work? DNS请求如何工作？

> As we already saw, when you want to display a webpage in your browser
> it\'s easier to type a domain name than an IP address. Let\'s take a
> look at the process:
> 正如我们所看到的，当你想在浏览器中展示一个网页的时候，输入域名比输入IP简单多了。让我们看一下这个过程：

1.  Type mozilla.org in your browser\'s location
    bar.在你的浏览器地址栏输入mozilla.org。

2.  Your browser asks your computer if it already recognizes the IP
    address identified by this domain name (using a local DNS cache). If
    it does, the name is translated to the IP address and the browser
    negotiates contents with the web server. End of
    story.您的浏览器询问您的计算机是否已经识别此域名所确定的IP地址（使用本地DNS缓存）。
    如果是的话，这个域名被转换为IP地址，然后浏览器与网络服务器交换内容。结束。

3.  If your computer does not know which IP is behind
    the mozilla.org name, it goes on to ask a DNS server, whose job is
    precisely to tell your computer which IP address matches each
    registered domain name.如果你的电脑不知道 mozilla.org 域名背后的IP,
    它会询问一个DNS服务器，这个服务器的工作就是告诉你的电脑已经注册的域名所匹配的IP。

4.  Now that the computer knows the requested IP address, your browser
    can negotiate contents with the web
    server.现在电脑知道了要请求的IP地址，你的浏览器能够与网络服务器交换内容。

 ![Explanation of the steps needed to obtain the result to a DNS
 request](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_domain_name/2014-10-dns-request2.png)
### nslookup命令

```
nslookup 域名//得到dns服务器返回域名对应ip地址
```

## IP 的作用是什么，ping 命令怎么用

### IP

ip主要约定两件事

1.  如何定位一台设备

2.  如何封装数据报文，以及跟其他设备交流

### ping命令使用

```
ping 域名//得到从dns服务器返回域名对应的ip地址
```

## 域名是什么，分别哪几类域名

### Summary概述

Domain names are a key part of the Internet infrastructure. They provide
a human-readable address for any web server available on the Internet.
Any Internet-connected computer can be reached through a
public IP address. Computers can handle such addresses easily, but
people have a hard time finding out who\'s running the server or what
service the website offers. IP addresses are hard to remember and might
change over time. To solve all those problems we use human-readable
addresses called domain names.

域名是互联网基础架构的关键部分。它们为互联网上任何可用的网页服务器提供了方便人类理解的地址。任何连上互联网的电脑都可以通过一个公共IP地址访问到，计算机可以很容易地处理这些IP地址,
但是对一个人来说很难找出谁在操控这些服务器以及这些网站提供什么服务。IP
地址很难记忆而且可能会随着时间的推移发生改变
。为了解决这些问题，我们使用方便记忆的地址，称作域名。

### Structure of domain names 域名的结构

![Anatomy of the MDN domain name](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_domain_name/structure.png)

A domain name has a simple structure made of several parts (it might be
one part only, two, three\...), separated by dots and read from right to
left. Each of those parts provides specific information about the whole
domain name.

一个域名是由几部分（有可能只是一部分，也许是两部分，三部分\...）组成的简单结构，它被点分隔，它需要从右到左阅读。域名的每一部分都提供着特定信息。

#### TLD (Top-Level Domain顶级域名).

TLDs tell users the general purpose of the service behind the domain
name. 顶级域名可以告诉用户域名所提供的服务类型。

Label标签(or component或者说是组件)

The labels are what follow the TLD. 标签都是紧随着TLD的。

#### Secondary Level Domain 二级域名

The label located right before the TLD is also called a *Secondary Level
Domain* (SLD).

A domain name can have many labels (or components). It is not mandatory
nor necessary to have 3 labels to form a domain name. For instance,
www.inf.ed.ac.uk is a valid domain name. For any domain you control
(e.g. [mozilla.org](https://mozilla.org/)), you can create
\"subdomains\" with different content located at each,
like [developer.mozilla.org](https://developer.mozilla.org/)

刚好位于TLD前面的标签也被称为二级域名 (SLD)。一个域名可以有多个标签（或者说是组件），没有强制规定必须要3个标签来构成域名。例如，www.inf.ed.ac.uk
是一个正确的域名。当拥有了"上级"部分(例如 [mozilla.org](https://mozilla.org/))，你还可以创建另外的域名
(有时被称为 \"子域名\")
(例如 [developer.mozilla.org](https://developer.mozilla.org/)).
