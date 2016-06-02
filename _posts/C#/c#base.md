<title>c#基础</title>
#c#基础


- 数据类型 
	- 值类型
		- 预定义值类型变量
			- Signed:sbyte, short, int, long
			- Unsigned:byte, ushort, uint, ulong
			- Floating-point:float, double, decimal
			- Character:char
			- Logical:bool
		- 自定义值类型变量(<b>struct</b>,enum)
	- 引用类型
		- 预定义引用类型(string(不可变),object)
		- 自定义引用类型(类<b>(class)</b>,数组,接口,委托,事件...)
	- 赋值特性
- 参数传递特性
	- 值类型： 传值
		- 如果需要改变参数值,使用ref
		- 若不需要参数初始值,使用out
	- 引用类型： 传址（本身就是地址）
- 预定义类型
- 用户自定义类型
- 类型转换
- 变量与常量
- 运算符
- 流控制
- 程序的结构 

####值类型和引用类型。
>- 值类型表示变量本身
引用类型表示其引用。
- 值类型和引用类型使用相同的语法来分配内存；
- 所有内存的释放都不需要手工地进行，CLR执行一种算法来跟踪可以访问的和不能访问的引用变量，定期清除那些不能访问的对象，并将其内存返回给操作系统。
- 预定义类型除了object和string之外都为值类型
- 自定义类型除了结构（struct）和枚举（enum）之外都为引用类型。

####初始化方式:
int i = 3 | int i = new int()(相当于0)

string a = "a"

在未初始化之前不能读,最好不要写

####Ref,Out传参
- 如果需要改变参数值,使用ref <br>for example:private void g(ref vpoint p)
- 若不需要参数初始值,使用out <br>for example:void f(out p) {p=8;}
		<br>如果使用ref时,参数变量没有初始化,则会出错, 此时若不需要初始值,可以直接使用out


#####对于引用类型，不用使用ref也可以改变引用对象的值。但使用ref可以改变整个对象指针

####Object

- 根类型。是其他所有类型（预定义和自定义的，值的和引用的）的基类型。语言通常不要求类声明从 Object 的继承，因为继承是隐式的。
- 因为 .NET Framework 中的所有类均从 Object 派生，所以 Object 类中定义的每个方法可用于系统中的所有对象。派生类可以而且确实重写这些方法中的某些，其中包括： 
	- Equals — 支持对象间的比较。 
	- Finalize — 在自动回收对象之前执行清理操作。 
	- GetHashCode — 生成一个与对象的值相对应的数字以支持哈希表的使用。 
	- ToString — 生成描述类的实例的可读文本字符串。

####数组

			- double[ ,] matrix =new double [10,10];

动态长度变化用ArrayList

####类型转换

#####隐式转换
>只能从较小的整数类型隐式转换为较大的整数类型，或者从无符号类型转换为大小相同的有符号类型。

#####checked
	<br>ss= checked((short)ii); //为避免上述情形，使用checked运算符来检测转换操作是否发生异常。需与异常处理配合使用。
	<br>try		{ss=checked((short)ii);	}
	<br>catch {  MessageBox.Show ("err");};

#####System.Convert类
si=Convert.ToInt32(s,10);

####变量与常量
######c#不允许全局变量
######常量语法：Const 类型 标识符＝值

####运算符
- 算术 +   -   *   /   % 
- 逻辑（布尔型和按位） &   |   ^   !   ~   &&   ||   true   false 
- 字符串串联 + 
- 递增、递减 ++   -- 
- 移位 <<   >> 
- 关系 ==   !=   <   >   <=   >= 
- 赋值 =   +=   -=   *=   /=   %=   &=   |=   ^=   <<=   >>= 
- 成员访问 . 
- 索引 [] 
- 转换 () 
- 条件 ?: 
- 创建对象 new 
- 类型信息 as   is   sizeof   typeof    
- 溢出异常控制 checked   unchecked 
- 间接寻址和地址 *   ->   []   & 
- 运算符可以重载
####流控制
- 条件语句  if else if
- 分支判断 Switch case
- 循环语句
	- For  
	- while 
	- for each   (VB)  
		>Int [ ] ints={1,2,3}
		<br>For each(int tmp in ints)
		<br>{ Console.writeline(tmp);}
	- do while
- 跳转语句
	- goto 
	- break 
	- continue
	- return
####程序的结构
- 名称空间  使用名称空间来组织类。
	- Using 名称空间
类似于java的import，c/C++的include。指示编译器在.netframework中寻找类库的支持。
类
- 数据成员： 字段，常量，事件。
- 函数成员： 方法，属性，构造函数，析构函数，操作符，索引
- Main方法。
	- Main方法必须为static。返回值 int 或void。
	- public static void main（string [ ]args)
- 注释  c++风格注释

