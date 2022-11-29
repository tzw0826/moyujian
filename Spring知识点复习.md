#### 什么是Spring？

- Spring是一个轻量级的IOC（控制反转）和AOP（面向切面）容器框架。是为Java应用程序提供基础性服务的一套框架，目的是用于简化企业级应用程序的开发，它使得开发者只需关心业务需求。
- Spring的功能底层都依赖于它的两个核心特性：依赖注入（DI）和面向切面编程（AOP）。

#### Spring框架的设计目标，设计理念，核心是什么？

- **Spring设计目标：**为开发者提供一个一站式轻量级应用开发平台；
- **Spring设计理念：**在JavaEE开发中，支持POJO和JavaBean开发方式，使应用面向接口开发，充分支持OO（面向对象）设计方法；通过IOC容器实现对象耦合关系的管理，并实现依赖反转，将对象之间的依赖关系交给IOC容器，实现解耦；
- **Spring框架的核心：**IOC容器和AOP模块。通过IOC容器管理POJO对象以及他们之间的耦合关系；通过AOP以动态非侵入的方式增强服务；IOC让互相协作的组件保持松散的耦合，而AOP编程允许你把遍布于应用各层的功能分离出来形成可重用的功能组件。

#### Spring的优点

- Spring属于低侵入式设计，代码的污染极低；
- Spring的DI机制将对象之间的依赖关系交由框架处理，减低组件的耦合性；
- Spring提供了AOP技术，支持将一些通用任务，如安全、事务、日志、权限等进行集中式管理，从而提供更好的复用；
- Spring对主流的应用框架提供了集成支持。

#### Spring对IOC的理解

- 控制反转（Inversion of Control，缩写为IOC），是面向对象编程中的一种设计思想，可以用来降低代码之间的耦合度，符合依赖倒置原则。它将对象的创建权交出去，将对象和对象之间关系的管理权交出去，由Spring来负责控制对象的生命周期（比如创建、销毁）和对象间的依赖关系。
- 控制反转常见的实现方式：依赖注入（Dependency Injection，简称DI）。通常依赖注入的实现包括两种方式：
  - set方法注入
  - 构造方法注入


#### Spring对AOP的理解

- IOC使软件组件松耦合，AOP让你能够捕捉系统中经常使用的功能，把它转换为组件。
- AOP（Aspect Orieted Programmin）：面向切面编程，面向方面编程。（AOP是一种编程技术）
- AOP是对OOP的补充延伸，实现AOP的关键在于代理模式，AOP代理主要分为静态代理和动态代理。静态代理的代表为AspectJ；动态代理则以SpringAOP为代表。
- SpringAOP中的动态代理主要有两种方式：JDK动态代理和CGLib动态代理。
  - Spring在这两种动态代理中灵活切换，如果是代理接口，会默认使用JDK动态代理，如果要代理某个类，这个类没有实现接口，就会切换使用CGLIB。

- 面向切面，将与核心业务无关的代码独立的抽取出来，形成一个独立的组件，然后以横向交叉的方式应用到业务流程当中的过程称为AOP。
- AOP的优点：
  - 代码复用性强；
  - 代码易维护；
  - 使开发者更关注业务逻辑。


#### AOP七大术语

- 连接点（Joinpoint）

  - 指程序运行过程中所执行的方法。在SpringAOP中，一个连接点代表一个方法的执行。

- 切点（Pointcut）

  - 在程序执行流程中，真正织入切面的方法，一个切点对应多个连接点。

- 通知（Advice）

  - 通知又叫增强，如权限校验、日志记录等。

  - 通知包括：

    - 前置通知 Before

    - 后置通知 After

    - 环绕通知 Around

    - 异常通知 After throwing

    - 最终通知 After returning

- 切面（Aspect）

  - 被抽取出来的公共模块，可以用来横切多个对象。由切点和通知的结合。

