#Spring 3.x
1. Weblogic - 分层,基于j2ee,服务器
2. IOC: 通过配置,解决了高内聚低耦合的问题
3. AOP: 例如日志文件,每个对象都要设计对应代码,aOP则将之变为公共切面, 每次需要调用写日志功能时,就通过拦截方式,对其进行处理
4. Transaction:
5. Spring取代EJB

##IOC
面向接口->引入工厂->配置文件

Spring提供IOC容器,相当于一个工厂
##DI
Dependency Injection
##实例化Bean方式
1. 类构造器实例化(默认无参数)
2. 静态工厂
3. 动态工厂
##Bean的作用域
1. singleton 单例
2. prototype 每次返回新实例
3. request 每次http请求都会创建新的
4. session 同一个http session共享一个
5. globalSession 用于portlet环境

##Setter方法注入

##集合类型属性注入
1. list,set,map,properties

##AOP
Aspect Oriented Programming

OOP的延伸,OOP纵向集成,AOP横向抽取(性能监视,事务管理,安全检查,缓存)

###两种实现方式

SpringAOP 不需要专门的编译过程和类加载,在运行期间通过代理方式向目标类织入(Weaving)增强代码

AspectJ:基于JAVA+AOP的框架(自己定义AOP切面)
##Aspect
- Joinpoint(连接点):所谓连接点是指那些被拦截到的点。在spring中,这些点指的是方法,因为spring只支持方法类型的连接点.
	- Pointcut(切入点):所谓切入点是指我们要对哪些Joinpoint进行拦截的定义.
- Advice(通知/增强):所谓通知是指拦截到Joinpoint之后所要做的事情就是通知.通知分为前置通知, 后置通知, 异常通知, 最终通知, 环绕通知(切面要完成的功能)
	- Introduction(引介): 引介是一种** 特殊的通知** 在不修改类代码的前提下,  只对某些方法进行增强,现在很少用
	- Introduction可以在运行期为类动态地添加一些方法或Field.
- Target(目标对象):代理的目标对象
	- Weaving(织入): 是指把增强应用到目标对象来创建新的代理对象的过程.
		- spring采用动态代理织入，而AspectJ采用编译期织入和类装在期织入
- Proxy（代理）:一个类被AOP织入增强后，就产生一个结果代理类
	- Aspect(切面): 是切入点和通知（引介）的结合
##代理
1. 动态代理
	1. 用户手动编写代理类,对目标类代理
		1. JDK动态代理、 Javassist 动态
代理 、 Cglib 动态代理,Spring 底层使用 JDK动态代理 + Cglib 动态代理
2. 静态代理
	1. 在虚拟机内部动态构造

###JDK动态代理

	@Test
	public void demo2() {
		// 对目标进行代理
		IUserService target = new UserServiceImpl(); // 获得目标
		// 构造代理工厂
		JdkProxyFactory factory = new JdkProxyFactory(target);
		// 通过工厂创建代理
		IUserService proxy = (IUserService) factory.createProxy();

		proxy.login();
	}

	
	public class JdkProxyFactory implements InvocationHandler {
	
		// 被代理目标对象
		private Object target;
	
		public JdkProxyFactory(Object target) {
			this.target = target;
		}
	
		// 创建代理对象
		public Object createProxy() {
			return Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), this);
		}
	
		@Override
		// 拦截目标对象，执行invoke方法
		public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
			System.out.println("执行代理...");
			return method.invoke(target, args);
		}
	}
##CGLIB动态代理
对于不使用接口的业务类，无法使用JDK动态代理

CGlib采用非常底层字节码技术，可以为一个类创建子类，解决无接口代理问题
##JDK+Spring AOP配置的代理方法
###Advice
	public class MyAroundAdvice implements MethodInterceptor {
	
		@Override
		/**
		 * 记录方法运行时间
		 */
		public Object invoke(MethodInvocation methodInvocation) throws Throwable {
			long start = System.currentTimeMillis();
			Object result = methodInvocation.proceed();
			long end = System.currentTimeMillis();
			System.out.println("方法运行时间：" + (end - start));
			return result;
		}
	}
