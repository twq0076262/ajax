# AJAX 快速指南

## 什么是 AJAX？

- AJAX 表示异步 JavaScript 和 XML。AJAX 是一种借助 XML，HTML，CSS 和 JavaScript 的帮助创建更好，更快以及更多交互的 Web 应用程序的新技术。

- AJAX 使用 XHTML 呈现内容，CSS 处理表现，以及使用文档对象模型和 JavaScript 显示动态内容。

- 传统的 Web 应用程序使用同步请求的方式从服务器传输信息。这就意味着我们要填写表单，点击提交然后定向到服务器提供的带有新信息的新页面。

- 使用 AJAX 时，当我们点击提交，JavaScript 会发起一个到服务器的请求，解析返回结果，然后更新当前屏幕显示。从纯粹意义上讲，用户甚至不知道给服务器传送了什么信息。

- XML 通常用作从服务器接收的数据格式，尽管它可以是任意格式，包括文本。

- AJAX 是一种独立于 Web 服务器软件的浏览器技术。

- 用户可以继续使用该应用程序，而从服务器请求信息的客户端程序运行在后台。

- 直观和自然的用户交互。不再需要点击，鼠标移动就是一个充分的事件触发器。

- 基于数据驱动的，而非页面驱动。

### 富互联网应用程序技术

AJAX 是目前为止最成功的富互联网应用程序（RIA）技术。它具有巨大的生产力，还有几个新兴的工具库和框架。但是同时，由于还有浏览器不兼容 AJAX 以及需要 JavaScript 支持，这导致它很难维护和调试。

### AJAX 基于开放标准

AJAX 基于以下开放标准

- 使用 HTML 和层叠样式表（CSS）基于浏览器呈现。
- 数据存储在 XML 格式中并且需要从服务器获取。
- 在浏览器中使用 XMLHttpRequest 在幕后从服务器获取数据。
- 使用 JavaScript 实现一切。

## AJAX 技术

AJAX 不能独立使用。适用于结合其他技术来创建交互式网页。

### JavaScript

- 松散类型的脚本语言。
- 页面中触发事件时调用某个 JavaScript 函数。
- 整个 AJAX 操作的胶带。

### DOM

- 访问和操作结构化文档的 API。
- 呈现 XML 和 HTML 文档的结构。

### CSS

- 允许我们从内容中清晰的分离显示样式，还允许通过 JavaScript 程序改变它。

### XMLHttpRequest

- 与服务器进行异步交互的 JavaScript 对象。

## AJAX 示例

下面列出了一些著名的使用 AJAX 的 Web 应用程序。

### Goole Maps

用户可以用鼠标拖动整个地图，而不是点击某个按钮。

