# REST简介

[转载来源](http://www.cnblogs.com/loveis715/p/4669091.html)

一说到REST，我想大家的第一反应就是“啊，就是那种前后台通信方式。”但是在要求详细讲述它所提出的各个约束，以及如何开始搭建REST服务时，却很少有人能够清晰地说出它到底是什么，需要遵守什么样的准则。

在您将看到的这一篇文章中，我们将对REST，尤其是基于HTTP的REST服务进行详细地介绍。通过这些文章，您不仅可以了解到什么是REST，更能清晰地了解到您在编写REST服务时所需要遵守的各个守则，设计RESTful API时需要考虑的各种因素以及实现过程中可能遇到的问题等内容。

### REST示例

我想，很多读者可能并不太清楚REST到底是一个什么概念。那么，首先让我们来看一个简单的基于HTTP的REST服务示例。

假设用户正在访问一个电子商务网站www.egoods.com。该网站对其所销售的各个物品进行了详细分类。当用户登录该网站进行购物时，他首先需要在该网站上选择其所需要寻找物品的分类，进而列出属于该分类的各个物品。

![商品分类](https://cl.ly/0e1u0U3b3l1V/Image%202017-05-13%20at%2005.12.20.png)

当然，虽然从业务逻辑的角度来说这个流程非常简单，但实际上浏览器向后台发送了多个请求：页面逻辑在页面加载时将首先得到所有的商品分类，并将这些分类显示在了页面中。在用户选择了一个分类的时候，页面逻辑将发送一个请求得到该分类的详细信息，并发送另外一个请求来得到该分类的商品列表：

![http过程](https://cl.ly/2S3p2A0d432t/Image%202017-05-13%20at%2005.17.26.png)

在通过浏览器的调试功能查看这些请求的时候，我们可以看到其首先向`www.egoods.com/api/categories`发送一个GET请求，以取得所有的商品分类：

```
GET /api/categories
Host: www.egoods.com
Authorization: Basic xxxxxxxxxxxxxxxxxxx
Accept: application/json
```

而服务端将返回所有的类别：

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
 
[
   {
      "label" : "食品",
      "url" : "/api/categories/1"
   }, {
      "label" : "服装",
      "url" : "/api/categories/2"
   }
   ...
   {
      "label" : "电子设备",
      "url" : "/api/categories/25"
   }
]
```

该响应返回了一个用JSON表示的数组。该数组中的每个元素包含了两部分信息：用户能够读懂的表示分类名称的label以及相应分类所对应的URL。其中Label所记录的分类名称将在页面中显示给用户。而在用户根据label所标示的分类名选择了一个分类的时候，页面逻辑会取得该分类所对应的URL并向该URL 发送请求，以得到该分类的详细信息。例如在用户点击了“食品”这个分类的时候，浏览器将会向服务器发送如下的请求：

```
GET /api/categories/1
Host: www.egoods.com
Authorization: Basic xxxxxxxxxxxxxxxxxxx
Accept: application/json
```

这一次，页面逻辑根据用户对分类的选择“食品”来得到了其所对应的URL，并向该URL发送了一个GET请求。而该请求所得到的响应则为：

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
 
{
   "url" : "/api/categories/1",
   "label" : "Food",
   "items_url" : "/api/items?category=1",
   "brands" : [
         {
            "label" : "友臣",
            "brand_key" : "32073",
            "url" : "/api/brands/32073"
         }, {
            "label" : "乐事",
            "brand_key" : "56632",
            "url" : "/api/brands/56632"
         }
         ...
   ],
   "hot_searches" : …
}
```

该响应略为复杂。首先，响应中的URL标示了“食品”分类所对应的URL。而label属性则和前面一样，用来在页面上显示分类的名称。一个较为特殊的属性则是items_url。其用来标示获取属于食品分类的各个产品的URL。而属性brands则用来列出在“食品”分类中的著名品牌，例如友臣，乐事等。这些品牌被组织为一个对象数组，而数组中的每个对象都拥有label，url等属性。在这些属性的帮助下，页面可以列出这些著名品牌的名称，并允许用户通过点击跳转到这些品牌所对应的页面上。除了这些属性之外，Food分类还包含了其它一系列属性，如表示当前其它用户正在搜索的hot_searches属性等，这里就不再赘述。

该响应有一个问题，那就是符合用户筛选条件的各个产品并没有包含在该响应中。这是因为页面所列出的各个产品是根据用户所设置的筛选条件，即其选择的品牌以及搜索关键字而变化的。因此，页面逻辑会根据属性items_url以及用户所设定的搜索条件组合成为目标URL，再次发送请求到后台，以请求需要在页面中展现的各个物品。

例如用户在只想浏览属于乐事品牌的食品时，其可以钩选乐事这个品牌，那么此时的URL将由食物分类的items_url以及表示按照品牌进行筛选的URL参数共同组成：

```
1 GET /api/items?category=1&brand_key=56632
2 Host: www.egoods.com
3 Authorization: Basic xxxxxxxxxxxxxxxxxxx
4 Accept: application/json
```

现在让我们来总结一下上面所展示的基于HTTP的REST系统的整个运行流程。在开始的时候，我们拿到了所有分类的列表。列表中的各个条目不仅仅包含了用户可以看到的分类名称等信息，更拥有一个额外的URL属性。在用户选择该列表中的一项时，页面逻辑将会向对应的URL发送一个请求，以获得该项目的详细信息。在这个详细信息中，一些内容又包含了一些其它的URL，从而使得页面逻辑又能通过该URL属性发送请求。

您也许会说，哎，这不和我们现有系统的运行流程一样的嘛。是的。在上面所举出的例子中，我们也更偏重地描述了REST系统所需要具有的HATEOAS（Hypermedia As The Engine Of Application State）特性。正是由于这个特性已经在大家所创建的系统里面广泛地使用了，因此我更希望从熟悉的地方入手，而不是开始就非常教条地说REST一定要这样，一定要那样，徒增了学习的难度。

反过来说，上面所展示的REST服务并不具有典型性。在充分了解了REST后，您会发现，REST在系统设计上的视角将不再把流程放在了最优先的位置。

而在后面的章节中，我们则会逐渐展开，详细地介绍如何创建一个纯正的基于HTTP的REST服务。



### REST的定义

OK，现在让我们来看看REST的定义。Wikipedia是这样描述它的：

> Representational State Transfer (REST) is a software architecture style consisting of guidelines and best practices for creating scalable web services. REST is a coordinated set of constraints applied to the design of components in a distributed hypermedia system that can lead to a more performant and maintainable architecture.


# 未完待续