###applicationContext.xml
	
		<!-- 自定义Advice -->
		<bean id="myaroundAdvice" class="bupt.spring.c_aop.MyAroundAdvice" />
		<bean id="myAspect" class="bupt.spring.d_aspectj.MyAspect" />
    	<!-- 对目标进行AOP代理 -->
    	<aop:config proxy-target-class="true">
    		<!-- 
    			aop:advisor Spring1.2传统意义上切面 ，只支持一个Pointcut切点和一个Advice通知
    			aop:aspect Spring2.0后整合 AspectJ框架定义切面，可以支持多个Pointcut切点和多个Advice通知
    			aop:pointcut 根据AspectJ规则定义切点 
    		 -->
    		 <aop:advisor advice-ref="myaroundAdvice" 
    		 	pointcut="execution(* bupt.spring.c_aop.CustomerServiceImpl.*(..))"/>
		<!--(..)表示所有的参数-->
    	</aop:config>

#### 通过execution函数，可以定义切点的方法切入
- 语法：
	- execution(<访问修饰符>?<返回类型><方法名>(<参数>)<异常>)
- 例如
	- 匹配所有类public方法 execution(public * *(..))
	- 匹配指定包下所有类方法execution(* cn.itcast.dao.*(..)) 不包含子包
		- execution(* cn.itcast.dao..*(..))  ..*表示包、子孙包下所有类
	- 匹配指定类所有方法execution(* cn.itcast.service.UserService.*(..))
	- 匹配实现特定接口所有类方法
		- execution(* cn.itcast.dao.GenericDAO+.*(..))
	- 匹配所有save开头的方法execution(* save*(..))

##AspectJ
-  AspectJ是一个基于Java语言的AOP框架,Spring2.0以后新增了对AspectJ切点表达式支持
- @AspectJ 是AspectJ1.5新增功能，通过JDK5注解技术，
- 允许直接在Bean类中定义切面
- 新版本Spring框架，建议使用AspectJ方式来开发AOP
- 使用AspectJ 需要导入Spring AOP和 AspectJ相关jar包
	- spring-aop-3.2.0.RELEASE.jar
	- com.springsource.org.aopalliance-1.0.0.jar
	- spring-aspects-3.2.0.RELEASE.jar
	- com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
- AspectJ提供不同的通知类型
	- Before 前置通知，相当于BeforeAdvice
	- AfterReturning 后置通知，相当于AfterReturningAdvice
	- Around 环绕通知，相当于MethodInterceptor
	- AfterThrowing抛出通知，相当于ThrowAdvice
	- After 最终final通知，不管是否异常，该通知都会执行
	- DeclareParents 引介通知，相当于
	- IntroductionInterceptor (不要求掌握)

##Transaction
事务管理高层抽象主要包括三个接口

1. PlatformTransactionManager 事务管理器
	1. getTransaction(TransactionDefinition):TransactionStatus
	2. commit
	3. rollback
1. TransactionDefinition 事务定义信息(隔离、传播、超时、只读)
1. TransactionStatus 事务具体运行状态
	1. isNewTransaction():boolean
	2. hasSavePoint():boolean
	3. isRollbackOnly():boolean
	4. setRollbackOnly():void
	5. flush
	6. isCompleted

Spring为不同持久化框架提供了不同PlatformTransactionManager实现

四种事务隔离级别

1. DEFAULT
	1. 根据各数据库不同
2. READ_UNCOMMITED
	1. 脏读,幻读,不可重复读
3. READ_COMMITED
	1. 幻读,不可重复读
4. REPEATABLE_READ
	1. 幻读
4. SERIALIZABLE
	1. 最慢,完全锁定数据


七种事务传播行为

1. PROPAGATION_REQUIRED
2. PROPAGATION_SUPPORTS
3. PROPAGATION_MANDATORY
4. PROPAGATION_REQUIRED_NEW
5. PROPAGATION_NOT_SUPPORTED
6. PROPAGATION_NEVER
7. PROPAGATION_NESTED
##事务传播行为
当一个业务层代码，去调用另一个业务层代码，当被调用方
发生异常，调用方代码是提交还是回滚，这就可以通过事务
传播行为进行控制. 

- REQUIRED ： 将调用方和被调用方，放入同一个事务中 （传播行为默认值 ），如果发生异常，整个事务回滚 （了解 SUPPORTS、MANDATORY ）-- 删除客户案例
- REQUIRES_NEW ： 挂起原来事务，新建一个事务， 调用方和被调用方法处于两个不同的事务，当其中一个事务发生异常，对另一个事务无影响 --- 取钱案例（了解 NOT_SUPPORTED、 NEVER ）
- NESTED ： 嵌套事务 （只对DataSourceTransactionManager 起效），就是使用JDBC3.0之后 SavePoint功能，当被调用方出现异常，可以选择将事务回滚到保存点，然后继续操作
- REQUIRED、NESTED 只有一个事务， REQUIRES_NEW 两个事务， NESTED可以实现REQUIRES_NEW 效果