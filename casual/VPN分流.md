###VPN分流

	https://github.com/jimmyxu/chnroutes
	
	在终端中执行python chnroutes.py -p mac，这将生成ip-up和ip-down两个文件；
	
	将这两个文件移入/etc/ppp/；
	
	设置这两个文件为可执行权限 chmod +x /etc/ppp/*
	
	重新连接VPN，观察测试。
    
---
	
	分别访问www.123cha.com和who.is，如果显示你的ip不同，那么就成功了。前者显示的是你国内的ip，后者显示的是你VPN主机的ip
