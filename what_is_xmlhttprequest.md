# AJAX 之 XMLHttpRequest

XMLHttpRequest 对象是 AJAX 的关键。它从 2000 年 7 月发布的 IE 5.5 开始可用，但是直到 2005 年 AJAX 和 Web 2.0 变得流行起来它都没有完全被发觉。

XMLHttpRequest (XHR) 是一个可以用 JavaScript，JScript，VBScript 和其他 Web 浏览器脚本语言传输和操作 XML 数据，以及使用 HTTP 从 Web 服务器上在网页客户端和服务端之间建立一个独立连接通道的 API。

调用 XMLHttpRequest 返回的数据通常都由后端数据库提供。除了 XML 之外，XMLHttpRequest 还可以用来获取其他格式的数据，例如 JSON 或者是纯文本。

我们已经见过好几个讲述如何创建 XMLHttpRequest 对象的例子了。

下面列出的是一些我们必须熟悉的方法和属性。

## XMLHttpRequest 方法

- __abort()__

取消当前请求。

- __getAllResponseHeaders()__

返回完整的 HTTP 头字符串。

- __open( method, URL )__
- __open( method, URL, async )__
- __open( method, URL, async, userName )__
- __open( method, URL, async, userName, password )__

指定请求的方法，URL 以及其他可选属性。

方法参数可以是 "GET"，"POST" 或者 "HEAD" 中的一个值。也可能是其他 HTTP 方法，比如 "PUT" 和 "DELETE"（主要用于 REST 应用程序中）。

"async" 参数指定该请求是否应该异步处理。"true" 意味着脚本处理发生在 send() 方法之后而无需等待响应，而 "false" 意味着继续脚本处理之前脚本要等待响应。

- __send( content )__

发送请求。

- __setRequestHeader( label, value )__

给要发送的 HTTP 头添加一个标签/值对。

## XMLHttpRequest 属性

- __onreadystatechange__

一个用于事件的事件处理程序，每个状态变化时都会触发。

- __readyState__

readyState 属性定义了 XMLHttpRequest 对象的当前状态。

下面的表格提供了一个 readyState 属性可能值的列表：

<table>
	<thead>
		<tr>
			<th>状态</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td>请求还未初始化。</td>
		</tr>
		<tr>
			<td>1</td>
			<td>请求已经建立。</td>
		</tr>
		<tr>
			<td>2</td>
			<td>请求已经发送。</td>
		</tr>
		<tr>
			<td>3</td>
			<td>请求正在处理。</td>
		</tr>
		<tr>
			<td>4</td>
			<td>请求已经完成。</td>
		</tr>
	</tbody>
</table>

__readyState = 0__ 在 XMLHttpRequest 对象创建之后，但是在我们调用 open() 方法之前。

__readyState = 1__ 在调用 open() 方法之后，但是在调用 send() 之前。

__readyState = 2__ 在我们调用 send() 之后。

__readyState = 3__ 在浏览器建立与服务器的通信之后，但是在服务器完成响应之前。

__readyState = 4__ 在请求完成以及响应数据已经完全从服务器接受之后。

- __responseText__

返回响应字符串。

- __responseXML__

返回响应的 XML 数据。这个属性返回一个 XML 文档对象，我们可以使用 W3C DOM 节点树方法和属性检查并解析它。

- __status__

返回状态数字（比如 404 表示 "Not Found" 或者 200 表示 "OK"）。

- __statusText__

返回状态字符串（比如 "Not Found" 或者 "OK"）。