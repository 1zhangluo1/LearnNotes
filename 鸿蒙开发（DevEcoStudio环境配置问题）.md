## DevEco Studio环境配置时ohpm下载失败解决办法：

#### 当遇到

#### Error: execute install task failed, component ohpm.zip.

#### Error: execute 'ohpm install' failed.

#### 如上报错原因的时候可以参照本方法来解决问题。

## 解决方案：

配置NPM代理
Hvigor、ohpm、SDK在初始化时需要从npm仓库下载依赖,如果需要代理才能访问网络,请配置npm的代理。
可通过如下步骤进入npm代理配置界面:

​	1.在欢迎页单击Configure(或图标)>Settings>Build,Execution,Deployment>Node.js and npm>Optimizeconfig,进入npm代理设置界面(macOS为Configure>Preferences>Build,Execution,Deployment>Node.js and npm>Optimize config)。

​	2.在打开了工程的情况下,可以单击File>Settings>Build,Execution,Deployment>Node.js and npm>Optimizeconfig,进入npm代理设置界面(macOS为DevEco Studio>Preferences>Build,Execution,Deployment>Node.js andnpm>Optimize config)。

进入后勾选上npm registry选项和ohos registry选项，之后点击ok确定更改配置即可。

完成如上步骤之后就可以 按照报错提示下载好ohpm到合适的位置，然后环境配置就完成了。

#### 注：好像在下载ohpm之前一定得先配置好node.js才行。