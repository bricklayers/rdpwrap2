### Window 10 家庭版远程桌面控制解决方案

#### 方案背景
由于个人比较懒想躺在床上用手机控制电脑，但又不想安装三方软件，此时就只能局域网内通过 远程桌面控制 去搞定，而操蛋的是 Window 10 家庭版隐藏了远程桌面控制，所以我们首先要做的就是使其支持 远程桌面控制，那么怎么支持呢？这里就需要了开源库 `rdpwrap` 的登场了

#### 下载开源工具 RDP Wrapper 配置

- GitHub资源下载 https://github.com/stascorp/rdpwrap/releases/tag/v1.6.2 由于开源库作者很久不再更新维护了，这里下载版本 v1.6.2 就行
<div align=center>
<img src="https://github.com/bricklayers/resources/blob/master/rdpwrap2/20210718182745965.png" width = "735" height = "600"/>
</div>


- 然后解压缩，管理员权限运行 install.bat文件，然后双击运行RDPConf.exe文件，如果不出意外的话看到全绿就代表成功了

<div align=center>
<img src="https://github.com/bricklayers/resources/blob/master/rdpwrap2/20210718181819890.png" alt="" align=center />
</div>

#### 疑难问题解决

-  诊断 **Service state: stopped** 未通过问题，这时可能是 `远程服务` 未启动，可通过 `Win+R` 打开 `services.msc` 服务找到 **Remote Desktop Services** 启动即可

- 诊断 **not supported** 未通过问题，因为工具库软件几年不更新了，所以配置文件都是旧的，需要自己去找最新的配置文件进行更新，具体可以根据自己对应的版本去仓库的`Issues` 搜索自己的版本，找到对应版本后覆盖 **C:\Program Files\RDP Wrapper\rdpwrap.ini** 一般都能解决，（如何查看自己的对应版本？如上图位置这里 `ver.10.0.19041.1081` 是我的版本）要注意的是覆盖前要先关闭 `远程服务`，后在启动

- 诊断 **not listening** 未通过问题，这种情况比较复杂，网上也提供了多种方案和诊断方法，如 **远程功能** （`如何查看？控制面板，系统，高级系统设置，远程`）是否开启；**远程服务** 是否开启等，操蛋的是上面方案通通不适用我此时的问题，不过最终还是让我找到了参考 @**[bunyrabitt](https://github.com/bunyrabitt)** https://github.com/stascorp/rdpwrap/issues/1454#issuecomment-875980377 的回答，设置 `远程服务` 的属性 **此账户** 设置为 `NETWORK SERVICE` 问题得到了解决
<div align=center>
<img src="https://github.com/bricklayers/resources/blob/master/rdpwrap2/20210718190557347.png" width = "507" height = "600"/>
</div>

#### 局域网内手机远程桌面控制方案

这是最终目的，如何实现手机远程控制桌面呢？前提是在同一网络环境下，`App Store` 搜索 `Microsoft 远程桌面` 下载，安装好后 **添加电脑** ，电脑名称填写电脑的 `IP地址` 即可，这样就可以远程链接电脑了，**特别注意的是 `电脑要设置密码` ，否则会连接不上**


#### 附录：
库中提供了版本为 `ver.10.0.19041.1081` 的 rdpwrap.ini 文件



