# Location根据类型分为两种：普通配置和正则匹配

 

## 一、 普通配置

 

普通location根据使用方法又分为两种，格式如下：

1. location  / {

命令序列

}

解释：括号中定义的表示对当前路径及子路径下的所有对象有效。“优先级最低”

用户所有的请求都能被它匹配到。

例子：

location / {  

              root /web; 

相应策略     

}

这说明网页根目录在/web

访问的时候直接http://127.0.0.1或是域名就可以了

用户所有的请求都能被它匹配到

location /bbs {

       root "/web";

相应策略

}

 

这就说明网页根目录是位于  /web/bbs

访问的时候直接http://127.0.0.1/bbs就可以了

当用户访问

http://127.0.0.1/bbs/

或是

http://127.0.0.1/bbs/子路径

的时候才能被上边的路径匹配到。

问题：当用户访问http://127.0.0.1/bbs/a.html时

这两段location 同时存在时如下,那么哪段配置会生效呢？

server {

        listen       80;

        server_name  www.benet.com;

        index index.html;

        location  / {

                root /web;

        }

        location  /bbs {

                root /web;

        }

 

结论就是，

当用户请求的（/bbs）url同时匹配到两段location时，

最大前缀生效（location /bbs生效）

如果没有这段(location /bbs） 第一段生效。

第一段相当于默认策略，因为location / 包含所有的请求，所有的请求都是以  ”/” 开始的

 

 

 

2. location = /路径 {

命令序列

}

解释：括号中定义的表示对当前路径有效，子路径不生效（精确匹配指定的路径不包括子路径）。“它的优先级最高。” 

例子：

location = /prefix {

}

 

也就是用户访问www.benet.com/prefix能被上边的location匹配到，它只匹配"/prefix",

"/"下的子路不匹配。

用户访问www.benet.com/prefix/a 就不能被它匹配到

优先级最高：指的是一旦匹配到此location ，立即生效。其它location无论是否匹配到请求都不生效。

 

例子：

<code>

		location  /prefix/ {

                root /;

        }

		location  = /prefix/  {

               return 500;

        }

 

匹配顺序注解：
## 二、 正则匹配

 

正则匹配也分为两种：

1. location ~ URI {}

~匹配的文件是区分字符 大小写的

2.location ~* URI {} ：

~*匹配的文件是不区分字符大小的

正则匹配是按照正则location编写的顺序生效的，一旦匹配成功即停止匹配到后续的location。

 

例子：

<code>

	   location  ~ /bbs {
	
	                return 400;
	
	   }
	
	   location ~* /bbs {
	
	                return 500;
	
	   }


网页返回错误信息400

 

 

然后将两段配置调换一下位置

<code>

  		location ~* /bbs {

                return 500;

        }

  		location  ~ /bbs {

                return 400;

        }

 

## 三、匹配顺序和生效顺序

 

匹配顺序和生效顺序是两个概念

当配置中出现多个locaton并且普通和正则都有，那么

1、匹配顺序是：

用户请求的URL

（1）先匹配普通location

普通location在匹配是按照编辑顺序匹配

（2）在匹配正则location

正则location在匹配时按照编辑顺序匹配

但是正则和普通locaiton不按照编辑顺序匹配

2、生效顺序

当普通和正则都存在的情况下，遵循以下原则

1.nginx开始按照编辑顺序依次匹配普通location

  （1）如果匹配过程中匹配到了

"location =" ：nginx会立即生效即停止后续的匹配

（2）如果没有"locaiton ="话，

如果匹配到"locatin ^~"。会停止后续的正则匹配

然后最大前缀locaiton生效

最后是location / 生效

 

（3） 如果以上两种location都不存在的话

nginx会匹配所有location后看后续有没有正则locaion

如果后续没有正则locaiton

然后最大前缀locaiton生效

最后是location / 生效

   如果后续还有正则location
一旦匹配成功一条正则locaion，这条会生效，并且会停止后续的正则匹配，还会会覆盖前边的普通location结果
