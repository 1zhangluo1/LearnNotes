# 运行Android Studio可能出现的问题



  在使用android studio时，**在build.gradle.kts中SDK后的序号需要改为34才能正常运行**，否则就会出现报错，无法运行。

  修改后就如此：![image-20231106213725880](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231106213725880.png)

  而且修改完毕后要记得点击“Sync now”，要不修改后也没有用！！！

## 日志的使用

日志在报错(尤其是空指针时)是有很大作用的，能够清楚地知道是在哪一步出现了错误。而日志中经常使用的就绕不开Log的用法了。

以下：

- Log.v()

  用于打印那些最为琐碎的、意义最小的日志信息。对应级别**verbose**，是Android日志里面级别最低的一种。

- Log.d()

  用于打印一些调试信息，这些信息对你调试程序和分析问题应该是有帮助的。对应级别**debug**，比verbose高一级。

- Log.i()

  用于打印一些比较重要的数据，这些数据应该是你非常想看到的、可以帮你分析用户行为数据。对应级别**info**，比debug高一级。

- Log.w()

  用于打印一些警告信息，提示程序在这个地方可能会有潜在的风险，最好去修复一下这些出现警告的地方。对应级别**warn**，比info高一级。

- Log.e()

  用于打印程序中的错误信息，比如程序进入到了catch语句当中。当有错误信息打印出来的时候，一般都代表你的程序出现严重问题了，必须尽快修复。对应级别**error**，比warn高一级。

  这些是基本的Log用法，其中我最常用Log.d来找寻程序中的一些问题。