# 拷贝.sql文件到一个文件夹下，并进行打包

<code>

	tar cf test.tar 'cp -R $(`find ./ -name '*.c'`) .\test'

	tar  cf test.tar 'find ./ -name "*.sql" | xargs cp -t test' 
	
	mkdir test && cp $(find ./ -name "*.c") test && tar cvf test.tar test



### 几个注意的点：
 
<code>

1. 多命令顺序执行  
多命令执行符 格式 作用:
	<code>
	
		; (分号) 命令1;命令2 多命令顺序执行，命令之间没有联系
		不管前面的命令执行是否正确，后面的命令都会执行
		&& (逻辑与) 命令1&&命令2 当命令1正确执行，命令2才会执行
		当命令1不正确执行，命令2不执行
		|| (逻辑或) 命令1||命令2 当命令1不正确执行，命令2才会执行
		当命令1正确执行，命令2不执行
		        命令 && echo yes || echo no  ///命令正确执行打印yes否则打印no


2. dd 命令（万能复制,可以复制磁盘或文件）

	<code>

		  格式： dd if=输入文件  of=输出文件 bs=字节数 count=个数
		         if=输入文件 设备源文件或源设备
		of=输出文件 目标文件或目标设备
		bs=字节数 一次输入或输出多少个字节，可以把字节看做一个数据块
		count=个数 指定输入或输出多少个数据块
		
		date;dd if=/dev/zero of=/root/testfiles bs=1k count=100000 ;date

3. 管道符

	<code>
	
	   格式：命令1  |  命令2  ///命令1的正确输出作为命令2的输入

	   netstat -an | grep "ESTABLISHED"



4. grep命令

	<code>
	
		grep [选项] 搜索内容 文件名
		-i 忽略大小写
		-n 输出行号
		-v 反向查找
		--color=auto  搜索出的关键字用颜色显示
		     grep  "root"  /etc/passwd 