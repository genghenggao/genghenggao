# Ajax_Demo1

## 1、jquery 使用ajax异步验证用户名密码

参考：<https://www.tianmaying.com/snippet/755>

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Ajax验证用户登录信息</title>
<style type="text/css">
   body{
	   font-size:9pt;
   }
   .title{
	   background-color:#CFC;
	   font-weight:bold;	   	   
   }
</style>
<script src="jquery/jquery-1.9.1.js"></script>
<script type="text/javascript" language="javascript">
   $(document).ready(function(){
        $("#btnsubmit").click(function(){             //为按钮关联单击事件处理代码
			 checklogin();                              //调用自定义函数进行登录验证
		});
      });
         function checklogin() {                       //定义一个登录验证的函数  
            if ($("#txtusername").val() == "") {       //检测用户名是否为空
                $("#msguser").html("用户名不能为空！"); //显示提示消息
                $("#txtusername").focus();
				return false;
            }else
			{
		    	$("#msguser").html("");	
				}
            if ($("#txtpassword").val() == "") {      //检测用户密码是否为空  
                $("#msgpwd").html("密码框不能为空！"); //显示提示消息
                $("#txtpassword").focus();
				return false;				
            }else{
		    	$("#msgpwd").html("");					
			}
            $.ajax({             //如果用户名和密码都不为空，则异步的发送Ajax验证请求，
                type: "POST",
                url: "8_5_validuser.php",
                data: "username=" + $("#txtusername").val().toString()
				    + "&password=" + $("#txtpassword").val().toString(),
                success: function (data) {           //如果异步调用成功，则判断返回的状态值
                    if (data == "1") {                //如果返回状态值为1，则表示登录成功
                       	$("#msg").html("登录成功！");
         				return true;
                    }
                    else {                             //如果返回的状态值为2,则登录失败
						$("#msg").html("请确认您输入的用户名或密码输入是否正确！");
                        $("#txtusername").focus();
        				return false;							
                    }
                }
            })
        }
</script>
</head>

<body>
<table>
    <tr>
        <td colspan=2 class="title">登录界面</td>  
    </tr>
    <tr>
        <td>用户名:</td>
        <td><input type=text name=username id="txtusername" size=30><span id="msguser"></span></td>
    </tr>
    <tr>
        <td>密码:</td>
        <td><input type=password  name=password  id="txtpassword"  size=30><span id="msgpwd"></span></td>
    </tr>
    <tr>
        <td colspan=2><input type=button value=登录 id="btnsubmit"><span id="msg"></span></td>
    </tr>
</table>

</body>
</html>
```

