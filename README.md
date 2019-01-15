# 病毒木马防御与分析

### [病毒包和工具包下载:Github](https://github.com/CasterWx/Killing-Of-Actual-Combat)

| [总纲](https://github.com/CasterWx/Killing-Of-Actual-Combat/blob/master/README.md) | [熊猫烧香](https://github.com/CasterWx/Killing-Of-Actual-Combat/blob/master/XMSX.md) |
| --------- | --------- |

<ul>
<li><a href="#qy">&#x4E00;.&#x524D;&#x8A00;</a></li>
<li><a href="#er">&#x4E8C;.&#x5EFA;&#x7ACB;&#x5BF9;&#x624B;&#x52A8;&#x67E5;&#x6740;&#x75C5;&#x6BD2;&#x6280;&#x672F;&#x7684;&#x6B63;&#x786E;&#x8BA4;&#x8BC6;</a>
<ul>
<li><a href="#er1">1.&#x75C5;&#x6BD2;&#x5206;&#x6790;&#x65B9;&#x6CD5;</a></li>
<li><a href="#er2">2.&#x75C5;&#x6BD2;&#x67E5;&#x6740;&#x6B65;&#x9AA4;</a></li>
<li><a href="#er3">3.&#x5FC5;&#x5907;&#x77E5;&#x8BC6;</a><br>
* <a href="#er31">1) &#x719F;&#x6089;windows&#x7CFB;&#x7EDF;&#x8FDB;&#x7A0B;</a><br>
* <a href="#er32">2) &#x719F;&#x6089;&#x5E38;&#x89C1;&#x7AEF;&#x53E3;&#x4E0E;&#x8FDB;&#x7A0B;&#x5BF9;&#x5E94;&#x5173;&#x7CFB;</a><br>
* <a href="#er33">3) &#x719F;&#x6089;windows&#x81EA;&#x5E26;&#x7CFB;&#x7EDF;&#x670D;&#x52A1;</a><br>
* <a href="#er34">4) &#x719F;&#x6089;&#x6CE8;&#x518C;&#x8868;&#x542F;&#x52A8;&#x9879;&#x4F4D;&#x7F6E;</a></li>
</ul>
</li>
<li><a href="#sa">&#x4E09;.&#x8BE6;&#x89E3;Windows&#x968F;&#x673A;&#x542F;&#x52A8;&#x9879;&#x76EE;&#x2014;&#x2014;&#x6CE8;&#x518C;&#x8868;</a></li>
<li><a href="#si">&#x56DB;.&#x8BE6;&#x89E3;Windows&#x968F;&#x673A;&#x542F;&#x52A8;&#x9879;&#x76EE;&#x2014;&#x2014;&#x7CFB;&#x7EDF;&#x670D;&#x52A1;</a></li>
<li><a href="#wu">&#x4E94;.&#x624B;&#x52A8;&#x67E5;&#x6740;&#x75C5;&#x6BD2;&#x5B9E;&#x6218;&#x2014;&#x2014;&#x718A;&#x732B;&#x70E7;&#x9999;&#x75C5;&#x6BD2;</a>
<ul>
<li><a href="#wu0">0. &#x75C5;&#x6BD2;&#x5206;&#x6790;</a><br>
* <a href="#wu01">1).&#x4E2D;&#x6BD2;&#x75C7;&#x72B6;</a><br>
* <a href="#wu02">2).&#x75C5;&#x6BD2;&#x7279;&#x5F81;</a><br>
* <a href="#wu03">3).&#x53D1;&#x4F5C;&#x75C7;&#x72B6;</a></li>
<li><a href="#wu1">1. &#x67E5;&#x5185;&#x5B58;&#xFF0C;&#x6392;&#x67E5;&#x53EF;&#x7591;&#x8FDB;&#x7A0B;&#xFF0C;&#x5C06;&#x75C5;&#x6BD2;&#x4ECE;&#x5185;&#x5B58;&#x4E2D;&#x5E72;&#x6389;</a></li>
<li><a href="#wu2">2. &#x67E5;&#x542F;&#x52A8;&#x9879;&#xFF0C;&#x5220;&#x9664;&#x75C5;&#x6BD2;&#x542F;&#x52A8;&#x9879;</a></li>
<li><a href="#wu3">3. &#x901A;&#x8FC7;&#x542F;&#x52A8;&#x9879;&#x5224;&#x65AD;&#x75C5;&#x6BD2;&#x6240;&#x5728;&#x4F4D;&#x7F6E;&#xFF0C;&#x5E76;&#x4ECE;&#x6839;&#x672C;&#x4E0A;&#x5220;&#x9664;&#x75C5;&#x6BD2;</a></li>
<li><a href="#wu4">4. &#x4FEE;&#x590D;&#x7CFB;&#x7EDF;</a></li>
</ul>
</li>
</ul>
</li>
</ul>

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

