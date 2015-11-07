# Android 开发前期工作

标签（空格分隔）： Android

---

### ADT Download
收集整理Android开发所需的Android SDK、ADT Bundle、开发中用到的工具、Android开发教程、Android设计规范，免费的设计素材等。

http://www.androiddevtools.cn/ 

### Eclipse 已安装的SDK及ADT插件更新
更新已安装 SDK版本：
1. 打开Android SDK Manager,把Tools 文件下的Android SDK Tools和Android SDK Platform-tools升级到最新，然后退出。
2. 重新进入或（reload）,选择要升级的Android API、SDK版本。 
升级 Android ADT插件
1. 如果Eclipse 版本在Version: 3.6.2以上的话，直接在菜单栏中Eclipse ——Help ——Check for Updates操作即可。
2. 如果所使用Eclipse版本较低的话，在升级ADT插件之前，需要去升级Eclipse 相应插件，最后去官网下载最新的ADT Plugin,本地安装ADT,需要删除掉之前的。安装完成后重启Eclipse完成升级！

### 默认情况 SDK Manager 更新SDK 失败
由于一些原因，Android SDK Manager更新经常会遇到Fitch fail URL等错误。以下通过代理服务器来解决国内访问慢的问题。

**解决方案：**
1. 启动 Android SDK Manager；
2. 打开主界面，依次选择「Tools」、「Options…」，弹出『Android SDK Manager – Settings』窗口；
3. 在『Android SDK Manager – Settings』窗口中，在「HTTP Proxy Server」和「HTTP Proxy Port」输入框内填入mirrors.opencas.cn和80，并且选中「Force https://… sources to be fetched using http://…」复选框；
4. 设置完成后单击「Close」按钮关闭『Android SDK Manager – Settings』窗口返回到主界面；
5. 依次选择「Packages」、「Reload」。

**Android SDK在线更新镜像服务器**

1. 中科院开源协会镜像站： 
> http://mirrors.opencas.cn 端口：80
> http://mirrors.opencas.org 端口：80(备份)
> http://mirrors.opencas.ac.cn 端口：80(备份)

2. 上海GDG镜像服务器地址:
> http://sdk.gdgshanghai.com 端口：8000

3. 北京化工大学镜像服务器地址:
> IPv4: http://ubuntu.buct.edu.cn/ 端口：80
> IPv4: http://ubuntu.buct.cn/ 端口：80
> IPv6: http://ubuntu.buct6.edu.cn/ 端口：80

4. 大连东软信息学院镜像服务器地址:
> http://mirrors.neusoft.edu.cn 端口：80

5. 腾讯Bugly 镜像:
> http://android-mirror.bugly.qq.com 端口：8080

腾讯镜像使用方法:http://android-mirror.bugly.qq.com:8080/include/usage.html

### SDK 更新后问题
The eclipse ADT plugin version doesn't match your SDK tools version，which describes "Android SDK requires Android Developer Toolkit version 23.0.0 or above.  Current version is 22.3.0.v201310242005-887826.  Please update ADT to the latest version."

由于 SDK 版本更新后导致与 ADT 版本过低不匹配，尝试如下：
**方案一：**
1. Help --> Install new software
2. Then choose "Android Developer Tools Update Site - http://dl-ssl.google.com/android/eclipse/" from the drop down list and update the ADT,
**产生新问题**： Cannot complete the install because of a conflicting dependency.

**方案二：**尝试先卸载ADT，后安装：

1. 选择 Help > Install New Software；
2. 在"Details" 面板中, 点击"What is already installed?" 链接；
3. 在Eclipse Installation Details 对话框中，选择"Android DDMS"和"Android Development Tools" ，然后点击Uninstall；
4. 在下一个窗口中，确认要删除的ADT，然后点击Finish进行删除；
5. 重启Eclipse.
**产生新问题**： 然而无法单独选择"Android DDMS"和"Android Development Tools"进行卸载……

**方案三：**准备下载单独的ADT Plugin，后进行安装：

Help > Install New Software > Add > Archive，结果还是导入失败。

**方案四：**下载新版本ADT Bundle，将已更新的SDK文件夹覆盖

No resource found that matches the given name: attr 'android:windowElevation'.

### Android更新最新版本的SDK引用v7资源报错问题
**错误一：** v7资源项目里的res资源属性报错,其中values-large-v14里的有个parent找不到。 No resource found that matches the given name 'Base.Theme.AppCompat.Light.DialogWhenLarge.Base'.

    <style name="Theme.Base.AppCompat.DialogWhenLarge"
       parent="Theme.Base.AppCompat.DialogWhenLarge.Base" />
    <style name="Theme.Base.AppCompat.Light.DialogWhenLarge"
       parent="Theme.Base.AppCompat.Light.DialogWhenLarge.Base" />
       
**解决方案：** 

    <style name="Theme.Base.AppCompat.DialogWhenLarge"
           parent="Base.Theme.AppCompat.DialogWhenLarge" />

    <style name="Theme.Base.AppCompat.Light.DialogWhenLarge"
           parent="Base.Theme.AppCompat.Light.DialogWhenLarge" />
          
**错误二：**  android-support-v7-appcompat\res\layout\abc_action_bar_home.xml:29: error: Error: No resource found that matches the given name (at 'layout_marginBottom' with value '@dimen/abc_action_bar_icon_vertical_padding').
           
**解决方案：**  在 value --> dimen 文件中添加一行
< dimen name="abc_action_bar_icon_vertical_padding">4dip< /dimen> 


### Github 安装
Github团队目前采用的是微软的 ClickOnce 技术来安装和更新应用程序，同时他们也在开发的自己同类的工具 Squirrel ,可能是因为防火墙，每次总是无法完整下载就和服务器断开了连接，一直没能下载成功，下面为其中一种解决方案：

1. 打开控制面板→ Internet 选项→“安全”选项卡；
2. 选择“可信的站点”→点击“站点”按钮：
3. 弹出的窗口中的文本框中输入点击“添加”  https://github-windows.s3.amazonaws.com/；
或者去除复选框“对该区域中的所有站点要求服务器验证(https:)”的钩，直接加入 github-windows.s3.amazonaws.com ；
4. 在IE浏览器中打开 https://github-windows.s3.amazonaws.com/GitHub.application
5. 运行安装。


---
**Reference：**
[Github Windows 离线安装](http://coderafi.github.io/archive/2015-07-08/githubforwindowsoffline/)
[GitHub for Windows离线安装的方法](http://www.cnblogs.com/fantacity/p/4347472.html)
