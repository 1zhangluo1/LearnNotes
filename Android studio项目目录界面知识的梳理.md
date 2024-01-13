# 项目目录界面知识的梳理

1. #### .gradle和.idea 

   这两个目录下放置的都是Android Studio自动生成的一些文件，我们无须关心，也不要去手动编辑。

2. #### app 

   项目中的代码、资源等内容都是放置在这个目录下的，我们后面的开 发工作也基本是在这个目录下进行的。详细介绍：01. build 这个目录和外层的build目录类似，也包含了一些在编译时自动生成的 文件，不过它里面的内容会更加复杂，我们不需要过多关心。 02. libs 如果你的项目中使用到了第三方jar包，就需要把这些jar包都放在libs 目录下，放在这个目录下的jar包会被自动添加到项目的构建路径里。 03. androidTest 此处是用来编写Android Test测试用例的，可以对项目进行一些自动 化测试。 04. java 毫无疑问，java目录是放置我们所有Java代码的地方（Kotlin代码也 放在这里），展开该目录，你将看到系统帮我们自动生成了一个 MainActivity文件。 05. res 这个目录下的内容就有点多了。简单点说，就是你在项目中使用到的 所有图片、布局、字符串等资源都要存放在这个目录下。当然这个目 录下还有很多子目录，图片放在drawable目录下，布局放在layout目 录下，字符串放在values目录下，所以你不用担心会把整个res目录弄 得乱糟糟的。 06. AndroidManifest.xml 这是整个Android项目的配置文件，你在程序中定义的所有四大组件都 需要在这个文件里注册，另外还可以在这个文件中给应用程序添加权 限声明。由于这个文件以后会经常用到，我们等用到的时候再做详细 说明。 07. test 此处是用来编写Unit Test测试用例的，是对项目进行自动化测试的另 一种方式。 08. .gitignore 这个文件用于将app模块内指定的目录或文件排除在版本控制之外，作 用和外层的.gitignore文件类似。 09. app.iml IntelliJ IDEA项目自动生成的文件，我们不需要关心或修改这个文件中 的内容。 10. build.gradle 这是app模块的gradle构建脚本，这个文件中会指定很多项目构建相 关的配置，我们稍后将会详细分析gradle构建脚本中的具体内容。 11. proguard-rules.pro 这个文件用于指定项目代码的混淆规则，当代码开发完成后打包成安 装包文件，如果不希望代码被别人破解，通常会将代码进行混淆，从 而让破解者难以阅读。

3. #### build 

   这个目录主要包含了一些在编译时自动生成的文件，你也不需要过多 关心。 

4. #### gradle

   这个目录下包含了gradle wrapper的配置文件，使用gradle wrapper的方式不需要提前将gradle下载好，而是会自动根据本地的 缓存情况决定是否需要联网下载gradle。Android Studio默认就是启 用gradle wrapper方式的，如果需要更改成离线模式，可以点击 Android Studio导航栏→File→Settings→Build, Execution, Deployment→Gradle，进行配置更改。 

5. #### .gitignore

    这个文件是用来将指定的目录或文件排除在版本控制之外的。关于版 本控制，我们将在第6章中开始正式的学习。 

6. ####  build.gradle

    这是项目全局的gradle构建脚本，通常这个文件中的内容是不需要修 改的。稍后我们将会详细分析gradle构建脚本中的具体内容。 

7. #### gradle.properties 

   这个文件是全局的gradle配置文件，在这里配置的属性将会影响到项 目中所有的gradle编译脚本。 

8. #### gradlew和gradlew.bat

    这两个文件是用来在命令行界面中执行gradle命令的，其中gradlew 是在Linux或Mac系统中使用的，gradlew.bat是在Windows系统中 使用的。 

9. ####  HelloWorld.iml 

   iml文件是所有IntelliJ IDEA项目都会自动生成的一个文件（Android Studio是基于IntelliJ IDEA开发的），用于标识这是一个IntelliJ IDEA 项目，我们不需要修改这个文件中的任何内容。 

10. #### local.properties

     这个文件用于指定本机中的Android SDK路径，通常内容是自动生成 的，我们并不需要修改。除非你本机中的Android SDK位置发生了变 化，那么就将这个文件中的路径改成新的位置即可。 

11. ####  settings.gradle 

    这个文件用于指定项目中所有引入的模块。由于HelloWorld项目中只 有一个app模块，因此该文件中也就只引入了app这一个模块。通常情 况下，模块的引入是自动完成的，需要我们手动修改这个文件的场景 可能比较少。
    
12. #### res

     所有以“drawable”开头的目录都是用来放图片的，所有 以“mipmap”开头的目录都是用来放应用图标的，所有以“values”开头的 目录都是用来放字符串、样式、颜色等配置的，所有以“layout”开头的目 录都是用来放布局文件的。

     之所以有这么多“mipmap”开头的目录，其实主要是为了让程序能够更好 地兼容各种设备。drawable目录也是相同的道理，虽然Android Studio 没有帮我们自动生成，但是我们应该自己创建drawable-hdpi、 drawable-xhdpi、drawable-xxhdpi等目录。在制作程序的时候，最好 能够给同一张图片提供几个不同分辨率的版本，分别放在这些目录下，然 后程序运行的时候，会自动根据当前运行设备分辨率的高低选择加载哪个 目录下的图片。当然这只是理想情况，更多的时候美工只会提供给我们一 份图片，这时你把所有图片都放在drawable-xxhdpi目录下就好了，因为 这是最主流的设备分辨率目录。

     