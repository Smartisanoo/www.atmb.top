---
title: Android漫谈
author: 神经元
---

## 引入

大家好，我是神经元，一个Android开发方向的小萌新，今天来和大家聊一聊Android系统相关的一些话题。本人学艺不精，也并非擅长计算机领域的方方面面，有所纰漏在所难免，如果有疑问欢迎大家指正讨论。下面是我的Github ：[singleNeuron](https://github.com/singleNeuron)

### 隐私问题

百度的董事长李彦宏曾经说过这样一句话：“中国人对隐私问题的态度更加开放，也相对来说没那么敏感。如果他们可以用隐私换取便利、安全或者效率。在很多情况下，他们就愿意这么做。”在享受互联网带来的便利的同时，隐私问题也正逐渐受到越来越多普通人的关注。然而，许可协议中晦涩繁杂的法律术语和让人不知所云的技术词汇却让许多普通人望而却步。今天，我将在技术的层面简单的分析一下目前常见的隐私信息及防范方式。

#### MIUI12

相信许多小米手机的用户已经收到了MIUI12的更新推送，在新系统的众多功能和视效之中，我相信“照明弹”一定是吸引了众多媒体和用户关注的一个重要功能。所有安装的应用的唤醒、权限的申请及使用都在这里面显示的让人一目了然，在感叹MIUI团队的别出心裁之时，不少人也对其中应用之乱像深感害怕。

#### 3·15晚会

而在每年的3·15晚会上，用户的隐私问题也被频频提及。就在今年，央视点名报道了数十款SDK（Software Development Kit，即一组提供给其他开发者以简单使用某些功能的工具包，如在App内提供地图显示时可能会使用高德地图SDK，获取应用崩溃统计可能会用到腾讯Bugly平台工具包）存在窃取个人隐私信息的行为。

### 交叉唤醒

Android系统中的交叉唤醒也是让用户头疼的一个重要问题。手机越用越慢，每天有一大堆广告和垃圾资讯推送，明明没开多少应用却内存不足 ……  
由于某些众所周知的原因，Google给Android系统设计的GCM/FCM推送服务在中国大陆完全派不上用场，因此，大多数国产App为了能够及时的收到消息就只能无所不用其及。从注册一大堆广播接收器到常驻后台，一个App启动以后拉起一堆“亲戚”。消息倒是收到了，用户却是苦不堪言。而iOS在系统级推送服务上占据了天然的优势，对于后台的管控也比早期的Android系统强很多，再加上硬件优势，自然给用户带来了苹果手机更好的体验。

## Xposed插件

那么，难道我们用户对于这些厂商的流氓行为就束手无策了吗。当然不是，今天我就要给大家介绍一个Android系统下的“尚方宝剑”——Xposed。下面，我们就通过一些实例来给大家演示他的威力。

### QQ防撤回

而这一部分主题则看似更加的魔法，首先请大家在群聊中随意的发布一些语句（几个人发就够了），然后撤回消息。

## Android系统介绍

说了这么多，接下来就正式进入我们今天演讲的主题。在介绍具体的应用之前，我先来给大家铺垫一些Android系统的知识背景。

### Android的历史及简介

Android，是一个基于Linux内核的开放源代码移动操作系统，由谷歌（Google）成立的开放手持设备联盟持续领导与开发，主要设计用于触摸屏移动设备如智能手机和平板电脑与其他便携式设备。  
Android Inc.于2003年10月由安迪·鲁宾、利奇·米纳尔（Rich Miner）、尼克·席尔斯（Nick Sears）、克里斯·怀特（Chris White）在加州帕罗奥图创建。Android最初由安迪·鲁宾等人开发制作，最初开发这个系统的早期方向是创建一个数字相机的先进操作系统，但是后来发现市场需求不够大，加上智能手机市场快速成长，于是Android成为一款面向智能手机的操作系统。于2005年7月11日Android Inc.被美国科技企业Google收购。  
2007年11月，Google与84家硬件制造商、软件开发商及电信营运商成立开放手持设备联盟来共同研发改良Android，随后，Google以Apache免费开放源代码许可证的授权方式，发布了Android的源代码，开放源代码加速了Android普及，让生产商推出搭载Android的智能手机，Android后来更逐渐拓展到平板电脑及其他领域上。

#### 开源

前面提到，Google以Apache免费开放源代码许可证的授权方式，发布了Android的源代码。这也就是说，世界上任何一个连接到（没有墙的）互联网的人，都可以自由免费的下载Android系统的源代码任意观看并在遵守Apache开源协议的前提下使用。Android的源码托管在[https://android.googlesource.com/](https://android.googlesource.com/)，而在[Github](https://github.com/aosp-mirror) ，[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/)等多地都有镜像提供。而这，也是Android得以不断发展完善壮大的一大重要原因。

### Linux及Android介绍

大部分人可能对Linux这个词语很是陌生，但他离你我并不遥远，我相信你也一定见过不少运行着Linux的设备而没有察觉。Linux是与Windows、macOS并列的一大操作系统，目前主要应用被应用于除了个人计算机之外的大多数应用场景。小到中高端路由器或机顶盒，大到超级计算机，大多都采用了Linux操作系统[^1] ，而Android手机也不例外。  
[^1]:此处的Linux操作系统指使用了Linux内核的操作系统，并非GNU/Linux。

#### Linux文件系统

Linux系统与Windows的一大不同就是其文件系统的设计。下面这部分内容，使用过macOS系统的同学可能相对更容易接受。  
在Linux系统中，没有Windows下C盘、D盘等的划分，取而代之的是一个根目录’/’。而所有的物理硬盘、磁盘分区甚至内存、摄像头等内外部设备都是挂载在根目录及其子目录下的目录或者文件，只要有恰当的权限就可以通过直接读写文件来操作硬件设备。下面，我来给大家具体演示一下。  
通过向`/sys/class/leds`写值控制灯的亮灭。

#### Root权限

在Linux系统中，root是一个对所有文件和目录拥有一切权限的用户。其大致相当于Windows下的管理员账户，但其权限却比管理员账户要大得多。可能有不少人都尝试过在Windows系统中格式化C盘[^2]，结果是显而易见的以失败告终。而面对流氓软件、顽固文件等情况，Windows系统下的管理员的权限也显得心有余而力不足。但是在Linux系统中，root用户的权限却是实打实的最高权限，如果在Linux系统中以root用户执行大名鼎鼎的`rm -rf /*`命令，系统就会不假思索递归遍历根目录并删除掉其下的一切文件，包括操作系统其自身（由于操作系统被加载到了内存中所以在重启前并不会崩溃），其权限之大甚至到了会把部分电脑的BIOS固件（这当然也是挂载在根目录下的一个文件或目录）清空以至于整台电脑彻底报废只能返厂的程度。  
由此可见，对于面向普通个人用户的Android而言，使普通用户接触到root账户的后果将是灾难性的。而且，手机厂商显然也不希望有大量的用户因为把自己手机固件清空了或者其他更糟糕的问题而要求提供保修。所以，绝大部分的普通厂商都是禁止用户接触到root用户的。在没有Bootloader锁（用于阻止刷入不信任的固件）和AVB（Android Verified Boot，用于验证将要引导的固件是否有信任的签名及其完整性）等保证用户不会私自篡改手机固件的早期时代，Android手机的root往往可以通过简单的把可执行文件`su`放入/system/bin中来实现，或者通过一些漏洞来获取临时root权限再进行进一步的操作。而目前，绝大部分root漏洞早已被封堵，Bootloader锁和AVB也会拒绝刷入和引导未验证经厂商签名的系统固件。绝大部分root及后续操作实际上都只能在小米、一加等少数愿意开放解锁Bootloader的厂商（甚至还在解锁后提供保修）的设备上实现。  
[^2]:此处C盘代指当前运行的Windows操作系统所在的分区。

#### Android结构

![由Google LLC - https://developer.android.com/guide/platform/index.html，CC BY 2.5，https://commons.wikimedia.org/w/index.php?curid=66319092](~./1.png)

Android系统的内核和部分底层库由C和C++编写，而绝大部分的系统框架及App由Java 编写。而这中间连接Native和Java的便是Dalvik/ART虚拟机。每一个Android系统上的App都运行在一个由Zygote孵化出的独立的虚拟机中。  
在Android App的开发和发布的过程中，由Java[^3]编写的App最终被编译成dalvik字节码并打包进apk文件提供给用户下载。而在运行时由Dalvik或ART虚拟机负责解释执行。  
而在Android系统的发展过程中，Android上的虚拟机也经历了数次大大小小的变动，比如在Android 5.0上以ART代替了Dalvik，在更高版本中会在手机空闲时自动将smali编译到二进制程序以加快下次运行时的速度。  
[^3]:实际上为主要是Java和Kotlin的JVM兼容语言，下文不再另行说明。

### Application生命周期

#### Android四大组件

Android系统中主要由四大组件构成：Activity、Service、Broadcast Receiver、Content Provider。  
Activity的中文名称是活动，大部分直接显示在手机屏幕上与用户交互的部分都是由activity来完成的，比如一个聊天窗口、一个浏览器页面等等。
Service则是服务，用于在后台下载文件，或者播放音乐等功能。
Broadcast Receiver是广播接收器，可以接受系统广播或其他Android应用的广播。例如在app没有运行的时候监听手机电量、网络状态的变化，或者其他app的消息等等。  
而Content Provider则是内容提供程序，主要用于向其他应用提供信息的读写。例如普通应用对手机联系人的读取和写入，就是通过和联系人这个系统应用的内容提供程序组件来完成的。  
由此可见，Service和Broadcast Receiver是国内流氓App泛滥的重灾区。其中Service用于常驻后台与推送服务器等保持连接。而为了常驻后台，0高度的状态栏通知、一个像素大小的悬浮窗等匪夷所思方法都是国内大厂App真实使用过的极端手段。  
Broadcast Receiver则是用于在Service被杀后快速启动。当系统网络状态更改时、开始充电时、有新软件包安装时，系统都会发出广播，而各流氓App就会在接收到广播后快速重启自己的后台服务。而在一个流氓app被用户打开后，同样也会发送广播通知其他的一丘之貉。  

#### 进程的强杀

##### 绕过强杀的N种漏洞

而在防止自身被杀死这方面，各大流氓也是花样百出，由于此部分与接下来的内容关联不大且技术层次较深，有兴趣的同学可以自行阅读下方的链接来了解今年最新的防止被杀“绝招”。  
[Android 黑科技保活实现原理揭秘](https://mp.weixin.qq.com/s/s7kYkHkbImjALuHKa7z30Q)

### ADB介绍

#### 是什么

ADB的全称是Android 调试桥（Android Debug Bridge），其向开发者提供了一个可以执行比普通用户更高权限的操作的通信通道。例如安装、卸载、冻结App，复制文件，更改屏幕分辨率，查看系统内安装的软件包及其相关信息，授予或拒绝App权限，进行屏幕截图或录像等功能。  
因为ADB拥有着比普通App更高的权限，因此可以被一些系统管理软件用来执行例如冻结其他应用，管理软件权限等操作。

#### 有什么隐患

由于ADB更高的操作权限，因此被陌生人连接到自己手机的ADB以后，可能造成相当大的安全隐患，如安装病毒软件，窃取联系人或相册等隐私信息等。  
![](~./2.png)  
所幸，在没有进行什么稀奇古怪的操作之前，ADB只能通过USB线缆进行访问，而且需要在设置中打开开发者选项及其中的USB调试。而在高版本的Android系统中，即使打开了USB调试，在陌生设备连接时系统也会二次弹框确认。MIUI等国内系统也对ADB权限进行了细分并给出了更为详尽的提示和警告。目前来看，绝大部分普通用户都是足够安全的。  
因此，在使用公共设备，如机场火车站的充电桩、网吧里的计算机时，或在计算机上安装不信任的软件时，请务必要警惕任何不明来源的引导你打开USB调试的行为，请不要在不明晰将要进行什么操作的情况下允许USB调试。  
![](~./3.png)

### Android系统中可能被利用的隐私信息

具体来说，用户易被滥用的个人隐私信息一般包括IMEI、WiFi网卡的Mac地址等用户标识符及通讯录，短信等个人数据两大部分。  
IMEI是国际移动设备识别码，可以理解为每一个手机的基带模块的唯一标识符；而Mac地址则对应的是WiFi网卡的唯一标识符。  
IMEI主要被滥用于用于跨App和卸载重装后的设备跟踪。即，如果两个不同的App获取到了相同的IMEI，则可以认为其二运行在同一个设备上，进而将二者获取到的用户习惯和行为等合并进行进一步的分析。比如当你打开百度App搜索了一个喜爱的衣服以后，后台算法就有可能针对性的给你的淘宝首页推荐更多类似的裙子或给出符合预测的你的心理预期价位的折扣以吸引你购买。对于绝大部分完全不需要拨打电话的App来说，申请一个莫名其妙的电话权限就是为了获取IMEI。  
WiFi的Mac地址则可用于用户的行动路线跟踪，当你在商场连接上了免费的WiFi之后，后台就有可能记录下你的Mac地址，通过大数据的交叉比对（别忘了你手机上的App也是可以申请权限读取Mac地址的）锁定到个人设备，从而将你的行动路线也纳入到“天网”的监控之下。  
至于联系人和短信的滥用，可能是通过对通讯录和短信的分析进一步加大后台大数据对你和你的社交关系的掌控程度。更进一步甚至可以给你的亲友定向发送勒索短信或者拦截短信验证码窃取游戏或银行账户。

### Android权限系统介绍

Android系统中的权限系统比较复杂。一般来说，在Android 6.0以前，App会在安装的时候就被赋予申请的所有权限，而在Android 6.0以后，App则需要在运行时动态的申请所需要的权限，而我们也可以在系统设置里动态的管理这些权限。  
有些人可能会说，如果软件想要读取隐私信息的话，直接拒绝不就好了。可是，面对那些不给权限就拒绝运行而又非用不可的程序来说，乖乖交出数据似乎也是无奈之举。  
然而，在Android系统中，还隐藏着另一套权限管理系统，也就是AppOps。这套系统与平时设置中见到的表面上的那一套之间相互独立。而且，在App使用相应权限的时候，会分别向这两套系统发起两次验证。不同之处在于，当表面上设置里的权限系统拒绝时，系统会直接抛出异常，这些流氓App也就知道了我们拒绝了他的权限申请，开始死皮赖脸的弹窗请我们给他程序运行所必须（个头）的权限，否则就拒绝启动。但是，当我们在设置中授权而在AppOps里拒绝的话，系统只会悄悄的给App返回一个空数据，这样就能达到瞒天过海的目的。  
但是，既然AppOps是一套刻意隐藏起来的系统，平时也就没有那么容易访问到。一般对其的访问需要打开隐藏的API或者通过adb shell来进行。例如在前文提到的ADB中，就可以通过ADB提供的Unix Shell执行“ops”命令来访问和管理App Ops。  
对于普通用户来说，命令行界面可谓是相当的不友好，而且小白也很容易在这一系列复杂的操作中迷失自我。那么，有没有什么办法可以让我们更加简便的管理AppOps呢？我们后文揭晓。  
更多资料：  
[https://appops.rikka.app/zh-hans/guide/#%E4%BB%80%E4%B9%88%E6%98%AF-android-%E7%B3%BB%E7%BB%9F%E4%B8%AD%E7%9A%84-appops](https://appops.rikka.app/zh-hans/guide/#%E4%BB%80%E4%B9%88%E6%98%AF-android-%E7%B3%BB%E7%BB%9F%E4%B8%AD%E7%9A%84-appops)  
[https://developer.android.com/reference/android/app/AppOpsManager](https://developer.android.com/reference/android/app/AppOpsManager)  
[https://blog.csdn.net/zhongfan520520/article/details/80939991](https://blog.csdn.net/zhongfan520520/article/details/80939991)  
[https://blog.csdn.net/lewif/article/details/49124757#%E8%AF%A6%E7%BB%86%E5%88%86%E6%9E%90%E6%9D%83%E9%99%90%E7%AE%A1%E7%90%86%E7%9A%84%E8%A7%A6%E5%8F%91](https://blog.csdn.net/lewif/article/details/49124757#%E8%AF%A6%E7%BB%86%E5%88%86%E6%9E%90%E6%9D%83%E9%99%90%E7%AE%A1%E7%90%86%E7%9A%84%E8%A7%A6%E5%8F%91)

### Android的改进

而面对前述问题，Android系统也在逐步的改进，针对毒瘤泛滥的重灾区，主要有以下几个方面。

#### 后台服务限制

从Android O开始，只有有常驻通知、有正在显示的Activity及关联到少部分特殊服务的服务（如输入法、壁纸等）可以常驻后台，其余服务将在数分钟后被系统停止。

#### 广播限制

从Android O开始，将禁止普通App静态注册如网络状态改变，开始充电等没有具体App作为目标的隐式广播接收器。也就是说，在App停止运行后，此类隐式广播将不会唤醒他们。

#### 限制反射

从Android P开始，Android限制了使用反射调用系统隐藏API的行为，从而防止某些App利用Java的反射（指程序可以在运行时动态的访问或修改自身）的特性来操作本不该由普通App访问到的API并做出无法预料的行为。

#### IMEI和Mac

在Android 10及更高的版本上，Android系统将不允许以此版本为目标的普通App获取IMEI及Mac地址等唯一标识符，如果强行获取则会抛出异常。而对于目标版本低于Android 10的普通应用，尝试获取IMEI时将会返回空字段。而在连接陌生的WiFi网路上时，Android系统也会默认使用随机生成的Mac地址代替设备网卡的地址。

#### 待机应用

在Android P中，Google引入了应用待机群组这一新的功能。在P及更高版本上，系统会按照用户的使用频率对App进行分组，并对不同使用频率的App施加不同的限制。例如，你每天都会看的QQ或者微信，就可以以更频繁的间隔检查消息或者接收服务器的推送。而极少打开的应用，则可能会被严格限制其活动。

#### 国内的改变

虽然Google在高版本上施加了一系列的限制，但是如果App不更新自己的目标版本，岂不是徒劳无用。实际上，在新版本的Android系统发布一年后，所有上传到Google Play的应用就必须将其目标SDK版本升级到上一年新发布的版本，否则将不予上架。而国内也在绿色守护作者Oasis Feng的大力奔波之下，由统一推送联盟发起了《中国绿色App公约》，并联合各大软硬件厂商发起联合行动，拒绝低目标版本的App上架国内的应用商店。  
而国内系统的改动则更加的激进，目前绝大部分主流手机操作系统已经无法在目标应用停止运行的时候获取到他们的内容提供程序。而对于交叉唤醒、常驻后台等的限制也比Android系统作出限制要早上很多。

#### 总结

由此可以看出，在最新的Android 10的操作系统上，手机的使用环境已经有了极为明显的改观，几乎不需要任何的第三方后台管理软件即可保持手机干净的后台和较高的运行速度。但是受限于后台机制的区别和硬件水平的参差不齐，想要让所有手机都有像iOS一样的流畅程度，还是一个十分遥远和艰巨的目标。

## 应用介绍

上面说了这么多理论，下面就该要介绍些具体的App来给大家使用了。

### Magisk

Magisk是一个开源的自定义工具套组。主要功能有root权限的获取与管理以及最重要的——在不修改闪存上的实际文件的情况下提供一个修改system分区的接口。也就是说，他可以任意的往系统里挂载或替换文件和目录而不产生不可撤销的影响，也不会对实际存储于手机中的系统固件[^4]做出任何实际修改，其将要修改的内容实际存储于/data目录下并于手机启动时替换。因此，Magisk也就绕过了AVB等系统启动时的校验过程。  
[^4]:仅指`/system`和`/vendor`分区而非包括引导程序在内的所有固件

### Riru

而riru则是一个Rikka开发的magisk模块，其主要功能是通过替换`libmemtrack`库来注入Zygote孵化器。前面我们说过，所有的App和大部分系统功能都实际运行于Zyote孵化出来的Dalvik/ART虚拟机之上。因此，通过注入Zygote，也就能实际操控虚拟机的创建过程和行为，为后续的操作提供了可能。

### Xposed

#### 用途

最后终于到了我们今天的重头戏——Xposed，Xposed最终提供了对App的注入能力。他可以在不修改App文件的情况下替换App的图片、字符串等资源，也可以修改或替换其软件的执行逻辑或者获取运行中的各种信息。例如我刚才展示的QQ消息防撤回或者主题美化等功能。

#### 介绍

Xposed是由rovo89在2012年初次发布的一个在Java层面上提供了Method粒度的hook框架。简而言之，就是他可以在不修改安装包文件的情况下，在任意App的Java方法之前或者之后插入自定义的代码，并修改或替换代码的运行逻辑及其返回值。

#### 实现

由于Xposed 的源代码在Github上开源，再加上原作者rovo89自Android O之后便没有继续维护更新。因此，Xposed的含义也从一个具体的框架逐渐演变成了一系列实现了Xposed Bridge API的框架或App的总称。这些实现可以是一个通过各种方法修改系统的框架，也可以是一个提供了Xposed运行环境的虚拟机或宿主App，甚至其某些实现直接修改了App以引入Xposed类。伴随着开源社区的蓬勃发展，仅Hook内核就有十余种之多，而其实现更是琳琅满目。需要注意的是，这些内核和实现仅为不同的实现原理，对于Xposed模块的开发者和用户来说不存在显著的差异。  
目前Xposed的主流实现EdXposed基于riru，通过加载YAHFA/SandHook框架以实现Xposed的功能。在这三级结构中，Magisk通过替换系统文件而使riru得以将自己的运行库逻辑注入Zygote，而riru又加载了EdXposed从而使得每一个App都得以在EdXposed的掌控之下运行。而Xposed框架的具体实现原理过于复杂，如有兴趣请自行阅读下面三个主流框架实现原理的简单介绍。  
[YAHFA](http://rk700.github.io/2017/03/30/YAHFA-introduction/)  
[SandHook](https://blog.csdn.net/ganyao939543405/article/details/86661040)  
[epic](https://weishu.me/2017/11/23/dexposed-on-art/)  
![常见的Hook内核](~./4.png)  
![目前主流的Xposed实现及对比 CC BY-NC-SA 3.0 Unported by MlgmXyysd](~./5.png)  
由于不同的手机及系统所适用的Xposed实现可能有着天壤之别，在此就不再赘述如何在手机上安装Xposed框架，有兴趣的同学可以前往自己手机的论坛寻找教程或发帖询问。

#### 模块

##### 应用变量

而在众多的Xposed插件中，与隐私防护关系最大的一个就是应用变量了。他可以通过hook对应的系统API来修改App读取到的手机型号、IMEI、Mac地址等信息为自定义的值，从而达到隐藏真实信息，保护隐私的目的。

##### 去你大爷的内置浏览器

嗯...乍一听它的名字似乎容易弄得大家一头雾水，那就首先讲一下这个模块的作用，它可以接管QQ等App打开浏览器的事件，使你可以在聊天页面点击链接直接打开浏览器（当然也可以重定向到能够打开相应链接的应用），而非App的内置浏览器，应用由xloger和oott123共同开发。（来自酷安）给大家列举一下应用场景：当你的朋友在QQ上分享给你一首来自QQ音乐的歌曲链接，你打开链接后听了感觉很好听，想要收藏/看评论，却还要再点击「打开」再转到应用内操作；朋友给了你一个外文网站/珍贵网站，却囿于QQ内置浏览器的能力而不能进行收藏/翻译等操作...这时候它的作用就体现了出来，简化了中间繁琐的操作而可以直接打开「专业」的浏览器或者打开对应应用。虽然QQ在内置浏览器里也提供了在浏览器内打开的功能，但若频繁进行此类操作便显得有些麻烦，而它也可以起到一劳永逸的作用...当然还可以有其他用途，等着你来发掘。  
目前该应用支持QQ，QQ轻聊版，QQ国际版，TIM，百度贴吧，微博，微信。  

##### Thanox

Thanox这个模块很有意思，在模块仓库里的简介是”I am thanos”，而thanos也可以指灭霸，模块本身也有与其名字相匹配的能力。Thanox是一个系统级模块，功能强大：有效管理应用在后台的运行；解决一些ROM无法通过划去任务卡片从而强制停止程序运行的问题 ；“照明弹”权限管理，监视应用权限申请记录；“隐匿”个人敏感信息以及一些其他功能（大多是ROM本身无法实现或比定制ROM超前的）。无论是对于MIUI等高度定制化的国产ROM还是原生ROM都可以做一个功能上的补全，从而更好地管理你的手机与你的隐私。  
![这是个锤子问题](~./6.jpg)

### 后台管理

#### 绿色守护

绿色守护是一个早在Android4.x时代就出现的可以依托无障碍服务/root/xposed运行的老牌后台管理软件，旨在限制部分Android第三方软件在后台运行，以达到省电和优化系统运行的作用。

#### 冰箱

而冰箱则是一个在策略上更为激进的后台管理软件，他会直接将用户选择的软件彻底冻结，在用户打开时再解冻并在运行结束后再次冻结。被冻结的软件将无法以任何方式运行，其图标也会在启动器中消失，对于用户来说与卸载无异，但是能够在需要的时候解冻并再次运行，无需下载也不会丢失数据。这些步骤虽然也可以很简单的通过前面提过的ADB来完成，但是冰箱无疑提供了一个友好的用户界面，大大简化了操作流程。

### 神奇的Rikka

Rikka，用爱与魔法创造 Android 应用。因为屡次实现着Android系统会在未来实现的功能而被怀疑是从未来穿越回来的人……不好意思跑题了。  
[Rikka](https://docs.google.com/document/d/e/2PACX-1vQPF8DTZ2ZoI8uoXRPD8JdCMU6mQIALMnKJHRmCt2gjj6SK6Fj4ZqsivPPt0YcQ7XM207ON9V-HymJ5/pub)

#### 存储重定向

你是否为手机存储卡[^5]内的一团糟而苦恼过？存储卡内堆积了各种不知谁创建的奇怪文件夹，而自己放进去的东西却往往要找上大半天才能找到。存储重定向就是为了解决这一问题而诞生的。他可以把App对存储卡的所有读写重定向到软件私有目录下面，而在软件卸载或清除数据后就会随之删除，从而保持了存储卡内的干净整洁。  
[^5]:指/sdcard分区，不一定为物理sd卡

#### App Ops

而App Ops就是为了便捷管理前面说过的AppOps的一个图形化应用程序。他将晦涩且难以直接接触到的ops命令转变成了简洁友好的图形界面，极大的方便了用户的操作。

## 和标题完全无关的闲聊话题

### 内存与存储的区别

很多人都会将内存与存储的区别混为一谈，甚至出现了“运存”之类的奇怪称呼。简单来说，内存就是程序执行时存放其自身和数据的地方，在断电后就会丢失。而存储则存放了大量并非随时需要的数据且会在断电后一段时间（闪存通常为几年到几十年）内保持稳定。  
而至于容量上，二者其实有很大的重叠区域。在二十年前，U盘容量普遍只有512M~1G大小。而现在最大的单条服务器内存已经达到了256Gib之大，面向个人的Mac Pro也拥有最大1.5T的内存规格。因此，见到512G就认为是存储而非内存的行为是十分愚蠢的。

### 剩余内存越大越好吗

当然不是，内存的用途就是存储需要运行的程序的数据，如果大量内存长时间空闲，那你还要那么大内存干什么。对于没有常驻后台等恶意行为或者内存泄漏的情况，内存使用量越高，系统反而会越流畅。因为绝大部分的操作系统都会将经常访问的数据或可能将要访问的数据缓存在内存中，从而使得下一次访问可以直接从内存中读取而无需等待缓慢的硬盘响应。在正常情况下，操作系统都会自动选择合适的内存调度策略，从而在保证需要的任务有足够内存的前提下尽可能多的提升运行速度和减少存储访问。而内存占用越大越卡，实际上是早期流氓软件横行之时，大量无用App强行占据在内存中，不肯被操作系统释放，而导致需要的程序无法及时分配到足够的内存导致的。在前面介绍过的那些措施之下，流氓软件的行为基本上已经被压制，较高的内存占用率实际上是有利于提升系统流畅程度的。反而如果每次操作都要等包括SSD等闪存在内的外部存储设备响应（内存和外部存储设备的响应时间通常差距在两个数量级左右），才会卡的让你怀疑人生。

### 为什么iOS比安卓流畅

关于这部分内容前面已经说过很多了。手机用久了卡顿也和新硬件性能的提升和软件性能需求的提升有很大关系。按照摩尔定律，每过18个月同价位手机性能就会翻一倍，而App的性能需求也会大致贴合于硬件的提升。因此，从这个角度来看，使用一年半以后的手机使用最新的App只有刚买时一半的流畅也是说的过去的正常现象。而对于大部分设备来说，想要彻底的识别和清理长年累月运行留下的垃圾文件和缓存也是技术上的一大难点 。
Android和iOS一大区别就是，iOS系统的硬件设备是可控的。也就是说，苹果和iOS开发者完全可以根据不同的iPhone或者iPad进行优化，从而使得每个设备都能得到更适合的二进制文件来运行。而Android这边，由于硬件设备和处理器架构的高度碎片化，想要让一份二进制文件能够在所有设备上都运行是完全不切实际的。因此，Android只能使用解释执行的方法，由Dalvik虚拟机对smali中间代码进行解释翻译后再交给CPU执行，而这一步就会极大的影响Android上App的性能。当然，随着Android的不断完善，Google也采用了包括前面介绍过的AOT和JIT在内的多种方式在性能空间和兼容性上探索着合适的平衡。  
另外，每年苹果新发布的处理器性能都领先高通和（这两年新冒出来的）华为的同年代旗舰水平半年以上，存储的读写速度也远高于Android的中上水平。因此想要你花了一两千块钱买的中端Android手机和最新的iPhone一样流畅，本来就是个不现实的事。  
![](~./7.jpg)