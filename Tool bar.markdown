# Tool bar

标签（空格分隔）： Android

---

### API Level & Platform Version
| Platform Version       | API Level   |  VERSION_CODE  |
| --------   | -----:  | :----:  |
| Android 6.0    | 23 |   Marshmallow     |
| Android 5.0        |   21  |   Lollipop   |
| Android 4.4        |    19    |  KitKat  |
| Android 4.0, 4.0.1, 4.0.2        |    14    |  ICE_CREAM_SANDWICH|
| Android 3.0.x        |    11    |  HONEYCOMB  |
| Android 2.3.2, 2.3.1, 2.3        |    9    |  Gingerbread  |
| Android 2.2.x       |    8    |  Froyo  |
**Reference:**  [The table above specifies the API Level supported by each version of the Android platform](http://developer.android.com/intl/zh-cn/guide/topics/manifest/uses-sdk-element.html#ApiLevels)

## Setting Up the App Bar
Beginning with Android 3.0 (API level 11), all activities that use the default theme have an ActionBar as an app bar. However, app bar features have gradually been added to the native ActionBar over various Android releases. As a result, the native ActionBar behaves differently depending on what version of the Android system a device may be using. By contrast, the most recent features are added to the support library's version of Toolbar, and they are available on any device that can use the support library.


## R文件缺失解决方案
Import Android projects，R 文件缺失，解决方案：
1. 右击你的工程(项目)——>Android Tools——>Fix Project Properties。
2. 检查你的源代码是否有错误。
3. 然后检查资源文件中是否有错误，可能是图片文件名重名，或者布局文件出错，或者string.xml文件出错等等。
4. 如果还有问题,并且XML没有提示，这时可以尝试修改一下任何一个.java文件，然后保存，这时Console窗口会有错误提示，修改错误。
5. 如果还不行，尝试菜单栏的Project——>Clean——>当前工程。





## Building the Android Support Library v7 samples

在import Support7Demos 项目后，需要设置依赖 android-support-v7-appcompat、android-support-v7-gridlayout、android-support-v7-mediarouter，但是还是显示有错。

**problem:**
>Getting the following errors in android-support-v7-mediarouter/res/values/styles.xml:

>**error:** Error retrieving parent for item: No resource found that matches the given name 'Widget.AppCompat.ActionButton'. (line 18)
**error:** Error retrieving parent for item: No resource found that matches the given name 'Widget.AppCompat.Light.ActionButton'. (line 28) 

**solution:**
>You must make the android-support-v7-mediarouter project "aware" of the android-support-v7-appcompat project as a referenced library.
Right click android-support-v7-mediarouter project, select Properties
Select Android In the Library section at the bottom, click Add....
Select android-support-v7-appcompat in the dialog.
Click Apply.
Click OK.
Do a clean build on the android-support-v7-mediarouter project.



Reference：
http://blog.csdn.net/twlkyao/article/details/8670496 
