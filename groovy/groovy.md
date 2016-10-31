# Groovy

### 入门教程
[Groovy Document](http://groovy-lang.org/documentation.html)

[Groovy中的隐式构造函数](http://yeziwang.iteye.com/blog/827155)

	Groovy 中提供了一种可以将List直接转成对象的方式，这种方式将隐式调用Groovy bean中定义的构造函数来创建对象。
	显示使用as来调用对应的构造函数	
	def addr=["home","office"] as Addr
	隐式的让groovy通过类型推断来调用对应的构造函数
	Addr addr=["home","office"]  
	groovy bean需要显示提供对应的构造函数定义。	


[Groovy高效编程——动态改变对象的能力](http://developer.51cto.com/art/200710/58079_all.htm)

[Groovy中的五种特殊运算符](http://it.chinawin.net/softwaredev/article-1b104.html)

	*. 一个集合使用展开运算符(*.)可以得到一个元素为原集合各个元素执行后面指定方法所得值的集合 
	?: Elvis Operator(二元运算符) 由于Groovy中“非空即真”，所以原java中的三元运算符可以简化为二元运算符 
	?. Safe Navigation/Dereference Operator(安全占位符) 安全占位符(?.)主要用于避免空指针异常
	
	.@ 由于Groovy自动的支持属性的getter，但有时候应某种特定的需求，需要自动写一个特殊的getter，如果有时候需要调用特殊的getter，有时候又想调用普通POJO那样的getter，那么怎么办呢？使用Groovy的Field Operator就可以轻松的解决这个问题
	.& Method Closure Operator 我们知道闭包可以被作为一个方法的参数，但是怎么让一个方法作为一个方法的参数呢？Method Closure Operator就是用来解决上述问题的，它允许将一个方法当成一个闭包作为另一个方法的参数。


[Groovy高效编程](http://www.blogjava.net/BlueSUN/archive/2007/08/26/139460.html)

	each 遍历list
	eachWithIndex 带index的each
	any 只要存在一个满足条件（此例中的条件为elem.length() < 3）的element就返回true，否则返回false
	every 所有的element都满足条件才返回true，否则返回false
	grep 符合条件的element会被提取出来，形成一个list 条件以closure的形式传入
	join 用指定的字符连接collection中的element
	sort 根据指定条件进行排序
	find 查找collection中满足条件的‘第一个’element
	findAll查找collection中满足条件的‘所有’element
	collect 对collection的element进行处理，并将处理结果放到一个新的collection中
	groupBy 对collection中的element按给定条件进行分组
	inject 一个累积的过程，传入inject方法的'I'作为sum的初始值，在遍历collection的过程中，将处理结果("$sum $elem ")保存到sum中
	reverse 将collection中各element的次序颠倒一下
	tokenize 指定分隔符，取得token集
	unique 去除collection中重复的element
	max 求最大值
	count 计数
	sum 求和





[Groovy入门教程](http://blog.csdn.net/kmyhy/article/details/4200563)

	1. 不在需要程序员声明任何构造函数，因为groovy自动提供了足够你使用的构造函数。不用担心构造函数不够多，因为实际上只需要两个构造函数（1个不带参数的默认构造函数，1个只带一个map参数的构造函数—由于是map类型，通过这个参数你可以在构造对象时任意初始化它的成员变量）。
	2. groovy中默认的修饰符就是public，所以public修饰符你根本就不需要写，这点跟java不一样。
	 字符串连接符跟java一样，如果你需要把一个字符串写在多行里，可以使用+号连接字符串。代码可以这样写：
       def var="hello "+
       "world"+
       ",groovy!"
	当然更groovy的写法是：
       def var="""hello
       world
       groovy!"""
	三个”号之间不在需要+号进行连接（不过字符串中的格式符都会被保留，包括回车和tab）
	切皆对象
	听起来象是“众生平等”的味道，事实上groovy对于对象是什么类型并不关心，一个变量的类型在运行中随时可以改变，一切根据需要而定。如果你赋给它boolean ，那么不管它原来是什么类型，它接受boolean值之后就会自动把类型转变为boolean值。看下面的代码：
	def var="hello "+
       "world"+
       ",groovy!"
       println var;
       println var.class;
       var=1001
       println var.class
       
       
         默认参数值
	可以为方法指定默认参数值。我们修改repeat方法的定义：
	def repeat(val,repeat=3){
            for(i in 0..<repeat){
             println "This is ${i}:${val}"
            }
       }
	可以看到，repeat方法增加了一个参数repeat（并且给了一个默认值3），用于指定循环次数。
	当我们不指定第2个参数调用repeat方法时，repeat参数取默认值3。

	String 和 Gstring
	除了标准的java.lang.String以外（用’号括住），groovy还支持Gstring字符串类型（用“号括住）。把上	面的for循环中的语句改成：
             println "This is ${i}:${val}"
             
             
    动态性
	Groovy所有的对象都有一个元类metaClass，我们可以通过metaClass属性访问该元类。通过元类，可以为这个对象增加方法（在java中不可想象）！
	

[安全导航](http://www.cnblogs.com/rollenholt/p/3349052.html)

	如果你在访问属性的时候，避免出现空指针异常的话，那么安全导航操作符可能适合你：

	def foo = null
	def bar = foo?.something?.myMethod()
	assert bar == null

 [groovy 定义数组方法](http://zhidao.baidu.com/question/1925109968157524147.html)

 一、数组的定义及赋初值
在Groovy语言中，数组的定义和Java语言中一样。

	    def a = new String[4]
	    def nums = newint[10]
	    def objs = new Object[3]

然后赋值也一样：

	a[0] = 'a'
	a[1] = 'b'
	a[2] = 'c'
	a[3] = 'd'

所不同的在于在数组定义的时候赋初值。

	在Java语言里，对一个字符串数组这样定义：
	String[] strs = new String[]{'a','b','c','d'};

而在Groovy语言中，对一个字符串数组则需要这样定义：

	def strs = ['a','b','c','d'] as String[]


 二、数组的遍历
在Groovy语言中，对数组的遍历方法很多，常用的是使用each方法：

	a.each{

	println it
	}

当然，你也可以使用增强for循环：

	for(it in a)
	{
	println it
	}

你还可以使用如下的遍历方式：
	(0..<a.length).each{
	println a[it]
	}
	···


[Groovy Tip 5 数组](http://blog.csdn.net/hivon/article/details/2312839)

### 反射
[Groovy深入探索——Metaclass的存放](http://www.blogjava.net/johnnyjian/archive/2010/03/19/315962.html)

	总的来说，在各种情况下，Metaclass的存放方式如下： 
	Per-class Metaclass：存放在Class对应的ClassInfo中，而Class到ClassInfo的映射关系则存放在ClassInfo中的一个静态的ManagedConcurrentMap中；
	POGO Per-instance Metaclass：直接存放在对象的metaClass字段中。
	POJO Per-instance Metaclass：对象到Metaclass的映射关系存放在该对象的Class对应的ClassInfo中的一个ManagedConcurrentMap中。

[Groovy基础——MetaClass详解](http://attis-wong-163-com.iteye.com/blog/1235880)

	在groovy中任何的对象都是实现GroovyObject并且继承GroovyObjectSupport的，在GroovyObject的接口中，我们可以看到几个方法首先是getMetaClass方法和setMetaClass方法，metaClass用来支持动态方法和动态参数的调用。另一组方法是getProperty和setProperty方法，这组方法是用来支持动态参数的设定与赋值的。最后还有一个invokeMethod方法，该方法则是用于调用动态方法的。
	
	
### DSL
[Groovy高效编程——创建DSL](http://www.blogjava.net/BlueSUN/archive/2008/05/17/201026.html)

[Groovy高效编程——DSL实战(更新于2008.05.25)](http://www.blogjava.net/BlueSUN/archive/2008/05/24/202609.html)	

### Closure	
	
[Groovy解惑——closure中的delegate](http://www.blogjava.net/BlueSUN/archive/2007/12/22/169580.html)	
	那closure的delegate的默认值是什么呢？默认值是closure所在context中的this（为了方便理解起见，可以暂时这么记忆，因为closure套closure的情况不是很多见。其实closure的delegate的默认值是closure的隐式变量owner，而owner通常引用closure所在context中的this，除非closure所处的context又是个closure，那么owner引用的就是那个外层的closure


[Groovy解惑——closure中的owner](http://www.blogjava.net/BlueSUN/archive/2007/12/archive/2007/12/23/169683.html)

	那么this, delegate以及owner有什么关系呢？
	隐式变量delegate的默认值为owner，
	如果closure没有‘嵌套’在其他closure中，那么该closure的owner的值为this；
	否则该closure的owner引用的是‘直接包含’该closure的closure
	
[闭包为参数的迭代集合的方法](http://blog.csdn.net/escaflone/article/details/5508291)

	1、boolean any(Closure clos)
     有一个集合元素满足闭包条件则返回true
	2、List collect(Closure clos)
     把集合每个元素用闭包转换后返回列表
	3、List clooect(Collection coll,Closure clos)
     把集合每个元素用闭包转换后放到coll中
	4、bollean every(Closure clos)
     判断是否每个元素都满足闭包条件
	5、List findAll(Closure clos)
     从集合中找到满足闭包条件的所有元素
	6、Object find(Closure clos)
     从集合中找的满足闭包条件的第一个元素
	7、int findindexOf(Closure clos)
     从集合中找到满足闭包条件的第一个元素的索引
	8、Object inject(Object value,Closure clos)
     value 与 第一个元素传给闭包，结果值与第二个集合元素又传给闭包，类推。（可以用来求阶乘）
	9、void reverseEach(Closure clos)
     反向迭代
	10、List sort(Closure clos)
     排序集合


### 正则表达式
[groovy-正则表达式](http://www.cnblogs.com/rollenholt/p/3349060.html)

	Groovy使用~”pattern” 来支持正则表达式，它将使用给定的模式字符串创建一个编译好的Java Pattern 对象。Groovy也支持 =~（创建一个Matcher）和 ==~ (返回boolean，是否给定的字符串匹配这个pattern)操作符。

[Groovy之旅系列之五(正则之分组)](http://www.blogjava.net/supercrsky/archive/2008/05/13/200155.html)

[ Unmi 学习 Groovy 之正则表达式](http://blog.csdn.net/kypfos/article/details/3178235)
	
### 文件操作
[groovy操作文件、目录及xml](http://it.chinawin.net/softwaredev/article-e4.html)


### HttpBuilder
[Java程序员为什么学习Groovy(HttpBuilder)](http://www.jianshu.com/p/a519bbd6e26c)


### 单元测试
[Mocking Static Methods in Groovy](https://dzone.com/articles/mocking-static-methods-groovy)

### 操作符
[美妙的操作符](http://www.ibm.com/developerworks/cn/java/j-pg10255.html)

	a == b	a.equals(b)
	a <=> b	a.compareTo(b)
	a > b	如果 a.compareTo(b) 返回的值大于 0，那么这个条件为 true
	a >= b	如果 a.compareTo(b) 返回的值大于等于 0，那么这个条件为 true
	a < b	如果 a.compareTo(b) 小于 0，那么这个条件为 true
	a <= b	如果 a.compareTo(b) 小于等于 0，那么这个条件为 true
	a + b	a.plus(b)
	a - b	a.minus(b)
	a * b	a.multiply(b)
	a / b	a.divide(b)
	a++ or ++a	a.next()
	a-- or --a	a.previous()
	a << b	a.leftShift(b)
	
[Groovy学习笔记——as操作符](http://johnnyjian.iteye.com/blog/160796)

	在Groovy中，as操作符有两种用途：定义导入别名和类型转换。
	只要在import一个类或方法的时候使用as操作符，就可以对其进行重命名
	import java.lang.Math as M  // 定义类的别名  
	assert M.log10(100) == 2  	
	
	语法为“变量 as 类型”，在执行这个操作时，将调用左操作数的类的asType方法：

	class A {  
    	def val  
	    def asType(Class t) {  
    	    assert t == Integer  
        	val  
	    }  
	}  
	def a = new A(val:123)  
	assert a as int == 123  // 这里调用了A#asType方法
	
	
	也可以使用as操作符把一个map转换成一个bean：

	a = [val:321] as A  // 与new A(val:321)功能相同  
	assert a.val == 321  
	
	把一个list用as操作符转换成其他类型时，将使用该类型的合适的构造函数：
	
	class B {  
    	def a  
    	def b  
    	B(a, b) {  
       	 this.a = a  
        	this.b = b  
    	}  
	}  
	def b = [1, 2] as B // 这里调用了B(a, b)构造函数  
	assert b.a == 1 &&  b.b == 2  
	
	
	可以把一个闭包转换成interface，如果该interface中有多个方法，则这些方法都会调用该闭包：
	
	也可以把一个闭包的map转换成interface：
	
	
### Groovy Generics failure

It parses if you add the public modifier

	interface A {
	  public <T> T getByClass( Class<T> clazz )
	}

	
### Groovy2.0 新特性

1. 静态类型检查
2. 静态编译 @CompileStatic 代码会被静态编译，同时生成的字节码非常像javac的字节码，运行速度一样
3. 多catch块 catch(IOException | NullPointerException e) {
	


