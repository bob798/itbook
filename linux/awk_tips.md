# AWK Tips
[linux awk 内置函数详细介绍（实例）](http://www.cnblogs.com/chengmo/archive/2010/10/08/1845913.html)

[awk 用-F指定多分隔符及正则表达式](http://blog.csdn.net/computer055maxi/article/details/6317251)
	
	命令行选项 -F"[@ /t]" 告诉awk @, 空格和Tab都是字段分隔符，例如：

[awk与cut在以空格为分割域时的区别](http://blog.chinaunix.net/uid-25513153-id-178420.html)

	awk 以空格为分割域时，是以单个或多个连续的空格为分隔符的；
	cut则是以单个空格作为分隔符。
 


LINUX - awk命令之NF和$NF区别  

	NF代表：浏览记录的域的个数
	$NF代表 ：最后一个Field(列)

awk取一行中倒数第N个域，有什么方法吗

	$(NF-5)


 [AWK 输出 ‘，“ 单引号，双引号 ](http://ryyt1231.blog.163.com/blog/static/20708281201101945417606/)

	双引号：

	awk '{print "\""}'        #放大：awk '{print "  \"  “}'

	使用“”双引号把一个双引号括起来，然后使用转移字符\去对双引号进行转意，就可以输出双引号。

	输出单引号的方法跟双引号又有些差别，方法如下

	单引号：

	awk '{print "'\''"}'       # 放大: awk '{print  "  '  \  '  '   " }'

	首先使用一个双引号“”，然后在双引号里面加入两个单引号‘’，接着在两个单引号里面加入一个转移的单引号\'，就可以输出单引号了
	