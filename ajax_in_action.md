# AJAX 实战

本章提供了一个清晰的 AJAX 操作的具体步骤。

## AJAX 操作步骤

- 触发客户端事件。
- 创建一个 XMLHttpRequest 对象。
- 配置 XMLHttpRequest 对象。
- 使用 XMLHttpRequest 对象创建一个到 Web 服务器的异步请求。
- Web 服务器返回包含 XML 文档的结果。
- XMLHttpRequest 对象调用 callback() 函数处理结果。
- 更新 HTML DOM。

让我们来一个个看下这些步骤。

## 触发客户端事件

- JavaScript 函数作为事件结果调用。
- 比如：JavaScript 函数 _validateUserId()_ 被映射为 id 为 _"userid"_ 的表单输入字段的 _onkeyup_ 事件的事件处理程序。
- `<input type="text" size="20" id="userid" name="id" onkeyup="validateUserId();">`。

## 创建 XMLHttpRequest 对象

```
var ajaxRequest;  // 缓存 XMLHttpRequest 对象
function ajaxFunction(){
	try{
		// Opera 8.0+, Firefox, Safari
		ajaxRequest = new XMLHttpRequest();
	}catch (e){

		// IE 浏览器
		try{
			ajaxRequest = new ActiveXObject("Msxml2.XMLHTTP");
		}catch (e) {

			try{
				ajaxRequest = new ActiveXObject("Microsoft.XMLHTTP");
			}catch (e){
				// 错误处理
				alert("Your browser broke!");
				return false;
			}
		}
	}
}
```

## 配置 XMLHttpRequest 对象

在这个步骤中，我们将会编写一个由客户端事件触发的函数，然后注册一个 processRequest() 回调函数。

```
function validateUserId() {
	ajaxFunction();

	// 这里的 processRequest() 就是回调函数
	ajaxRequest.onreadystatechange = processRequest;

	if (!target) target = document.getElementById("userid");
	var url = "validate?id=" + escape(target.value);

	ajaxRequest.open("GET", url, true);
	ajaxRequest.send(null);
}
```

## 发起到服务器的异步请求

上面的代码是有效的。加粗的代码负责发起到 Web 服务器的请求。这是使用 XMLHttpRequest 对象 _ajaxRequest_ 做到的。

```
function validateUserId() {
	ajaxFunction();

	// 这里的 processRequest() 就是回调函数
	ajaxRequest.onreadystatechange = processRequest;

	__if (!target) target = document.getElementById("userid");__
	__var url = "validate?id=" + escape(target.value);__

	__ajaxRequest.open("GET", url, true);__
	__ajaxRequest.send(null);__
}
```

假设我们在 userid 输入框中输入 _Zara_，那么在上面的请求中，URL 会被设置为 "validate?id=Zara"。

## Web 服务器返回包含 XML 文档的结果

我们可以使用任意语言实现服务端脚本，但是它应该包含如下逻辑。

- 从客户端获取请求。
- 解析来自客户端的输入信息。
- 做必要的处理。
- 将输出信息发送到客户端。

假设我们要编写一个 servlet 程序，这里有一段示例代码。

```
public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
	String targetId = request.getParameter("id");

	if ((targetId != null) && !accounts.containsKey(targetId.trim())) {
		response.setContentType("text/xml");
		response.setHeader("Cache-Control", "no-cache");
		response.getWriter().write("true");
	} else {
		response.setContentType("text/xml");
		response.setHeader("Cache-Control", "no-cache");
		response.getWriter().write("false");
	}
}
```

## 被调用的回调函数 processRequest()

XMLHttpRequest 对象被配置为 _XMLHttpRequest_ 对象的 _readyState_ 状态发生变化时调用 processRequest() 函数。这个函数接受从服务端返回的结果然后做必要的处理。正如下面的示例所示，它基于从 Web 服务器返回的值将消息变量设置为 true 或 false。

```
function processRequest() {
	if (req.readyState == 4) {
		if (req.status == 200) {
			var message = ...;
...
}
```

## 更新 HTML DOM

下面是最后一步，在这一步中我们的 HTML 页面会被更新。它发生在以下方式中：

- JavaScript 使用 DOM API 获取页面任意元素的引用。
- 获取一个元素引用推荐的方式就是调用

```
document.getElementById("userIdMessage"), 
// 这里 "userIdMessage" 就是 HTML 文档中某个元素的 ID 属性
```

- 然后 JavaScript 可能被用来修改元素的属性；修改元素的样式属性，或者添加，移除或修改元素的子元素。这里有一个例子：

```
<script type="text/javascript">
<!--
function setMessageUsingDOM(message) {
	var userMessageElement = document.getElementById("userIdMessage");
	var messageText;

	if (message == "false") {
		userMessageElement.style.color = "red";
		messageText = "Invalid User Id";
	}
	else 
	{
		userMessageElement.style.color = "green";
		messageText = "Valid User Id";
	}

	var messageBody = document.createTextNode(messageText);

	// 如果 messageBody 元素已经创建了，则简单的替换它，否则插入一个新的元素。 
	if (userMessageElement.childNodes[0]) {
		userMessageElement.replaceChild(messageBody, userMessageElement.childNodes[0]);
	} 
	else
	{
		userMessageElement.appendChild(messageBody);
	}
}
-->
</script>
<body>
<div id="userIdMessage"><div>
</body>
```

如果理解了上述 7 步，差不多就完成 AJAX 学习了。下一章，我们会看到更详细的 _XMLHttpRequest_ 对象。