## <span id="wu">五.手动查杀病毒实战——熊猫烧香病毒</span>

> 如果像自己实践记得在虚拟机下！
> 病毒包可以在Github仓库找到

### <span id="wu0">0. 病毒分析</span>

病毒名称: `武汉男生`，又名`熊猫烧香病毒`。"Worm.WhBoy.h"

###### <span id="wu01">1).中毒症状</span>
  
* 拷贝自身到所有驱动器根目录，命名为Setup.exe，并生成一个autorun.inf使得用户打开该盘运行病毒，并将这两个文件属性设置为隐藏、只读、系统。

* 无法手工修改“文件夹选项”将隐藏文件显示出来。

* 在每个感染后的文件夹中可见Desktop_ini的隐藏文件，内容为感染日期 如：2007-4-1

* 电脑上的所有脚本文件中加入一段代码：

```html
<iframe src=xxx width=”0” height=”0”></iframe>
```

* 中毒后的机器上常见的反病毒软件及防火墙无法正常开启及运行。

* 不能正常使用任务管理器及注册表。

* 无故的向外发包，连接局域网中其他机器。

* 感染其他应用程序的.exe文件，并改变图标颜色，但不会感染微软操作系统自身的文件。

* 删除GHOST文件(.gho后缀)，网吧、学校和单位机房深受其害。

* 禁用常见杀毒工具。

###### <span id="wu02">2).病毒特征</span>

* 关闭众多杀毒软件和安全工具。

* 循环遍历磁盘目录，感染文件，对关键系统文件跳过。

* 感染所有EXE、SCR、PIF、COM文件,并更改图标为烧香熊猫。

* 感染所有.htm/.html/.asp/.php/.jsp/.aspx文件，添加木马恶意代码。

* 自动删除*.gho文件。

###### <span id="wu03">3).发作症状</span>

1. 拷贝文件

> 病毒运行后,会把自己拷贝到C:\WINDOWS\System32\Drivers\spoclsv.exe

2. 添加注册表自启动

> 病毒会添加自启动项HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run\svcshare -> C:\WINDOWS\System32\Drivers\spoclsv.exe

3. 病毒行为

* 每隔1秒寻找桌面窗口,并关闭窗口标题中含有以下字符的程序

> QQKav,QQAV,防火墙,进程,VirusScan,网镖,杀毒,毒霸,瑞星,江民,黄山IE,超级兔子,优化大师,木马克星,木马清道夫,QQ病毒,注册表编辑器,系统配置实用程序,卡巴斯基反病毒,Symantec AntiVirus,Duba,esteem proces,绿鹰PC,密码防盗,噬菌体,木马辅助查找器,System Safety Monitor,Wrapped gift Killer,Winsock Expert,游戏木马检测大师,msctls_statusbar32,pjf(ustc),IceSword
并使用的键盘映射的方法关闭安全软件IceSword

并中止系统中以下的进程:

```
Mcshield.exe VsTskMgr.exe naPrdMgr.exe UpdaterUI.exe TBMon.exe scan32.exe
Ravmond.exe CCenter.exe RavTask.exe Rav.exe Ravmon.exe RavmonD.exe
RavStub.exe KVXP.kxp kvMonXP.kxp KVCenter.kxp KVSrvXP.exe KRegEx.exe UIHost.exe TrojDie.kxp
FrogAgent.exe Logo1_.exe Logo_1.exe Rundl132.exe
```

* 每隔18秒

> 点击病毒作者指定的网页,并用命令行检查系统中是否存在共享，存在的话就运行net share命令关闭admin$共享。

