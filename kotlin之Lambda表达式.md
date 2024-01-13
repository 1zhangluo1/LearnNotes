## kotlin之Lambda表达式

#### 示例：

在一个水果集合里面找到单词最长的那个水果：

```kotlin
val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon") var maxLengthFruit = "" for (fruit in list) { if (fruit.length > maxLengthFruit.length) { maxLengthFruit = fruit } } println("max length fruit is " + maxLengthFruit)
```

这段代码很简洁，思路也很清晰，可以说是一段相当不错的代码了。但是 如果我们使用集合的函数式API，就可以让这个功能变得更加容易：

```kotlin
val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape",
"Watermelon")
val maxLengthFruit = list.maxBy { it.length }
println("max length fruit is " + maxLengthFruit)
```

上述代码使用的就是函数式API的用法，只用一行代码就能找到集合中单词 最长的那个水果。

首先来看一下Lambda的定义，如果用最直白的语言来阐述的话， Lambda就是一小段可以作为参数传递的代码。从定义上看，这个功能就 很厉害了，因为正常情况下，我们向某个函数传参时只能传入变量，而借 助Lambda却允许传入一小段代码。这里两次使用了“一小段代码”这种描 述，那么到底多少代码才算一小段代码呢？Kotlin对此并没有进行限制，但是通常不建议在Lambda表达式中编写太长的代码，否则可能会影响代码的可读性。 

接着我们来看一下Lambda表达式的语法结构：

**{参数名1: 参数类型, 参数名2: 参数类型 -> 函数体}**

这是Lambda表达式最完整的语法结构定义。首先最外层是一对大括号， 如果有参数传入到Lambda表达式中的话，我们还需要声明参数列表，参 数列表的结尾使用一个->符号，表示参数列表的结束以及函数体的开始， 函数体中可以编写任意行代码（虽然不建议编写太长的代码），并且最后 一行代码会自动作为Lambda表达式的返回值。 当然，在很多情况下，我们并不需要使用Lambda表达式完整的语法结 构，而是有很多种简化的写法。

接下来展示这些简化版的写法是从何而来的：

还是回到刚才找出最长单词水果的需求，前面使用的函数式API的语法结构 看上去好像很特殊，但其实maxBy就是一个普通的函数而已，只不过它接 收的是一个Lambda类型的参数，并且会在遍历集合时将每次遍历的值作 为参数传递给Lambda表达式。maxBy函数的工作原理是根据我们传入的条件来遍历集合，从而找到该条件下的最大值，比如说想要找到单词最长的水果，那么条件自然就应该是单词的长度了。 

理解了maxBy函数的工作原理之后，我们就可以开始套用刚才学习的 Lambda表达式的语法结构，并将它传入到maxBy函数中了，如下所示： 

```kotlin
val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon") val lambda = { fruit: String -> fruit.length } val maxLengthFruit = list.maxBy(lambda)
```

可以看到，maxBy函数实质上就是接收了一个Lambda参数而已，并且这个Lambda参数是完全按照刚才学习的表达式的语法结构来定义的，因此这段代码应该算是比较好懂的。 这种写法虽然可以正常工作，但是比较啰嗦，可简化的点也非常多，下面我们就开始对这段代码一步步进行简化。 

首先，我们不需要专门定义一个lambda变量，而是可以直接将lambda表 达式传入maxBy函数当中，因此第一步简化如下所示：

```kotlin
 val maxLengthFruit = list.maxBy({ fruit: String -> fruit.length })
```

然后Kotlin规定，当Lambda参数是函数的最后一个参数时，可以将 Lambda表达式移到函数括号的外面，如下所示： 

```kotlin
val maxLengthFruit = list.maxBy() { fruit: String -> fruit.length }
```

接下来，如果Lambda参数是函数的唯一一个参数的话，还可以将函数的 括号省略： 

```kotlin
val maxLengthFruit = list.maxBy { fruit: String -> fruit.length }
```

 这样代码看起来就变得清爽多了吧？但是我们还可以继续进行简化。

由于 Kotlin拥有出色的类型推导机制，Lambda表达式中的参数列表其实在大多 数情况下不必声明参数类型，因此代码可以进一步简化成：

```kotlin
 val maxLengthFruit = list.maxBy { fruit -> fruit.length } 
```

最后，当Lambda表达式的参数列表中只有一个参数时，也不必声明参数 名，而是可以使用it关键字来代替，那么代码就变成了： 

```kotlin
val maxLengthFruit = list.maxBy { it.length }
```

通过一步步推导的方式，我们就得到了和一开始那段函数式API一 模一样的写法，

### 再来学习几个集合中比较常用的函数式API：

#### 1.map

集合中的map函数是最常用的一种函数式API，它用于将集合中的每个元素 都映射成一个另外的值，映射的规则在Lambda表达式中指定，最终生成 一个新的集合。比如，这里我们希望让所有的水果名都变成大写模式，就 可以这样写：

```kotlin
 fun main() { val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon") val newList = list.map { it.toUpperCase() } for (fruit in newList) { println(fruit) } }
```