- 织入（Wearing）

  - 通过动态代理，在目标对象（Target）的方法（即连接点Joinpoint）中执行增强逻辑（Advice）的过程。

- 代理对象（Porxy）

  - 一个目标对象被织入通知后产生的新对象。

- 目标对象（Target）

  - 包含连接点的对象，也被称作被通知的对象。由于Spring AOP是通过动态代理实现的，所以这个对象永远是一个代理对象。


#### Spring的通知类型

Advice的类型：

- 前置通知（Before Advice）：在连接点之前执行的通知。

- 后置通知（After Advice）：当连接点退出的时候执行的通知（不论是正常返回还是异常退出）。 
- 环绕通知（Around Advice）：包围一个连接点的通知，这是最强大的一种通知类型。 环绕通知可以在方法调用前后完成自定义的行为。它也可以选择是否继续执行连接点或直接返回它们自己的返回值或抛出异常来结束执行。
- 返回后通知（AfterReturning Advice）：在连接点正常完成后执行的通知（如果连接点抛出异常，则不执行）
- 抛出异常后通知（AfterThrowing advice）：在方法抛出异常退出时执行的通知

#### Advice的执行顺序

没有异常的执行顺序：

- - around before advice
  - before advice
  - target method 执行
  - after advice
  - around after advice
  - afterReturning advice

出现异常情况下的执行顺序：

- - around before advice
  - before advice
  - target method 执行
  - after advice
  - around after advice
  - afterThrowing advice
  - java.lang.RuntimeException：异常发生

#### Bean的生命周期

**分为7步：**

- - 实例化Bean
  - Bean属性赋值
  - Bean后处理器before执行
  - 初始化Bean
  - Bean后处理器after执行
  - 使用Bean
  - 销毁Bean

**分为10步：**

- - 实例化Bean
  - Bean属性赋值
  - 检查Bean是否实现了Aware的相关接口，并设置相关依赖
  - Bean后处理器before执行
  - 检查Bean是否实现了InitializingBean接口，并掉i用接口方法
  - 初始化Bean
  - Bean后处理器after执行
  - 使用Bean
  - 检查Bean是否实现了DisposableBean接口，并调用接口方法
  - 销毁Bean

#### Spring循环依赖的三种形态

1. 互相依赖：A依赖B，B依赖A；
2. 间接依赖：A依赖B，B依赖C，C依赖A；
3. 自我依赖：自己依赖自己。

#### Spring如何解决循环依赖问题（BeanCurrentlyInCreationException，当前的Bean正在处于创建中异常）

1、什么是循环依赖：

​	类与类之间的依赖关系形成了闭环，就会导致循环依赖问题的产生。

​	例：A类依赖B类，B类依赖C类，C类又依赖A类，这样就形成了循环依赖问题。

2、循环依赖在Spring中主要有三种情况：

- 通过构造方法进行依赖注入时产生的；

- 通过setter方法进行依赖注入且是在多例模式下产生的；
- 通过setter方法在单例模式下产生的。

3、Spring无法解决setter在多例下和在构造方法下发生的循环依赖问题

- setter + 多例 ：每一次getBean() 时，都会产生一个新的Bean，如此反复下去就会有无穷无尽的Bean产生，最终发生OOM（内存溢出）；

- 构造方法：构造方法注入会导致实例化对象和对象属性赋值的过程没有分离开，必须在一起完成所导致的。

4、为什么 singleton + setter 模式下发生的循环依赖被Spring解决了？如何解决的？

​	主要原因是，在这种模式下Spring对Bean的管理主要分为清晰的两个阶段：

​		第一个阶段：在Spring容器加载的时候，实例化Bean，只要其中任意一个Bena实例化之后，马上进行“曝光”【不等属性赋值就曝光】；

​		第二个阶段：Bean“曝光”之后，再进行属性的赋值（调用set方法）。

​			核心解决方案是：实例化对象和对象的属性赋值分为两个阶段来完成的。