- [http://maps.google.com/](http://www.google.com/maps)

### Google Suggest

用户输入时，Google 会提供搜索建议。我们可以使用方向键来导航结果。

- [http://www.google.com/webhp?complete=1&hl=en](https://www.google.com.hk/webhp?complete=1&hl=en)

### Gmail

Gmail 是一个网络邮箱，它的理念是邮箱可以更直观，高效，实用。

- [http://gmail.com/](http://gmail.com/)

### Yahoo Maps（新项目）

让我们要去哪里变得更容易更有趣。

- [http://maps.yahoo.com/](http://maps.yahoo.com/)

### AJAX 和传统 CGI 程序的差异

试一试下面两个例子便可以感受到差异。尝试 AJAX 示例时可以感受到它是连贯的，我们可以很快得到响应；但是当我们尝试 CGI 示例时，我们不得不等待响应，并且页面也会刷新。

__AJAX示例__

```html
<form name="form1" action="" onsubmit="return ajax_call()">
	<input type="text" name="num1" id="num1"></input> *
	<input type="text" name="num2" id="num2"></input> = 
	<input type="text" name="result" id="result"></input>
	<input type="submit" name="semajax" value="AJAX"></input>
</form>
<script type="text/javascript">
var xmlhttp=false;

function ajax_call() {
	try{
		// Opera 8.0+, Firefox, Safari
		xmlhttp = new XMLHttpRequest();
	} catch (e){
		// Internet Explorer Browsers
		try{
			xmlhttp = new ActiveXObject("Msxml2.XMLHTTP");
		} catch (e) {
			try{
				xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
			} catch (e){
				// 错误处理
				alert("Your browser broke!");
				return false;
			}
		}
	}
	xmlhttp.open("GET", '/cgi-bin/ajaxWorks.cgi?num1=' + document.getElementById('num1').value + '&num2=' + document.getElementById('num2').value , true);
	xmlhttp.onreadystatechange= function() {
		if (xmlhttp.readyState==4) {
			document.getElementById('result').value = xmlhttp.responseText;
		}
	}
	xmlhttp.send(null)
	return false;
}
</script>
```

__标准示例__

```html
<form name="form1" action="/cgi-bin/ajaxCGI.cgi">
	<input type="text" name="num1" id="num1" value=0></input> *
	<input type="text" name="num2" id="num2" value=0></input> =
	<input type="text" name="result" id="result" value=0></input>
	<input type="submit" name="semajax" value="Standard"></input>
</form>
```

__注意：__ 在 AJAX 数据库部分我们提供了一个更复杂的示例。

## AJAX 之浏览器支持

所有可用的浏览器都支持 AJAX。下面是一个支持 AJAX 的主流浏览器列表：

- Mozilla FireFox 1.0 及以上版本
- Netscape 7.1 及以上版本
- Apple Safari 1.2 及以上版本
- 微软 IE 5 及以上版本
- Konqueror
- Opera 7.6 及以上版本

当我们编写下一个应用程序时，要考虑那些不支持 AJAX 的浏览器。

__注意：__当我们说某个浏览器不支持 AJAX 时，只是意味着该浏览器不支持使用 JavaScript 创建 XMLHttpRequest 对象。

### 编写浏览器特定的代码

让代码与浏览器兼容最简单的方式便是在 JavaScript 中使用 _`try..catch`_ 块。

```html
<html>
<body>
	<script language="javascript" type="text/javascript">
	<!-- 
	//浏览器特定的代码
	function ajaxFunction(){
		var ajaxRequest;  // 缓存XHR对象便于AJAX使用

		try{
			// Opera 8.0+, Firefox, Safari 
			ajaxRequest = new XMLHttpRequest();
		}catch (e){

			// Internet Explorer Browsers
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
	//-->
	</script>
	<form name='myForm'>
	Name: <input type='text' name='username' /> <br />
	Time: <input type='text' name='time' />
	</form>
</body>
</html>
```

在上面的 JavaScript 代码中，我们三次尝试获得 XMLHttpRequest 对象。下面是第一次尝试：

- _ajaxRequest = new XMLHttpRequest();_

这适用于 Opera 8.0+，FireFox 和 Safari 浏览器。如果这个尝试失败，接下来我们两次尝试针对 IE 浏览器创建正确的对象：

- _ajaxRequest = new ActiveXObject("Msxml2.XMLHTTP");_
- _ajaxRequest = new ActiveXObject("Microsoft.XMLHTTP");_

如果它不工作，那表示我们可能在使用一个不支持 _XMLHttpRequest_ 的非常过时的浏览器，这也意味着它不支持 AJAX。

但最有可能的是，我们的 _ajaxRequest_ 变量现在被设置为浏览器使用的 XMLHttpRequest 标准，然后我们就可以开始向服务器发送数据了。分步进行的 AJAX 工作流会在单独的章节中讨论。

## AJAX 实战

这个部分提供了一个清晰的 AJAX 操作的具体步骤。

### AJAX 操作步骤

- 触发客户端事件。
- 创建一个 XMLHttpRequest 对象。
- 配置 XMLHttpRequest 对象。
- 使用 XMLHttpRequest 对象创建一个到 Web 服务器的异步请求。
- Web 服务器返回包含 XML 文档的结果。
- XMLHttpRequest 对象调用 callback() 函数处理结果。
- 更新 HTML DOM。

让我们来一个个看下这些步骤。

### 触发客户端事件

- JavaScript 函数作为事件结果调用。
- 比如：JavaScript 函数 _validateUserId()_ 被映射为 id 为 _"userid"_ 的表单输入字段的 _onkeyup_ 事件的事件处理程序。
- `<input type="text" size="20" id="userid" name="id" onkeyup="validateUserId();">`。

### 创建 XMLHttpRequest 对象

```javascript
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

### 配置 XMLHttpRequest 对象

在这个步骤中，我们将会编写一个由客户端事件触发的函数，然后注册一个 processRequest() 回调函数。

```javascript
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

### 发起到服务器的异步请求

上面的代码是有效的。加粗的代码负责发起到 Web 服务器的请求。这是使用 XMLHttpRequest 对象 _ajaxRequest_ 做到的。

```javascript
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

### Web 服务器返回包含 XML 文档的结果

我们可以使用任意语言实现服务端脚本，但是它应该包含如下逻辑。

- 从客户端获取请求。
- 解析来自客户端的输入信息。
- 做必要的处理。
- 将输出信息发送到客户端。

假设我们要编写一个 servlet 程序，这里有一段示例代码。

```java
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

### 被调用的回调函数 processRequest()

XMLHttpRequest 对象被配置为 _XMLHttpRequest_ 对象的 _readyState_ 状态发生变化时调用 processRequest() 函数。这个函数接受从服务端返回的结果然后做必要的处理。正如下面的示例所示，它基于从 Web 服务器返回的值将消息变量设置为 true 或 false。

```javascript
function processRequest() {
	if (req.readyState == 4) {
		if (req.status == 200) {
			var message = ...;
...
}
```

### 更新 HTML DOM

下面是最后一步，在这一步中我们的 HTML 页面会被更新。它发生在以下方式中：

- JavaScript 使用 DOM API 获取页面任意元素的引用。
- 获取一个元素引用推荐的方式就是调用

```javascript
document.getElementById("userIdMessage"), 
// 这里 "userIdMessage" 就是 HTML 文档中某个元素的 ID 属性
```

- 然后 JavaScript 可能被用来修改元素的属性；修改元素的样式属性，或者添加，移除或修改元素的子元素。这里有一个例子：

```html
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

如果理解了上述 7 步，差不多就完成 AJAX 学习了。在单独的章节中，我们可以看到更详细的 _XMLHttpRequest_ 对象。

## AJAX 之 XMLHttpRequest

XMLHttpRequest 对象是 AJAX 的关键。它从 2000 年 7 月发布的 IE 5.5 开始可用，但是直到 2005 年 AJAX 和 Web 2.0 变得流行起来它都没有完全被发觉。

XMLHttpRequest (XHR) 是一个可以用 JavaScript，JScript，VBScript 和其他 Web 浏览器脚本语言传输和操作 XML 数据，以及使用 HTTP 从 Web 服务器上在网页客户端和服务端之间建立一个独立连接通道的 API。

调用 XMLHttpRequest 返回的数据通常都由后端数据库提供。除了 XML 之外，XMLHttpRequest 还可以用来获取其他格式的数据，例如 JSON 或者是纯文本。

我们已经见过好几个讲述如何创建 XMLHttpRequest 对象的例子了。

下面列出的是一些我们必须熟悉的方法和属性。

### XMLHttpRequest 方法

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

### XMLHttpRequest 属性

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

## AJAX 之数据库操作

为了说明使用 AJAX 从数据库中访问信息有多么容易，我们要构建一个 MySQL 查询，然后把结果显示在 "ajax.html" 中。但是在开始之前，我们先来做一些基础工作。使用下面的命令创建一个数据表。

__注意：__ 这里我们假设你有足够的权限执行以下 MySQL 操作。

```sql
CREATE TABLE 'ajax_example' (
   'name' varchar(50) NOT NULL,
   'age' int(11) NOT NULL,
   'sex' varchar(1) NOT NULL,
   'wpm' int(11) NOT NULL,
   PRIMARY KEY  ('name')
)
```

然后使用下面的 SQL 语句把下列数据存到这个表中：

```sql
INSERT INTO 'ajax_example' VALUES ('Jerry', 120, 'm', 20);
INSERT INTO 'ajax_example' VALUES ('Regis', 75, 'm', 44);
INSERT INTO 'ajax_example' VALUES ('Frank', 45, 'm', 87);
INSERT INTO 'ajax_example' VALUES ('Jill', 22, 'f', 72);
INSERT INTO 'ajax_example' VALUES ('Tracy', 27, 'f', 0);
INSERT INTO 'ajax_example' VALUES ('Julie', 35, 'f', 90);
```

### 客户端 HTML 文件

现在我们来建立客户端的 HTML 文件，也就是 ajax.html，它的代码如下所示：

```html
<html>
<body>
<script language="javascript" type="text/javascript">
<!-- 
// 浏览器支持代码
function ajaxFunction(){
	var ajaxRequest;  // 缓存 XMLHttpRequest 对象
	try{

		// Opera 8.0+, Firefox, Safari
		ajaxRequest = new XMLHttpRequest();
	}catch (e){
	  
		// Internet Explorer Browsers
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

	// 创建一个接受服务器发送的数据的函数，它还会更新同一页面的 div 部分。
	ajaxRequest.onreadystatechange = function(){

		if(ajaxRequest.readyState == 4){
			var ajaxDisplay = document.getElementById('ajaxDiv');
			ajaxDisplay.innerHTML = ajaxRequest.responseText;
		}
	}

	// 然后获取用户输入值并传递给服务器脚本
	var age = document.getElementById('age').value;
	var wpm = document.getElementById('wpm').value;
	var sex = document.getElementById('sex').value;
	var queryString = "?age=" + age ;

	queryString +=  "&wpm=" + wpm + "&sex=" + sex;
	ajaxRequest.open("GET", "ajax-example.php" + queryString, true);
	ajaxRequest.send(null); 
}
//-->
</script>

<form name='myForm'>

	Max Age: <input type='text' id='age' /> <br />
	Max WPM: <input type='text' id='wpm' /> <br />
	Sex: 
	<select id='sex'>
	  <option value="m">m</option>
	  <option value="f">f</option>
	</select>
	<input type='button' onclick='ajaxFunction()' value='Query MySQL'/>
   
</form>
<div id='ajaxDiv'>结果会显示在这里。</div>
</body>
</html>
```

__注意：__ 在查询中传递变量的方法取决于 HTML 标准以及我们使用哪种形式。

```
URL?variable1=value1;&variable2=value2;
```

上面的代码显示如下所示：

__注意：__ 这还是一个模拟的屏幕显示，它还不能工作。

![query-mysql-1](images/query-my-sql-1.png)

获取到条目之后结果会显示在表单的下面。

__注意：__ 这里是一个模拟的屏幕显示。

### 服务端 PHP 文件

客户端脚本已经准备就绪。现在，我们来编写服务端脚本，它会从数据库中提取 age，wpm 和 sex，然后把它们发送回客户端。请把下面的代码放到 "ajax-example.php" 中。

```php
<?php
$dbhost = "localhost";
$dbuser = "dbusername";
$dbpass = "dbpassword";
$dbname = "dbname";
	
// 连接 MySQL 服务器
mysql_connect($dbhost, $dbuser, $dbpass);
	
// 选择数据库
mysql_select_db($dbname) or die(mysql_error());
	
// 从查询字符串中检索数据（字段）
$age = $_GET['age'];
$sex = $_GET['sex'];
$wpm = $_GET['wpm'];
	
// 转移用户输入便于防止 SQL 注入
$age = mysql_real_escape_string($age);
$sex = mysql_real_escape_string($sex);
$wpm = mysql_real_escape_string($wpm);
	
// 构建查询
$query = "SELECT * FROM ajax_example WHERE sex = '$sex'";

if(is_numeric($age))
	$query .= " AND age <= $age";

if(is_numeric($wpm))
	$query .= " AND wpm <= $wpm";
	
// 执行查询
$qry_result = mysql_query($query) or die(mysql_error());

// 构建结果字符串
$display_string = "<table>";
$display_string .= "<tr>";
$display_string .= "<th>Name</th>";
$display_string .= "<th>Age</th>";
$display_string .= "<th>Sex</th>";
$display_string .= "<th>WPM</th>";
$display_string .= "</tr>";

// 针对返回的每个 person 条目在表格中插入一个新行
while($row = mysql_fetch_array($qry_result)){
	$display_string .= "<tr>";
	$display_string .= "<td>$row[name]</td>";
	$display_string .= "<td>$row[age]</td>";
	$display_string .= "<td>$row[sex]</td>";
	$display_string .= "<td>$row[wpm]</td>";
	$display_string .= "</tr>";
}

echo "Query: " . $query . "<br />";
$display_string .= "</table>";

echo $display_string;
?>
```

现在可以尝试在 _Max Age_ 或者其他输入框中输入一个有效的值（比如 120），然后点击 Query MySQL 按钮。

![query-mysql-1](images/query-my-sql-1.png)

<p style="color: red">获取到条目之后结果将会显示在这个部分</p>

如果你成功完成这一课，那么你就知道如何串联使用 MySQL，PHP，HTML 和 JavaScript 编写 AJAX 应用程序了。

## AJAX 之安全

### 服务器端 AJAX 安全

- 基于 AJAX 的 Web 应用程序使用与常规 Web 应用程序相同的服务器端安全方案。

- 我们可以在 web.xml 文件（声明式）或者程序中（程序化）指定身份认证，授权信息以及要保护的数据。

- 基于 AJAX 的 Web 应用程序也受和常规 Web 应用程序一样安全威胁。

### 客户端 AJAX 安全

- JavaScript 代码对于用户/黑客是可见的。黑客可以使用 JavaScript 代码推断服务器端的弱点。

- JavaScript 代码是从服务下载的，然后在客户端执行（"eval"），可以通过恶意代码来危害客户端。

- 下载的 JavaScript 代码受安全沙箱模型约束，但是我们可以对签名的 JavaScript 有所放宽。

## AJAX 相关问题

AJAX 的发展非常迅猛，这也是它有很多问题的原因。我们希望随着时间的流逝，这些问题会被解决，并且 AJAX 也能成为 Web 应用程序的理想选择。下面列出了一些 AJAX 目前面临的一些问题。

### 增加复杂性

- 服务端开发人员需要理解客户端 HTML 页面需要的显示逻辑和服务端逻辑。

- 页面开发人员必须掌握 JavaScript 技术。

### 基于 AJAX 的应用程序可能难以调试，测试和维护

- JavaScript 难以测试，自动化测试更难。

- JavaScript 模块化特点薄弱。

- 缺少设计模式以及最佳实践指引。

### 工具箱/框架还不成熟

- 大部分都处在 beta 阶段。

### XMLHttpRequest 尚未标准化

- 未来版本的 IE 将会解决这个问题。

### 旧浏览器不支持 XMLHttpRequest

- Iframe 会有所帮助。

### JavaScript 技术依赖和不兼容性

- 必须为应用程序启用这个功能。
- 仍然存在一些浏览器不兼容。

### JavaScript 代码对黑客可见

- 设计不良的 JavaScript 代码可能导致安全问题。