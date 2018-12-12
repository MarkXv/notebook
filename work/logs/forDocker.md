# forDocker
-------------------------

## 1. 私有仓库登陆

	1. copy 仓库的认证文件，对认证文件进行Base64编码  
		echo "{\"192.168.1.200:5000\":{\"ca_base64\":\"$(base64 -w 0 ca.crt)\"}}"
	2. docker login 登陆私服，在root（登陆用户主文件夹中）
		1. .docker/config.json
		2. {"auths":{"host:port":{"auth":"……"}}} 

## 2. 