​	Spring底层实现原理

```java
	protected Object getSingleton(String beanName, boolean allowEarlyReference) {
		// 尝试在一级缓存 singletonObjects 中获取
		Object singletonObject = this.singletonObjects.get(beanName);
		// 如果没有从一级缓存中获取到, 并且获取的 bean 正在创建中
		if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
			// 从二级缓存 earlySingletonObjects 中获取
			singletonObject = this.earlySingletonObjects.get(beanName);
			// 如果没有从二级缓存中获取到, 并且允许创建早期对象的引用
			if (singletonObject == null && allowEarlyReference) {
				// 进入同步代码块, 锁定全局变量并进行处理
				synchronized (this.singletonObjects) {
					// 再次从 singletonObjects 一级缓存中获取
					singletonObject = this.singletonObjects.get(beanName);
					// 如果没有从一级缓存中获取到
					if (singletonObject == null) {
						// 再次从 earlySingletonObjects 二级缓存中获取
						singletonObject = this.earlySingletonObjects.get(beanName);
						// 如果没有获取到
						if (singletonObject == null) {
							// 从三级缓存中获取, 三级缓存中获取到的不是我们需要的实例, 三级缓存中保存的是 ObjectFactory 是一个工厂
							ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
							// 如果从三级缓存中获取到
							if (singletonFactory != null) {
								// 从对象工厂中获取 bean 实例对象(调用工厂方法获取 bean 实例对象, lambda 表达式回调获取)
								// 当某些方法需要提前初始化的时候则会调用 addSingletonFactory 方法将对应的 ObjectFactory 初始化策略									存储在 singletonFactories 中
								singletonObject = singletonFactory.getObject();
								// 放入二级缓存中, 一级缓存用于存放完整实例化的 bean 实例, 此时获取的 bean 实例并非完整的 bean 实例
								this.earlySingletonObjects.put(beanName, singletonObject);
								// 将获取到的对象工厂从三级缓存中移除
								this.singletonFactories.remove(beanName);
							}
						}
					}
				}
			}
		}
		// 返回从 Spring 三级缓存中获取到的单实例 bean 对象
		return singletonObject;
	}
```

5、解决构造函数互相注入造成的循环依赖

​	前面说Spring可以自动解决单例模式下通过setter()方法进行依赖注入产生的循环依赖问题。而对于通过[构造方法](https://so.csdn.net/so/search?q=构造方法&spm=1001.2101.3001.7020)进行依赖注入时产生的循环依赖问题没办法自动解决，那针对这种情况，我们可以使用@Lazy注解来解决。

​	也就是说，对于类A和类B都是通过构造器注入的情况，可以在A或者B的构造函数的形参上加个@Lazy注解实现延迟加载。@Lazy实现原理是，当实例化对象时，如果发现参数或者属性有@Lazy注解修饰，那么就不直接创建所依赖的对象了，而是使用动态代理创建一个代理类。

​	比如，类A的创建：A a=new A(B)，需要依赖对象B，发现构造函数的形参上有@Lazy注解，那么就不直接创建B了，而是使用动态代理创建了一个代理类B1，此时A跟B就不是相互依赖了，变成了A依赖一个代理类B1，B依赖A。但因为在注入依赖时，类A并没有完全的初始化完，实际上注入的是一个代理对象，只有当他首次被使用的时候才会被完全的初始化。

#### 为什么第三级缓存要使用ObjectFactory

​	如果仅仅是解决循环依赖问题，使用二级缓存就可以了，但是如果对象实现了AOP，那么注入到其它bean的时候，并不是最终的代理对象，而是原始的。这时就需要通过三级缓存的ObjectFactory才能提前产生最终需要代理的对象。

![img](https://cdn.nlark.com/yuque/0/2022/png/32486163/1667874005923-95bfaf10-3d3f-49f0-b583-08d384f13148.png)

#### Spring框架中都用到了哪些设计模式
