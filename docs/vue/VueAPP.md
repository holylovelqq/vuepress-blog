# VUE原生APP制作

::: tip
2019 世界移动通信大会 (MWC 大会) 于 2 月 27 日在巴塞罗那顺利拉开帷幕。值此移动盛会，Flutter 团队宣布正式推出 Flutter 1.2,这是flutter更新的首个稳定版本。

Flutter 是 Google 用以帮助开发者在 iOS 和 Android 两个平台开发高质量原生 UI 的移动 SDK。Flutter 兼容现有的代码，免费并且开源，在全球开发者中广泛被使用

有句话叫google出品必属精品，可以预测未来的移动端开发框架的天下必然是属于flutter的,什么react-native、weex、uni-app都将逐渐退出历史舞台。所以如果你的业务涉及到移动端app开发，那么就从今天起学习flutter吧！

由于作者暂时尚未涉及到这一块业务，所以Flutter的学习留待以后，本章内容暂时保留

附[Flutter中文网](https://flutter-io.cn/)[Flutter英文官网](https://flutter.dev/)，网上已经存在很多Flutter相关的教程，有兴趣的可以自己搜索查看
:::
⭐以下使用到的框架/库/插件等，license均为MIT⭐

⭐实际操作以安卓为例，但是每一步都会介绍IOS对应的操作⭐

关于license介绍，请参见阮一峰[如何选择开源许可证](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html)

## 目标

+ 使用vue开发一个简单的项目（可以使用现有的项目）
+ 使用weex（或者其他框架）新建项目或对项目进行修改，制作成一个IOS/Android app
+ 进行客户端打包->熟悉客户端打包流程
+ 安装在自己手机上试用

## 步骤

### 1. 调研vue项目开发成移动端实用的框架

UI frameworks for mobile

+ Framework7-Vue - Build full featured iOS & Android apps using Framework7 & Vue.
+ vux - [Chinese] Vue UI Components based on WeUI.
+ vue-onsenui - Mobile app development framework and SDK using HTML5 and JavaScript. Create beautiful and performant cross-platform mobile apps. Based on Web Components, and provides bindings for Angular 1, 2, React and Vue.js.
+ Weex - Weex provides the ability to publish cross platform, so web, Android, and IOS apps can use the same API development functions.
+ weex-eros - [Chinese] Eros is a app solution based on Weex and Vue, which enables you to use API of Vue, simple and quick development of small and medium app.

Set of components for mobile

+ mint-ui - Mobile UI elements for Vue.js.
+ vant - A Vue.js 2.0 Mobile UI From YouZan.
+ cube-ui - A fantastic mobile ui lib implement by Vue.js 2.
+ mand-mobile - A mobile UI toolkit, based on Vue.js 2, designed for financial scenes.

以上几种是[vue资源](https://github.com/vuejs/awesome-vue#mobile)推荐的app开发框架和库，每个都有大量的使用者，根据个人具体情况，笔者选择以下

+ 框架使用[weex](https://weex.incubator.apache.org/zh/guide/introduction.html),[weex-eros](https://bmfe.github.io/eros-docs/#/zh-cn/)和[uni-app](https://uniapp.dcloud.io/README)也是不错选择，目前国内开发环境而言，使用uni-app进行开发的项目较多，因为其内置weex引擎，有专门的开发editor：HBuilder，支持H5+语法，唯一缺点就是只有中文文档，如果在国内开发的话还是建议使用的
+ 库的话，暂定阿里出品的[weex-ui](https://alibaba.github.io/weex-ui/#/cn/weex-ui-report),[bui-weex](http://dev.bingocc.com/buiweex/docs/)和[mint-ui](http://mint-ui.github.io/docs/#/zh-cn2)也是不错的选择，不过个人觉得前两个都是在weex基础上开发的ui库，更适用于原生应用，mint-ui更偏向于手机web端页面开发使用

### 2. 学习框架的使用

1. 依照weex文档[安装开发环境](https://weex.incubator.apache.org/zh/guide/develop/setup-develop-environment.html#%E5%AE%89%E8%A3%85%E4%BE%9D%E8%B5%96),并[创建一个新的app](https://weex.incubator.apache.org/zh/guide/develop/create-a-new-app.html#%E5%88%9D%E5%A7%8B%E5%8C%96)
2. 装备开发环境：

+ iOS环境依赖XCode，安装后请打开XCode以便完成后续的初始化工作。
+ Android环境依赖Android studio, Java JDK 1.8 (Windows需要设置Java的环境路径，教程), Android SDK Platform 26 (通过Android studio安装), Android SDK Build-Tools 26 (通过Android studio安装), Android virtual device (通过Android studio安装)
::: tip 开发环境调查结果
+ [IOS开发环境搭建](https://www.jianshu.com/p/ff29bd79bdba)
+ [IOS从开发完到上AppStore](https://www.cnblogs.com/liuliliuli2017/p/6809360.html)

参考以上文档，大致说明了IOS的开发环境和打包发布过程。

+ [Android studio安装与配置](https://www.cnblogs.com/xiadewang/p/7820377.html)

安卓参考上面文档，按照以上教程可以制作出一个最基本的安卓apk
:::

### 3. 安装安卓模拟器(非必需)

作者虽然安装了[夜神模拟器](https://www.yeshen.com/)，但是基本没用到，只做备用

### 4. 其他安卓开发环境

+ nodeJS（在安装框架之前就应该已经安装了）
+ [JDK安装、java环境配置](https://www.cnblogs.com/renqiqiang/p/6822143.html)，必须正确安装,建议安装完成后重启电脑
+ 根据文档选择性安装[NDK r16](https://developer.android.com/ndk/downloads/older_releases.html)和[Cmake 3.9.0+](https://cmake.org/download/?spm=a2c7j.-zh-guide-develop-integrate-to-android-app.0.0.5a841a8ePGctAs)官网有说明，非必需

::: tip 开发环境踩坑
运行"weex run android"，可能会报出任何意外的错，以下就是几个：

``` text
Error: Command failed: call gradlew.bat clean assembleDebug

FAILURE: Build failed with an exception.

* What went wrong:
Could not determine java version from '12.0.1'.
```

很显然是java JDK的问题，可能是最新版的12.0.1不能识别？，尝试降级看能不能解决问题,降级到1.8.0_211

降级（记得更改环境变量地址）重启后，重新执行"weex run android"，原错误消失，出现新错误

``` text
\ Error: Command failed: call gradlew.bat clean assembleDebug
isLibProject: false, isAppProject: true
weex_plugin: []

FAILURE: Build failed with an exception.

* What went wrong:
A problem occurred configuring project ':app'.
> You have not accepted the license agreements of the following SDK components:
[Android SDK Platform 26, Android SDK Build-Tools 26].
Before building your project, you need to accept the license agreements and complete the installation of the missing components using the Android Studio SDK Manager.
Alternatively, to learn how to transfer the license agreements from one workstation to another, go to http://d.android.com/r/studio-ui/export-licenses.html
```

通过搜索后，发现需要在Android Studio中安装Android SDK Platform 26，虽然报错提示是没有接受license 协议，其实是因为默认安装了Platform 28，而非26，安装后，重新执行"weex run android"，可能又会出现其他错误，比如“not find device”之类的。

总之，执行"weex run android"以后，请耐心等待，出错就根据错误提示解决问题，不得不说，有时候即使报错了，但是还是已经把apk打包好了，报错不一定影响打包文件。可以直接复制apk文件安装到Android virtual device上看到效果

综上所述，要想顺利的使用weex 2.0.0版本开发，**必须的环境和版本**：

+ iOS环境依赖XCode，安装后请打开XCode以便完成后续的初始化工作。
+ Android环境依赖[Android studio](https://www.cnblogs.com/xiadewang/p/7820377.html), [Java JDK](https://www.cnblogs.com/renqiqiang/p/6822143.html) 1.8 (Windows需要设置Java的环境路径), Android SDK Platform 26 (通过Android studio安装，默认会安装最新版【版本不同会报错】，需要我们手动安装：tools-SDK Manager-选择安装), Android SDK Build-Tools 26 (通过Android studio安装,默认一起安装), Android virtual device (通过Android studio安装【未安装会报错】:tools-AVD Manager-Creat new virtual Device-然后就进入选择设备和下载安装过程过程,请选择APIlevel26，与Platform一致)

就个人的环境而言，到现在还是报错如下

```text
Error: Command failed: C:\Users\holy\AppData\Local\Android\Sdk\platform-tools\adb -s emulator-5554 install -r D:\Program Files\WEEX\app\platforms\android\app\build\outputs\apk\weex-app.apk
adb: failed to stat Files\WEEX\app\platforms\android\app\build\outputs\apk\weex-app.apk: No such file or directory

    at ChildProcess.exithandler (child_process.js:289:12)
    at ChildProcess.emit (events.js:182:13)
    at maybeClose (internal/child_process.js:962:16)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:251:5)
```

错误信息中的weex-app.apk实际是存在的，具体为什么网上也没有很好的解释。不过将weex-app.apk安装到虚拟机上是可以执行的。个人也不明白报错的具体原因，留待以后研究或者大神指点
:::
参考[WEEX开发环境爬坑之旅](https://mobilesite.github.io/2017/12/17/weex-enviroment/)

### 4. 利用框架将现有项目开发成一个android app

这一点主要是weex语法的学习，以及与vue语法的不同点的学习，参考文档[在 Weex 中使用 Vue.js](https://weex.apache.org/zh/guide/use-vue-in-weex.html#%E5%9C%A8-weex-%E4%B8%AD%E4%BD%BF%E7%94%A8-vue-js)

因为只是做了一个简单的app，所以并没有异常。以后的实际使用中如果发现异常，在此添加

### 5. 装在自己手机上试用

虚拟机上试用+夜神模拟器上试用+手机上试用

### 6. bug调试

有任何bug的话随时修复