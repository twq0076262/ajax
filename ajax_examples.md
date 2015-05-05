# AJAX 示例

下面列出了一些著名的使用 AJAX 的 Web 应用程序。

## Goole Maps

用户可以用鼠标拖动整个地图，而不是点击某个按钮。

- [http://maps.google.com/](http://www.google.com/maps)

## Google Suggest

用户输入时，Google 会提供搜索建议。我们可以使用方向键来导航结果。

- [http://www.google.com/webhp?complete=1&hl=en](https://www.google.com.hk/webhp?complete=1&hl=en)

## Gmail

Gmail 是一个网络邮箱，它的理念是邮箱可以更直观，高效，实用。

- [http://gmail.com/](http://gmail.com/)

## Yahoo Maps（新项目）

让我们要去哪里变得更容易更有趣。

- [http://maps.yahoo.com/](http://maps.yahoo.com/)

## AJAX 和传统 CGI 程序的差异

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