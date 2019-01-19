# 病毒木马防御与分析

### [病毒包和工具包下载:Github](https://github.com/CasterWx/Killing-Of-Actual-Combat)

## 目录

* [一.前言](#qy)
* [二.建立对手动查杀病毒技术的正确认识](#er)
    * [1.病毒分析方法](#er1)
    * [2.病毒查杀步骤](#er2)
    * [3.必备知识](#er3)
      * [1) 熟悉windows系统进程](#er31)
      * [2) 熟悉常见端口与进程对应关系](#er32)
      * [3) 熟悉windows自带系统服务](#er33)
      * [4) 熟悉注册表启动项位置](#er34) 
* [三.详解Windows随机启动项目——注册表](#sa) 
* [四.详解Windows随机启动项目——系统服务](#si)

## 实战

| [总纲](https://github.com/CasterWx/Killing-Of-Actual-Combat/blob/master/README.md) | [熊猫烧香分析](https://github.com/CasterWx/Killing-Of-Actual-Combat/blob/master/XMSX.md) | [txt病毒分析](https://github.com/CasterWx/Killing-Of-Actual-Combat/blob/master/TXT.md) |
| --------- | --------- | --------- |


## <span id="qy">一.前言</span>

《病毒木马防御与分析》系列以真实的病毒木马（或恶意程序）为研究对象，通过现有的技术手段对其分析，总结出它的恶意行为，进而制定出相应的应对方法，对其彻底查杀。当然，因为我个人水平的有限，查杀分析的病毒可能不是过于高端复杂，但对你认识病毒工作原理还是会很有帮助的，甚至最后你也可以利用c语言实现一个简单的病毒程序。

## <span id="er">二.建立对手动查杀病毒技术的正确认识</span>

### <span id="er1">1.病毒分析方法</span>

一般来说，除非是感染型病毒，否则是不需要对病毒进行逆向分析的，只需要对病毒进行行为分析就可以编写专杀工具。而如果是感染型病毒，由于需要修复被病毒感染的文件，那么就不能仅仅简单地分析病毒的行为，而必须对病毒进行逆向分析，从而修复被病毒所感染的文件。因此，实际中的分析方法有以下两种：

1. 行为分析。恶意程序为了达到目的，都有自己的一些特殊的行为，这些特殊的行为是正常的应用程序所没有的。比如把自己复制到系统目录下，或把自己添加进启动项，或把自己的某个DLL文件注入到其它进程中去。

2. 逆向分析。当恶意程序感染了可执行文件之后，所感染的内容是无法通过行为监控工具发现的。而病毒对可执行文件的感染，有可能是通过PE文件结构中的节与节之间的缝隙来存放病毒代码，也可能是添加一个新节来存放病毒代码。无论是哪种方式，都需要通过逆向的手段进行分析。

### <span id="er2">2.病毒查杀步骤</span>

1. 查内存，排查可疑进程，将病毒从内存中干掉

2. 查启动项，删除病毒启动项

3. 通过启动项判断病毒所在位置，并从根本上删除病毒

4. 修复系统

### <span id="er3">3.必备知识</span>

##### <span id="er31">1) 熟悉windows系统进程</span>

##### <span id="er32">2) 熟悉常见端口与进程对应关系</span>

##### <span id="er33">3) 熟悉windows自带系统服务</span>

* 系统随机启劢服务查看：msconfig/services.msc
* SvcHost.exe宿主进程对应的多项服务
* windows隐藏服务管理工具：SDCT

##### <span id="er34">4) 熟悉注册表启动项位置</span>

> 随机启动项目在注册表中的位置
* HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run

* HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

* HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon

* HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options

## <span id="sa">三.详解Windows随机启动项目——注册表</span>

注册表是Windows中的一个重要的数据库，用于存储系统和应用程序的设置信息。早在很多年前的Windows系统中注册表就已经出现。随后推出的Windows NT是第一个从系统级别广泛使用注册表的操作系统。但是，从Microsoft Windows 95操作系统开始，注册表才真正成为Windows用户经常接触的内容，并在其后的操作系统中继续沿用至今。

<font color="red">注册表是一个重要的数据库，里面存储的是本系统中的所有配置，如开机启动项，桌面背景，右键菜单，图标，系统更新，系统中一些按键的响应，甚至还有系统管理员的信息。所以修改注册表是一个病毒可以控制影响我们系统一个很直接的方式。比如在c语言中就提供了可以直接操作Windows注册表的接口函数。</font>

```c
// 打开注册表
LONG WINAPI RegCreateKey(
_In_ HKEY hKey,
_In_opt_ LPCTSTR lpSubKey,
_Out_ PHKEY phkResult
);
```

```c
// 读写注册表
LONG RegSetValueEx(
    HKEY hKey,
    LPCTSTR lpValueName,
    DWORD Reserved,
    DWORD dwType,
    CONST BYTE *lpData,
    DWORD cbData
);
```

> 此处在病毒编程实战中再做详细阐述

开机自启动的实现方法就是通过注册表实现，在注册表中有固定的开机自启程序设置位置。

在命令提示符中输入`regedit`打开注册表看看能不能在下面五个开机自启项中找到你本机的开机自启软件吧！

> 一个软件出现在五个启动项一个中即可

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run;
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Runonce;
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run;
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce;
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx
```

![img1](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/1.jpg)

## <span id="si">四.详解Windows随机启动项目——系统服务</span>

一个病毒往往会以系统服务的形式存在，也就是说他的图标不会出现在你的桌面任务栏，不会像在我们初学编程时程序运行时的一个小黑框展现给用户。

系统服务是指执行指定系统功能的程序、例程或进程，以便支持其他程序，尤其是底层程序。通过网络提供服务时，服务可以在Active Directory（活动目录）中发布，从而促进了以服务为中心的管理和使用。

在`运行`中输入`msconfig`打开系统配置

![2](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/2.png)

![3](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/3.png)

在这里我们可以看到有`服务`和`启动`，`启动`中即是之前我们所说在注册表中的开机自启动项了，不过很多病毒都有在系统配置启动中隐藏自己的功能，所以我们还是要会在注册表中查找。

我们选择`隐藏所以Microsoft服务`便可看服务列表大量服务被隐藏，只剩下非Microsoft服务，在这些中就可以查找异常服务进行查杀了。

除了这种查看服务的方式，我们还有一种更加详细的方法，通过`services.msc`查看。

在`运行`中输入`services.msc`打开服务。

![4](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/4.png)

在这里我们可以看到大量的系统服务，比如有WLAN服务(连不上WIFI可以考虑重新启动这个服务)，Windows更新服务(可以考虑禁用)。通过查看描述，我们就可以发现一些异常的服务了，比如灰鸽子远控，在其服务描述中很明显的写出了是灰鸽子。

![5](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/5.png)

在Windows下病毒也可以对自身服务进行隐藏，这类病毒就需要一些第三方工具了，利用SDCT工具可以查看到本机所有服务的信息，包括隐藏与未隐藏，启动与未启动。

![5](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/7.png)

> SDCT工具还有之后的工具都可以在我的Github仓库中找到

<font color="red">此外，病毒进程可能利用svcHost.exe宿主进程，此时在Windows任务管理器中病毒进程显示的就是svcHost.exe名称了，这种情况下我们需要利用一条命令来查看SvcHost.exe下有哪些进程。</font>

命令: `tasklist /svc`

![6](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/6.png)

<font color="red">可以看到svchost.exe会存在多个进程，而每个进程下还有多个依赖于此进程的服务。</font>