# 用caddy来搭建服务器

### 1.下载caddy

### 2.找到caddy.exe文件，在里面建一个Caddyfile，这个文件里面主要是用来设置不同端口所要展示的内容，

```
:70 {
	root * D:\Service_Web\caddy\root
	file_server
}

:8090 {
	root * D:/
	file_server browse
}
```

70和8090就为端口值，默认情况下是80。

file_server browse这段的意思是要展示上面root路径下的所有文件。

root后面要跟文件路径。

目前只能在同一局域网下才能访问此网站。

网站地址为本机地址，可以在电脑属性面板中的网络设置中看到，查看网络的IPv4地址。如图：

![image-20231210162140916](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231210162140916.png)

然后在浏览器中就能访问了，但是注意网址后面要加冒号，冒号后面是端口值。

![image-20231210162336660](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231210162336660.png)