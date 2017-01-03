# Carthage的一般使用

> 项目源址： https://github.com/Carthage/Carthage

> 在我尝试使用Carthage时，折腾了比较久，现在整理出最简单的方法，献给使用Xcode+Swift+Carthage开发的新手朋友，希望能帮助你们！如果老手们觉得小弟文章哪里有问题，请一定指出，谢谢！

## ＝＝安装＝＝
* 安装方式一：下载pkg，https://github.com/Carthage/Carthage/releases
* 安装方式二：使用 Homebrew 进行安装：
```
brew update
brew install carthage
```

## ＝＝使用＝＝

![1.png](http://upload-images.jianshu.io/upload_images/1698649-42258c7d1c7a094a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 第一步，如上图，在工程根目录下，新建一个无后缀的Cartfile文件，Cartfile.resolved和Carthage文件夹是执行下面第二步操作后自动生成的，不需要手动建立。Cartfile格式说明:

![2.png](http://upload-images.jianshu.io/upload_images/1698649-e932b4e9122783c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 第二步，打开命令终端，cd到所在项目目录，执行：

![3.png](http://upload-images.jianshu.io/upload_images/1698649-6ed85e4d9d2c430b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

会自动checkout所有依赖的git仓库，并生成framework，如果不指定平台，则会生成依赖自身支持的所有平台的文件。
> 如遇到问题，可尝试使用：
```
carthage update --platform iOS --no-use-binaries
```

* 第三步，引入Framework

把生成的.framework文件（在Carthage/Build目录中）拖到 Targets -> General -> Linked Frameworks and Libraries 里。【OSX APP为 Embedded Binaries 】
> 注意： 拖拽后不要选择拷贝

如果是iOS，还需要在 Targets -> Build Phases -> “+” (New Run Script Phase”) Shell的下面一行填入：
```
/usr/local/bin/carthage copy-frameworks
```
并在 “Input Files” 选项里添加 framework 路径，如：
```
$(SRCROOT)/Carthage/Build/iOS/Localize_Swift.framework
```
如图：

![4.png](http://upload-images.jianshu.io/upload_images/1698649-ca47ddfee704b266.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 这个脚本是针对由 universal binaries 引起的 App Store submission bug 的一种变通方案。

**最后command+B编译一下，并在代码里import xxx.framework试试吧！**


[本文Github地址>>>](https://github.com/pangpingfei/CodingLife/blob/master/Carthage.md)