* 每隔10秒

> 下载病毒作者指定的文件,并用命令行检查系统中是否存在共享共存在的话就运行net share命令关闭admin$共享。

* 每隔6秒

> 删除安全软件在注册表中的键值。

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
RavTask KvMonXP kav KAVPersonal50 McAfeeUpdaterUI Network Associates Error Reporting Service ShStartEXE YLive.exe yassistse
```

> 并修改以下值不显示隐藏文件

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Hidden\SHOWALL\CheckedValue

修改为 0x00
```

> 删除以下服务

```
navapsvc wscsvc KPfwSvc SNDSrvc
ccProxy ccEvtMgr ccSetMgr SPBBCSvc
Symantec Core LC NPFMntor MskService FireSvc
```

* 感染文件

> 病毒会感染扩展名为exe,pif,com,src的文件,把自己附加到文件的头部并在扩展名为htm,html, asp,php,jsp,aspx的文件中添加一网址,用户一旦打开了该文件,IE就会不断的在后台点击写入的网址,达到增加点击量的目的,但病毒不会感染以下文件夹名中的文件,防止系统崩溃。

```
WINDOW
Winnt
System Volume Information
Recycled
Windows NT
WindowsUpdate
Windows Media Player
Outlook Express
Internet Explorer
NetMeeting
Common Files
ComPlus Applications
Messenger
InstallShield Installation Information
MSN
Microsoft Frontpage
Movie Maker
MSN Gamin Zone
```

### <span id="wu1">1. 查内存，排查可疑进程，将病毒从内存中干掉</span>

在虚拟机中运行熊猫烧香病毒，记得要在xp虚拟机啊，物理机现在Windows补丁已经免疫熊猫烧香了。

![9](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/9.png)

在虚拟机中我们打开任务管理器，发现刚一打开就会被关闭，这是熊猫烧香的特征之一。

![10](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/10.png)

右键一个分区，你会发现第一项不是打开，而是`Auto`，这是因为熊猫烧香病毒会在分区产生一个`autorun.inf`文件使得用户打开该盘运行病毒，`autorun.inf`文件是系统,隐藏文件。

> 甚至一些病毒会把Auto起名为打开，右键分区你会发现两个`打卡`选项。

我们第一步就要先关闭病毒进程，排查内存时我们需要使用`tasklist`命令查看可疑进程，`spoclsv.exe`就是熊猫烧香的进程名了(这个可能需要大量的积累，最好是对Windows系统进程有大量了解)。

找到后通过`taskkill /f /im PID`命令将其终止

> 有些病毒无论任务管理器还是taskkill命令都无法将其终止，这类病毒大多是有三个进程相互保护，有一个被终止后其他进程会立即再次启动这个进程。

![8](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/8.png)

### <span id="wu2">2. 查启动项，删除病毒启动项</span>

将病毒从内存中清除之后，接下来我们要删除其服务和启动项。

![12](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/12.png)

在禁用删除掉启动项之前，我们需要先记住这个病毒的路径，以便第三步去删除它的主体。

### <span id="wu3">3. 通过启动项判断病毒所在位置，并从根本上删除病毒</span>

下图就是熊猫烧香病毒本体的位置了，其实但看启动项中exe路径就能发现spoclsv服务的可疑了，它位于system32\drivers下，也不是一些常见的系统服务。

![13](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/13.png)

到这个路径下删除这个exe程序。

### <span id="wu4">4. 修复系统</span>

删除完exe之后我们重启系统，会发现现在系统中没有spoclsv.exe这个进程了。

这时病毒还有可能会复发，因为系统还未完成修复，之前说的分区双击默认选项可能会导致病毒程序再次运行。

我们需要将Auto选项删除，并且清理系统。

![14](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/14.png)

`autorun.inf`就是关联我们右键菜单的文件了。

我们通过`attrib -s -h -a -r autorun.inf`来分别将`autorun.inf`和`setup.exe`隐藏属性删除并且删除这两个文件。

![15](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/15.png)

删除之后我们双击分区打开会发现无法生效。

![16](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/16.png)

注销系统后，右键菜单恢复。

![17](https://github.com/CasterWx/Killing-Of-Actual-Combat/raw/master/img/17.png)