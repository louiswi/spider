#####`urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)`

打开一个名为`url`的URL(Uniform Resource Locator:统一资源定位符)，`url`可以是一个字符串或者一个`Request`对象。  
`data`必须是指定要发送给服务器的额外bytes object(一串由0到255之间的数字组成的序列叫做bytes对象)，或者`None`(若不需要这样的数据的话)。`data`还可以是可迭代对象，这种情况下，必须在headers中明确指出Content-Length(在entity-header field中，它指出entity-body大小，[w3](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)参考)的值。目前，仅有HTTP请求使用`data`；如果`data`参数被提供，HTTP请求将会使用POST方法而不是GET方法。  
`data`应该是采用标准`application/x-www-form-urlencoded`形式的buffer。 `urllib.parse.urlencode()`函数可接受映射对象或者2-元组序列，且会返回这种格式的字符串。它应该在作为`data`参数使用前被编码为bytes。在`Content-Type`头(内容类型实体头域指出媒体类型，[w3](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)参考)中的charset parameter可用于指定编码方式。若charset parameter(字符集参数)不以Content-Type header方式发送，且假定服务器遵循推荐的HTTP 1.1，那么数据会采用ISO-8859-1编码方式进行编码。明智的做法是使用具有`urllib.request.Request`的`Content-Type` header编码的charset parameter。(It is advisable to use charset parameter with encoding used in `Content-Type` header with the `urllib.request.Request`。)  
`urllib.request`模块使用HTTP/1.1，且其HTTP请求包括`Connection:close`头。  
可选的`timeout`参数在进行类似尝试连接的阻塞操作(block operations)时候，指定以秒为单位(若不指定，则会使用全局默认超时设置)。实际上，这仅适用于HTTP,HTTPS及FTP连接。  
如果`context`被指定，它必须是一个描述不同SSL选项的[`ssl.SSLContext`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext)实例。请看[`HTTPSConnection`](https://docs.python.org/3/library/http.client.html#http.client.HTTPSConnection)获取更多信息。  
可选的`cafile`和`capath`参数指定了HTTPS请求中可信赖的CA证书集。`cafile`应指向包含一系列CA证书的单个文件，而`capath`应指向hashed certificated files的工作目录。在[`ssl.SSLContext.load_verify_locations()`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext.load_verify_locations)中可找到更多相关信息。  
`cadefault`参数被忽略。  
对于http与https url而言，该函数会返回一个遵守[`HTTPResponse Objects`](https://docs.python.org/3/library/http.client.html#httpresponse-objects)方法的http.client.HTTPResponse`对象。  
对于ftp、文件、数据URL以及可通过传统`urllib.request.URLopener`和`urllib.request.FancyURLopener`类处理的明确请求而言，该函数会返回可作为[`context manager`](https://docs.python.org/3/glossary.html#term-context-manager)工作且具有这些方法的`urllib.response.addinfourl`对象：  
`geturl()`--返回源检索URL，常用于确定是否遵从重定向  
`info()`--以[`email.message_from_string()`](https://docs.python.org/3/library/email.parser.html#email.message_from_string)实例形式返回页面meta-infomation，例如headers(请参阅[`Quick Reference to HTTP Headers`](http://www.cs.tut.fi/~jkorpela/http.html))  
`getcode()`--返回HTTP响应状态码。  
出错时候会引发[`urllib.error.URLError`](https://docs.python.org/3/library/urllib.error.html#urllib.error.URLError)错误。  
注意：  
如果没有程序处理请求的话(尽管默认安装了全局的`urllib.request.OpenerDirector`使用`urllib.request.UnknownHandler`来确保这永远不会发生)，会返回`None`。  
此外，若检测到代理设置(比如，当设置了类似于http_proxy的`*_proxy`环境变量时)，由于`urllib.request.ProxyHandle`已默认安装，会确保请求是通过代理进行处理。  
Python2.6以及之前的版本已经停用了传统的`urllib.urlopen`函数；`urllib.request.urlopen()`对应旧的`urllib2.urlopen`。通过把字典参数传递给`urllib.urlopen`可进行代理操作，通过使用`urllib.request.ProxyHandler`对象也可以获得代理处理。  
Changed in version 3.2: cafile and capath were added.  
Changed in version 3.2: HTTPS virtual hosts are now supported if possible (that is, if ssl.HAS_SNI is true).  
New in version 3.2: data can be an iterable object.  
Changed in version 3.3: cadefault was added.  
Changed in version 3.4.3: context was added.  
