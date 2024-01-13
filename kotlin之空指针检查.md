## kotlin之空指针检查

### 1.避免空指针的核心机制：

**Kotlin默认所有的参数和变量都不可为空，所以这里传入 的Study参数也一定不会为空，我们可以放心地调用它的任何函数。**

### 2.需要使用空值的时候：

Kotlin提供了另外一套可为空的类型系统，就是在类名的后面加上一 个问号。比如，Int表示不可为空的整型，而Int?就表示可为空的整型； String表示不可为空的字符串，而String?就表示可为空的字符串。

### 3.判空辅助工具

#### (1). ?.

首先学习最常用的?.操作符。

这个操作符的作用非常好理解，就是当对象不为空时正常调用相应的方法，当对象为空时则什么都不做。比如以下的 判空处理代码：

```java
 if (a != null) { a.doSomething() } 
```

这段代码使用?.操作符就可以简化成：

```kotlin
 a?.doSomething()
```

可以看到，这样我们就借助?.操作符将if判断语句去掉了。

#### (2). ?:

我们再来学习另外一个非常常用的?:操作符。这个操作符的左右两边都接收一个表达式，如果左边表达式的结果不为空就返回左边表达式的结果，否则就返回右边表达式的结果。

观察如下代码：

```kotlin
 val c = if (a ! = null) { a } else { b } 
```

这段代码的逻辑使用?:操作符就可以简化成：

```kotlin
val c = a ?: b
```

接下来我们通过一个具体的例子来结合使用?.和?:这两个操作符，从而加深对它们的理解。 

比如现在要编写一个函数用来获得一段文本的长度，使用传统的写法 就可以这样写：

```kotlin
 fun getTextLength(text: String?): Int { if (text != null) { return text.length } return 0 } 
```

由于文本是可能为空的，因此我们需要先进行一次判空操作，如果文本不 为空就返回它的长度，如果文本为空就返回0。 

这段代码看上去也并不复杂，但是我们却可以借助操作符让它变得更加简 单，如下所示：

```kotlin
 fun getTextLength(text: String?) = text?.length ?: 0 
```

这里我们将?.和?:操作符结合到了一起使用，首先由于text是可能为空的，因此我们在调用它的length字段时需要使用?.操作符，而当text为空时，text?.length会返回一个null值，这个时候我们再借助?:操作符让它返回0。

#### (3). !!.

不过Kotlin的空指针检查机制也并非总是那么智能，有的时候我们可能从逻辑上已经将空指针异常处理了，但是Kotlin的编译器并不知道，这个时候它 还是会编译失败。 观察如下的代码示例：

```kotlin
 var content: String? = "hello" fun main() { if (content != null) { printUpperCase() } } fun printUpperCase() { val upperCase = content.toUpperCase() println(upperCase) } 
```

这里我们定义了一个可为空的全局变量content，然后在main()函数里先 进行一次判空操作，当content不为空的时候才会调用 printUpperCase()函数，在printUpperCase()函数里，我们将 content转换为大写模式，最后打印出来。

看上去好像逻辑没什么问题，但是很遗憾，这段代码一定是无法运行的。 因为printUpperCase()函数并不知道外部已经对content变量进行了非 空检查，在调用toUpperCase()方法时，还认为这里存在空指针风险，从 而无法编译通过。

在这种情况下，如果我们想要强行通过编译，可以使用非空断言工具，写 法是在对象的后面加上!!.

如下所示：

```kotlin
 fun printUpperCase() { val upperCase = content!!.toUpperCase() println(upperCase) }
```

这是一种有风险的写法，意在告诉Kotlin，我非常确信这里的对象不会为空，所以不用你来帮我做空指针检查了，如果出现问题，你可以直接抛出空指针异常，后果由我自己承担。

#### (4). let

let既不是操作 符，也不是什么关键字，而是一个函数。这个函数提供了函数式API的编程 接口，并将原始调用对象作为参数传递到Lambda表达式中。示例代码如 下：

```kotlin
 obj.let { obj2 -> // 编写具体的业务逻辑 } 
```

可以看到，这里调用了obj对象的let函数，然后Lambda表达式中的代码 就会立即执行，并且这个obj对象本身还会作为参数传递到Lambda表达式中。不过，为了防止变量重名，这里我将参数名改成了obj2，但实际上它们是同一个对象，这就是let函数的作用。

可以结合使用?.操作符和let函数来对代码进行优化，如下所示：

```kotlin
 fun doStudy(study: Study?) { study?.let { stu -> stu.readBooks() stu.doHomework() } } 
```

我来简单解释一下上述代码，?.操作符表示对象为空时什么都不做，对象不为空时就调用let函数，而let函数会将study对象本身作为参数传递到 Lambda表达式中，此时的study对象肯定不为空了，我们就能放心地调用它的任意方法了。 另外还记得Lambda表达式的语法特性吗？当Lambda表达式的参数列表中只有一个参数时，可以不用声明参数名，直接使用it关键字来代替即可，那么代码就可以进一步简化成： 

```kotlin
fun doStudy(study: Study?) { study?.let { it.readBooks() it.doHomework() } }
```

let函数是可以处理全局变量的 判空问题的，而if判断语句则无法做到这一点。比如我们将doStudy()函 数中的参数变成一个全局变量，使用let函数仍然可以正常工作，但使用 if判断语句则会提示错误之所以这里会报错.

是因为全局变量的值随时都有可能被其他线程所修改，即使做了判空处理，仍然无法保证if语句中的study变量没有空指针风险。从这一点上也能体现出let函数的优势。