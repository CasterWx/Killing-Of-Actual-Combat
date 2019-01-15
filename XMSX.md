## <span id="wu">手动查杀病毒实战——熊猫烧香病毒</span>

> 如果像自己实践记得在虚拟机下！
> 病毒包可以在Github仓库找到


<li><a href="#wu">&#x624B;&#x52A8;&#x67E5;&#x6740;&#x75C5;&#x6BD2;&#x5B9E;&#x6218;&#x2014;&#x2014;&#x718A;&#x732B;&#x70E7;&#x9999;&#x75C5;&#x6BD2;</a>
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