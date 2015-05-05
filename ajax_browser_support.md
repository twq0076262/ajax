# AJAX 之浏览器支持

所有可用的浏览器都支持 AJAX。下面是一个支持 AJAX 的主流浏览器列表：

- Mozilla FireFox 1.0 及以上版本
- Netscape 7.1 及以上版本
- Apple Safari 1.2 及以上版本
- 微软 IE 5 及以上版本
- Konqueror
- Opera 7.6 及以上版本

当我们编写下一个应用程序时，要考虑那些不支持 AJAX 的浏览器。

__注意：__当我们说某个浏览器不支持 AJAX 时，只是意味着该浏览器不支持使用 JavaScript 创建 XMLHttpRequest 对象。

## 编写浏览器特定的代码

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

但最有可能的是，我们的 _ajaxRequest_ 变量现在被设置为浏览器使用的 XMLHttpRequest 标准，然后我们就可以开始向服务器发送数据了。分步进行的 AJAX 工作流会在下一章讨论。