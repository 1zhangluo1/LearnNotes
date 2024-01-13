## kotlin之函数可见性修饰符

Java中有public、private、protected和 default（什么都不写）这4种函数可见性修饰符。Kotlin中也有4种，分 别是public、private、protected和internal，需要使用哪种修饰 符时，直接定义在fun关键字的前面即可。

首先private修饰符在两种语言中的作用是一模一样的，都表示只对当前 类内部可见。

public修饰符的作用虽然也是一致的，表示对所有类都可 见，但是在Kotlin中public修饰符是默认项，而在Java中default才是默 认项。前面我们定义了那么多的函数，都没有加任何的修饰符，所以它们 默认都是public的。protected关键字在Java中表示对当前类、子类和 同一包路径下的类可见，在Kotlin中则表示只对当前类和子类可见。

Kotlin 抛弃了Java中的default可见性（同一包路径下的类可见），引入了一种 新的可见性概念，只对同一模块中的类可见，使用的是internal修饰符。 比如我们开发了一个模块给别人使用，但是有一些函数只允许在模块内部 调用，不想暴露给外部，就可以将这些函数声明成internal。