map函数的功能非常强大，它可以按照我们的需求对集合中的元素进行任意 的映射转换，除此之外，你还可以将水果 名全部转换成小写，或者是只取单词的首字母，甚至是转换成单词长度这样一个数字集合，只要在Lambda表示式中编写你需要的逻辑即可。

#### 2.filter

顾 名思义，filter函数是用来过滤集合中的数据的，它可以单独使用，也可 以配合刚才的map函数一起使用。 比如我们只想保留5个字母以内的水果，就可以借助filter函数来实现， 代码如下所示： 

```kotlin
fun main() { val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon") val newList = list.filter { it.length <= 5 } .map { it.toUpperCase() } for (fruit in newList) { println(fruit) } }
```

可以看到，这里同时使用了filter和map函数，并通过Lambda表示式将 水果单词长度限制在5个字母以内。

另外值得一提的是，上述代码中我们是先调用了filter函数再调用map函 数。如果你改成先调用map函数再调用filter函数，也能实现同样的效 果，但是效率就会差很多，因为这样相当于要对集合中所有的元素都进行 一次映射转换后再进行过滤，这是完全不必要的。而先进行过滤操作，再 对过滤后的元素进行映射转换，就会明显高效得多。

#### 3.any和all

any函数用于判断集合中是否至少存在一个元素满足指定条件，all函数用于判断集合中是否所有元素都满足指定条件。由于这两个函数都很好理解，就直接通过代码示例学习了：

```kotlin
 fun main() { val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon") val anyResult = list.any { it.length <= 5 } val allResult = list.all { it.length <= 5 } println("anyResult is " + anyResult + ", allResult is " + allResult) } 
```

这里还是在Lambda表达式中将条件设置为5个字母以内的单词，那么any 函数就表示集合中是否存在5个字母以内的单词，而all函数就表示集合中是否所有单词都在5个字母以内。



#### 4.Runable接口

—Runnable接口。这个接口中只有一个待实现的run()方法， 定义如下：

```kotlin
 public interface Runnable { void run(); }
```

对于任何一个Java方法，只要它接收Runnable参数， 就可以使用函数式API。那么什么Java方法接收了Runnable参数呢？这就有很多了，不过Runnable接口主要还是结合线程来一起使用的。

因此这里我们就通过Java的线程类Thread来学习一下。 Thread类的构造方法中接收了一个Runnable参数，我们可以使用如下 Java代码创建并执行一个子线程：

```kotlin
 new Thread(new Runnable() { @Override public void run() { System.out.println("Thread is running"); } }).start(); 
```

注意，这里使用了匿名类的写法，我们创建了一个Runnable接口的匿名类 实例，并将它传给了Thread类的构造方法，最后调用Thread类的 start()方法执行这个线程。

而如果直接将这段代码翻译成Kotlin版本，写法将如下所示：

```kotlin
 Thread(object : Runnable { override fun run() { println("Thread is running") } }).start()
```

Kotlin中匿名类的写法和Java有一点区别，由于Kotlin完全舍弃了new关键 字，因此创建匿名类实例的时候就不能再使用new了，而是改用了object 关键字。这种写法虽然算不上复杂，但是相比于Java的匿名类写法，并没有什么简化之处。

但是别忘了，目前Thread类的构造方法是符合Java函数式API的使用条件 的，下面我们就看看如何对代码进行精简，如下所示

```kotlin
： Thread(Runnable { println("Thread is running") }).start() 
```

这段代码明显简化了很多，既可以实现同样的功能，又不会造成任何歧 义。因为Runnable类中只有一个待实现方法，即使这里没有显式地重写 run()方法，Kotlin也能自动明白Runnable后面的Lambda表达式就是要在run()方法中实现的内容。 

另外，如果一个Java方法的参数列表中有且仅有一个Java单抽象方法接口 参数，我们还可以将接口名进行省略，这样代码就变得更加精简了：

```kotlin
 Thread({ println("Thread is running") }).start() 
```

不过到这里还没有结束，和之前Kotlin中函数式API的用法类似，当 Lambda表达式是方法的最后一个参数时，可以将Lambda表达式移到方 法括号的外面。同时，如果Lambda表达式还是方法的唯一一个参数，还 可以将方法的括号省略，最终简化结果如下： 

```kotlin
Thread { println("Thread is running") }.start()
```

#### 5.OnClickListener接口

Android中有一个极为常用的点击事件接口 OnClickListener，其定义如下：

```java
 public interface OnClickListener { void onClick(View v); } 
```

可以看到，这又是一个单抽象方法接口。假设现在我们拥有一个按钮 button的实例，然后使用Java代码去注册这个按钮的点击事件，需要这么写：

```java
 button.setOnClickListener(new View.OnClickListener() { @Override public void onClick(View v) { } });
```

而用Kotlin代码实现同样的功能，就可以使用函数式API的写法来对代码进 行简化，结果如下： 

```kotlin
button.setOnClickListener { } 
```

可以看到，使用这种写法，代码明显精简了很多。

### 注意：

的Java函数式API的使用都限定于从Kotlin 中调用Java方法，并且单抽象方法接口也必须是用Java语言定义的。因为Kotlin中有专门的高阶函数来实现更 加强大的自定义函数式API功能，从而不需要像Java这样借助单抽象方法接口来实现。