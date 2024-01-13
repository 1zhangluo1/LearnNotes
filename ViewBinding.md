# ViewBinding

ViewBinding 总体来说其实非常简单，它的目的只有一个，就是为了避免编写 findViewById

要想使用 ViewBinding 需要注意两件事。第一，确保你的 Android Studio 是 3.6 或更高的版本。第二，在你项目工程模块的 build.gradle 中加入以下配 置： android { ... buildFeatures { viewBinding true } } 这样准备工作就完成了。

### 1.在activity中使用ViewBinding

一旦启动了 ViewBinding 功能之后，Android Studio 会自动为我们所编写的每 一个布局文件都生成一个对应的 Binding 类。 

Binding 类的命名规则是将布局文件按驼峰方式重命名后，再加上 Binding 作 为结尾。 比如说，前面我们定义了一个 activity_main.xml 布局，那么与它对应的 Binding 类就是 ActivityMainBinding。 

当然，如果有些布局文件你不希望为它生成对应的 Binding 类，可以在该布局 文件的根元素位置加入如下声明：   

```xml
tools:viewBindingIgnore="true" 
```

接下来我们看一下如何使用 ViewBinding 来实现在 MainActivity 中去设置 TextView 内容的功能，代码如下所示： 

```kotlin
class MainActivity : AppCompatActivity() { override fun onCreate(savedInstanceState: Bundle?) { super.onCreate(savedInstanceState) val binding = ActivityMainBinding.inflate(layoutInflater) setContentView(binding.root) binding.textView.text = "Hello" } } 
```

ViewBinding 的用法可以说就是这么简单。

首先我们要调用 activity_main.xml 布局文件对应的 Binding 类，也就是 ActivityMainBinding 的 inflate()函数 去加载该布局，inflate()函数接收一个 LayoutInflater 参数，在 Activity 中 是可以直接获取到的。

接下来就更加简单了，调用 Binding 类的 getRoot()函数可以得到 activity_main.xml 中根元素的实例，调用 getTextView()函数可以获得 id 为 textView 的元素实例。 

那么很明显，我们应该把根元素的实例传入到 setContentView()函数当中，这 样 Activity 就可以成功显示 activity_main.xml 这个布局的内容了。然后获取 TextView 控件的实例，并给它设置要显示的文字即可。

当然，如果你需要在 onCreate()函数之外的地方对控件进行操作，那么就得将 binding 变量声明成全局变量，写法如下：

```kotlin
class MainActivity : AppCompatActivity() { private lateinit var binding: ActivityMainBinding override fun onCreate(savedInstanceState: Bundle?) { super.onCreate(savedInstanceState) binding = ActivityMainBinding.inflate(layoutInflater) setContentView(binding.root) binding.textView.text = "Hello" } }
```

注意，Kotlin 声明的变量都必须在声明的同时对其进行初始化。而这里我们显 然无法在声明全局 binding 变量的同时对它进行初始化，所以这里又使用了 **<u>lateinit</u>** 关键字对 binding 变量进行了延迟初始化。