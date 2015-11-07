# Android 支持多种设备

标签（空格分隔）： Android

------

> Android是一个“碎片化”的世界。多种系统版本、多种尺寸、多种分辨率、多种机型，还有不同的厂商定制的不同ROM，开发的应用会在不可预期的手机上报错。这给开发适配带来不小的难度。这篇文章会进行相关分析。多数资料参考来源 Android API指南，详细转至官网文档。

------

## Support Different Screens

### Screen size 屏幕尺寸
Actual physical size, measured as the screen's diagonal.
For simplicity, Android groups all actual screen sizes into four generalized sizes: small, normal, large, and extra-large.

物理尺寸测量为屏幕对角线长度，为简便，可将所有屏幕尺寸分为为small, normal, large, and extra-large 四个标准。

**small**：尺寸类似于低密度 QVGA 屏幕的屏幕。小屏幕的最小布局尺寸约为 320x426 dp 单位。例如，QVGA 低密度屏幕和 VGA 高密度屏幕。
**normal**：尺寸类似于中等密度 HVGA 屏幕的屏幕。标准屏幕的最小布局尺寸约为 320x470 dp 单位。例如，WQVGA 低密度屏幕、HVGA 中等密度屏幕、WVGA 高密度屏幕。
**large**：尺寸类似于中等密度 VGA 屏幕的屏幕。 大屏幕的最小布局尺寸约为 480x640 dp 单位。 例如，VGA 和 WVGA 中等密度屏幕。
**xlarge**：明显大于传统中等密度 HVGA 屏幕的屏幕。超大屏幕的最小布局尺寸约为 720x960 dp 单位。在大多数情况下，屏幕超大的设备体积过大，不能放进口袋，最常见的是平板式设备。 此项为 API 级别 9 中新增配置。

### Screen density 屏幕密度
The quantity of pixels within a physical area of the screen; usually referred to as dpi (dots per inch). For example, a "low" density screen has fewer pixels within a given physical area, compared to a "normal" or "high" density screen.
For simplicity, Android groups all actual screen densities into six generalized densities: low, medium, high, extra-high, extra-extra-high, and extra-extra-extra-high.

dpi 表示每英寸屏幕像素点的数目，衡量屏幕的细腻程度，为简便起见，可将所以所以屏幕密度分为: low, medium, high, extra-high, extra-extra-high, and extra-extra-extra-high 6个标准。下面为各自尺寸：
> LDPI（低）〜120DPI
MDPI（中）〜160dpi
HDPI（高）〜240dpi
xhdpi（超高）〜320dpi
xxhdpi（超超高）〜480dpi
xxxhdpi（超特超高）〜640dpi

### Orientation 屏幕方向
The orientation of the screen from the user's point of view. This is either landscape or portrait, meaning that the screen's aspect ratio is either wide or tall, respectively. Be aware that not only do different devices operate in different orientations by default, but the orientation can change at runtime when the user rotates the device.

### Resolution 分辨率
The total number of physical pixels on a screen. When adding support for multiple screens, applications do not work directly with resolution; applications should be concerned only with screen size and density, as specified by the generalized size and density groups.
Density-independent pixel (dp)
A virtual pixel unit that you should use when defining UI layout, to express layout dimensions or position in a density-independent way.
The density-independent pixel is equivalent to one physical pixel on a 160 dpi screen, which is the baseline density assumed by the system for a "medium" density screen. At runtime, the system transparently handles any scaling of the dp units, as necessary, based on the actual density of the screen in use. The conversion of dp units to screen pixels is simple: px = dp * (dpi / 160). For example, on a 240 dpi screen, 1 dp equals 1.5 physical pixels. You should always use dp units when defining your application's UI, to ensure proper display of your UI on screens with different densities.

分辨率一般指屏幕上垂直方向和水平方向上的像素个数，例如1920 *1080，dip 密度独立（无关）像素，缩写dp，指抽象意义上的像素。跟设备的屏幕密度有关系。在dpi为160的屏幕上（"medium" 等级屏幕密度），1dp = 1px , px 是物理像素的单位，dp 和 px 之间的换算公式很简单：px = dp * (dpi / 160). 举例，在240dpi 的屏幕上，1dp等价1.5物理像素。使用dp为单位可以避免因为不同屏幕密度差异产生布局不协调。

### Alternative drawables
To create alternative bitmap drawables for different densities, you should follow the 3:4:6:8:12:16 scaling ratio between the six generalized densities. For example, if you have a bitmap drawable that's 48x48 pixels for medium-density screens, all the different sizes should be:

36x36 (0.75x) for low-density
48x48 (1.0x baseline) for medium-density
72x72 (1.5x) for high-density
96x96 (2.0x) for extra-high-density
180x180 (3.0x) for extra-extra-high-density
192x192 (4.0x) for extra-extra-extra-high-density (launcher icon only; see note above)

### Best Practices
Here is a quick checklist about how you can ensure that your application displays properly on different screens:

- Use wrap_content, fill_parent, dp or sp units when specifying dimensions in an XML layout file
- Do not use hard coded pixel values in your application code
- Do not use AbsoluteLayout (it's deprecated)
- Supply alternative bitmap drawables for different screen densities
The following sections provide more details.

## Support Different Languages
### Create Locale Directories and String Files
To add support for more languages, create additional values directories inside res/ that include a hyphen and the ISO language code at the end of the directory name. 
```
MyProject/
    res/
       values/
           strings.xml
       values-es/
           strings.xml
       values-fr/
           strings.xml
       values-zh/
           strings.xml
```
English (default locale)
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="title">My Application</string>
    <string name="hello_world">Hello World!</string>
</resources>
```
French
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="title">Mon Application</string>
    <string name="hello_world">Bonjour le monde !</string>
</resources>
```
> ISO language code 639-1:
http://www.loc.gov/standards/iso639-2/php/code_list.php 

### Use the String Resources

You can reference your string resources in your source code and other XML files using the resource name defined by the <string> element's name attribute.
For example:
```
// Get a string resource from your app's Resources
String hello = getResources().getString(R.string.hello_world);

// Or supply a string resource to a method that requires a string
TextView textView = new TextView(this);
textView.setText(R.string.hello_world);
```

For example:
```
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/hello_world" />
```
### Android 如何找到最匹配资源

https://developer.android.com/intl/zh-cn/guide/topics/resources/providing-resources.html#BestMatch

## Supporting Different Platform Versions
https://developer.android.com/intl/zh-cn/training/basics/supporting-devices/platforms.html 
While the latest versions of Android often provide great APIs for your app, you should continue to support older versions of Android until more devices get updated. This lesson shows you how to take advantage of the latest APIs while continuing to support older versions as well.

### Support Library Features
https://developer.android.com/intl/zh-cn/tools/support-library/features.html#v7 
#### Setting Up the App Bar


Kelvin 
2015 年 10 月 30 日    

