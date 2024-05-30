# flutter中BottomAppBar调整高度会报错的原因及解决办法：

## 前言：

在flutter开发中想要写出中间部分凹陷有一个悬浮按钮的导航栏会用到**BottomAppBar**这个组件。该组件指定其形状(shape参数)为：

```dart
shape: const CircularNotchedRectangle(),
```

便可以轻松地写出中间凹陷的导航栏。但是默认的**BottomAppBar**高度很高，看起来应用界面积就会是一个大下巴。个人认为非常影响App界面美观。如果直接指定其***height***的话，如下：

```dart
BottomAppBar(
      shape: const CircularNotchedRectangle(),
      notchMargin: 10.0,
      shadowColor: Colors.black,
      color: Colors.white,
      surfaceTintColor: Colors.white,
      elevation: 5,
      height: 60,}
```

你的导航栏下面内容如果是纯Icon的话可能还能容下，但是如果是Icon加文字的话，极大概率是会得到组件溢出报错的。那么如何解决这个问题呢？接下来我就说明我本次的心得体会。

## 问题原因：

其实此问题的原因这个也并不困难，甚至可以说是很简单。经过我多次验证，发现原因在于

**BottomAppBar**这个组件本身会将在其**child**中的**row**中的组件加上一个默认的**padding**。

其padding值就会影响里面每个item的空间。从而导致即便item的大小明明明显不会溢出容器却还是报错的情况，因为padding的填充导致item本身的所处空间极大所缩水，item所需空间自然是不足的啦，所以报错。

## 解决办法：

我们依然是将**BottomAppBar**的高度（height）调整为自己觉得合适的程度，比如我一般就会设置为60。然后有一个极为关键的属性**padding**。此属性是指BottomAppBar中的item之间的空白填充。如果不声明此属性的话，flutter就会使用默认的值来构建。所以我们可以将其主动声明为0，或者是调整到自己觉得合适的程度。（ps：我认为在水平方向上可以不用过多声明，因为row自带的`mainAxisAlignment: MainAxisAlignment.spaceAround`就将水平空间平均分配了。）我一般是在其垂直方向上做出微调。因为我认为item还是得与导航栏有一个较为合理的空间留白才显得更加美观。以下是我的代码示例：

```dart
Widget bottomBar() {
    return BottomAppBar(
      shape: const CircularNotchedRectangle(),
      notchMargin: 10.0,
      shadowColor: Colors.black,
      color: Colors.white,
      surfaceTintColor: Colors.white,
      elevation: 5,
      height: 60,
      padding: EdgeInsets.only(top: 10),
      child: Row(
        mainAxisSize: MainAxisSize.max,
        mainAxisAlignment: MainAxisAlignment.spaceAround,
        children: <Widget>[
          bottomItem(0, Icons.school, "首页",),
          bottomItem(1, Icons.table_view, "课表"),
          const SizedBox(width: 40,),
          bottomItem(2, Icons.forum, "论坛"),
          bottomItem(3, Icons.person, "我的"),
        ],
      ),
    );
  }

  Widget bottomItem(int index, IconData? icon, String title, {Color? color = Colors.grey}) {
    return Expanded(
      flex: 1,
      child: InkWell(
        splashColor: Colors.transparent,
        onTap: () {
          setState(() {
            pageId = index;
            _controller.animateToPage(index,
                duration: const Duration(
                    days: 0, hours: 0, minutes: 0, milliseconds: 250),
                curve: Curves.linear);
          });
        },
        child: Column(
          children: [
            Icon(icon,color: pageId == index ? Colors.cyan : color,),
            Text(title),
          ],
        ),
      ),
    );
  }
```

这样声明以后问题就完美的解决啦！

# 结语

希望此篇文章能够帮助您解决实际开发中遇到的问题。如文章中有问题，还望多多包涵，也欢迎大家来指正我的错误，给我提出宝贵的意见和建议。