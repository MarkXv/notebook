## 用JS动态改变表单form里的action值属性的方法

###方法1：

<code>

	<form id="form1" name="form1" method="post" action="../news/index.asp">
	  <table width="100%" height="43" border="0" cellpadding="0" cellspacing="0">
	<tr>
	  <td height="28"><input name="keyword" type="text" style="width:150px" id="keyword"/></td>
	</tr>
	<tr>
	  <td height="28"><select name="Searchtype"  style="width:110px" id="Searchtype" onchange="Searchtype1();">
	<option value="news" selected="selected">新闻中心</option>
	<option value="case">工程案例</option>
	  </select>
	  <input type="submit" name="Submit" value="搜索" /></td>
	</tr>
	  </table>
	  </form>
	  <script language="javascript">
	  function Searchtype1(){
	  var type=document.getElementById("Searchtype").options[document.getElementById("Searchtype").selectedIndex].value;
	  if (type=="news"){document.getElementById("form1").action="../news/index.asp"}
	  else if (type=="case"){document.getElementById("form1").action="../case/index.asp"}
	  }
	  </script>

 

###方法2：

<code>

	<html>
	<head>
	<script language="javascript">
	function check(){
	if(document.form1.a[0].checked==true)
	document.form1.action="1.htm"
	else
	document.form1.action="2.htm"
	}
	</script>
	</head>
	<body>
	<form name="form1" method="post" action="" onSubmit="check();">
	转到页面一<input type="radio" name="a">
	转到页面二<input type="radio" name="a">
	<input name="" type="submit" value="提交">
	</form>
	</body>
	</html>  