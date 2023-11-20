# 运行Android Studio可能出现的问题



  在使用android studio时，**在build.gradle.kts中SDK后的序号需要改为34才能正常运行**，否则就会出现报错，无法运行。

  修改后就如此：![image-20231106213725880](C:\Users\张洛\AppData\Roaming\Typora\typora-user-images\image-20231106213725880.png)

  而且修改完毕后要记得点击“Sync now”，要不修改后也没有用！！！