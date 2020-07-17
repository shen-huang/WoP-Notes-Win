# 设置文件夹


## 把文件夹添加到快速访问区

为了方便操作，我把课程相关的文件夹固定到了资源管理器的快速访问区：

<img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Quick_access.png" width="287" alt="快速访问" />

具体的操作是在资源管理器里打开想要固定到快速访问区的文件夹，然后点击 <span class="menutext">主页</span> 选项卡中的 <span class="menutext">固定到快速访问</span> ：

<img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Pin_to_Quick_access.png" width="1120" alt="固定到快速访问" />

如果不需要了，也可以取消固定，在打算取消固定的文件夹上点击鼠标右键，再在右键菜单里点击 <span class="menutext">从“快速访问”取消固定</span> ：

<img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Unpin_from_Quick_access.png" width="350" alt="从“快速访问”取消固定" />

这样操作完成之后，可能会有点不好看——“桌面”、“文档”、“图片”等文件夹的图标各有不同，但新固定上去的文件夹图标都是默认的样子。为了美观、醒目，可以把文件夹的图标做一点修改。


## 修改文件夹图标

通过资源管理器设置文件夹的属性，就可以修改文件夹的图标，具体的操作是：

在要修改的文件夹上点击鼠标右键，在弹出的菜单中点击 <span class="menutext">属性</span>，在弹出的窗口中点击 <span class="menutext">自定义</span> 选项卡，在其中的 <span class="menutext">文件夹图标</span> 区域里点击 <span class="menutext">更改图标(I)...</span>，选择图标，点击 <span class="menutext">确定</span>。

这一系列操作实际做的动作，是在被设置的文件夹中创建一个隐藏的 <span class="paths">desktop.ini</span> 文件，在其中写入了文件夹图标的配置信息，再把文件夹属性设置为“只读”，最后刷新图标缓存。

这个操作虽然浅显易懂，但它有一个弊病——把这样设置好图标的文件夹移动到其他计算机的时候，设置可能会失效。这是由于文件夹属性的设置中，表示图标位置默认使用的是“**绝对路径**”，也就是说，一旦图标位置或者文件夹位置进行了调整，就可能因为找不到图标而使设置失效。

相对更稳妥的做法，是采用“**相对路径**”来设置图标的位置。这种设置需要直接修改 <span class="paths">desktop.ini</span> 文件。具体步骤如下——

1. 在文件夹中建立 <span class="paths">desktop.ini</span> 文件。
2. 在文件夹中放入需要使用的图标文件，如 <span class="paths">foldericon.ico</span>。
3. 在 <span class="paths">desktop.ini</span> 写入图标相关的配置信息，例如：  
    ```ini
    [.ShellClassInfo]
    IconResource=foldericon.ico,0
    ```
4. 将文件夹属性设置为“只读”，这个步骤需要借助命令行完成，打开命令行后，输入并执行：
    ```powershell
    ATTRIB +R /D [文件夹路径]
    ```
5. 在资源管理器中，把欲处理的文件夹内的其他文件夹和文件的属性里的“只读”去掉。
6. 视需要，将 <span class="paths">desktop.ini</span> 文件和文件夹所用的图标文件的属性设置为隐藏。
7. 刷新图标缓存：  
   进入 <span class="paths">C:\\Users\\<用户名>\\AppData\\Local</span> 文件夹，删除 <span class="paths">IconCache.db</span> 文件，通过任务管理器重新启动资源管理器，或者，重启计算机。

除了文件夹图标外，<span class="paths">desktop.ini</span> 文件还可以控制文件夹的背景、文字颜色等，相关信息可以参考：

- [<span class="paths">Desktop.ini</span> 文件详解](https://blog.csdn.net/mawj0326/article/details/83883213)  
  [https://blog.csdn.net/mawj0326/article/details/83883213](https://blog.csdn.net/mawj0326/article/details/83883213)
- [<span class="paths">Desktop.ini</span> Commands](https://hwiegman.home.xs4all.nl/desktopini.html)  
  [https://hwiegman.home.xs4all.nl/desktopini.html](https://hwiegman.home.xs4all.nl/desktopini.html)
- [<span class="paths">Desktop.ini</span>](https://ru.wikipedia.org/wiki/Desktop.ini)  
  [https://ru.wikipedia.org/wiki/Desktop.ini](https://ru.wikipedia.org/wiki/Desktop.ini)


## 图标的来源

### 系统自带

Windows 自带了一系列的图标，这些图标基本上都存在 <span class="paths">%SystemRoot%\System32\\</span> 文件夹里的一系列 <span class="paths">.dll</span> 文件中。具体来说，主要是这些：

- Windows 10 风格
  - <span class="paths">%SystemRoot%\System32\DDORes.dll</span>
  - <span class="paths">%SystemRoot%\System32\dmdskres.dll</span>
  - <span class="paths">%SystemRoot%\System32\imageres.dll</span>
  - <span class="paths">%SystemRoot%\System32\mmres.dll</span>
  - <span class="paths">%SystemRoot%\System32\networkexplorer.dll</span>
  - <span class="paths">%SystemRoot%\System32\pnidui.dll</span>
  - <span class="paths">%SystemRoot%\System32\SensorsCpl.dll</span>
  - <span class="paths">%SystemRoot%\System32\setupapi.dll</span>
  - <span class="paths">%SystemRoot%\System32\shell32.dll</span>
  - <span class="paths">%SystemRoot%\System32\wmploc.dll</span>
  - <span class="paths">%SystemRoot%\System32\wpdshext.dll</span>
- Windows 7 风格
  - <span class="paths">%SystemRoot%\System32\accessibilitycpl.dll</span>
  - <span class="paths">%SystemRoot%\System32\dsuiext.dll</span>
  - <span class="paths">%SystemRoot%\System32\gameux.dll</span>
  - <span class="paths">%SystemRoot%\System32\ieframe.dll</span>
  - <span class="paths">%SystemRoot%\System32\mstscax.dll</span>
  - <span class="paths">%SystemRoot%\System32\netcenter.dll</span>
- Windows 早期风格
  - <span class="paths">%SystemRoot%\System32\compstui.dll</span>
  - <span class="paths">%SystemRoot%\System32\mmcndmgr.dll</span>
  - <span class="paths">%SystemRoot%\System32\moricons.dll</span>
  - <span class="paths">%SystemRoot%\System32\pifmgr.dll</span>

这些文件中具体图标内容可以参考[吕毅](https://blog.walterlv.com/)撰写的《[Windows 10 自带那么多图标，去哪里找呢？](https://blog.walterlv.com/post/where-is-the-windows-10-native-icons.html)》一文。

### 网络搜寻

如果系统自带的图标不够用，还可以使用网络上的资源。

比如 [Iconfont](https://www.iconfont.cn/)、[Iconfinder](https://www.iconfinder.com/)、[Icons8](https://icons8.com/) 等图标库网站中就有很多值得一用的图标；[DeviantArt](https://www.deviantart.com/)、[Pinterest](https://www.pinterest.com/)、[Dribbble](https://dribbble.com/)、[Behance](https://www.behance.net/) 等设计网站也有不少可选择的资源；还可以从 [Google Play](https://play.google.com/store/search?q=icon%20pack&c=apps)、[酷安](https://www.coolapk.com/apk/tag/%E5%9B%BE%E6%A0%87)等平台寻找图标包，解开 APK 文件后挑选需要的图标。提醒：具体操作时请注意具体授权。

### 按需自制

有些时候我们手里想要用的资源不是图标的 <span class="paths">.ico</span> 格式的，又有些时候找到的图标不是很合心意，在这种情况下可能就需要自己制作图标了。

自制图标可以用把图片文件转换成图标格式的方式来做，在线多文件转换工具 [Convertio](https://convertio.co/zh/) 就提供了将多种不同格式图片转换成图标的[在线 ICO 转换器](https://convertio.co/zh/ico-converter/)，如果上传的图片是包含有透明部分的 PNG 图片，还可以转换成同样透明的 ICO 文件。

不过在线转换工具可能无法生成包含多个不同图标尺寸的 ICO 文件，要实现在不同尺寸下呈现更合适的图标的目的，专门的图标制作软件更为合适。比如使用功能很丰富的开源软件 [Greenfish Icon Editor Pro](http://greenfishsoftware.org/gfie.php)，轻巧好用的 [IcoFX Portable](https://portableapps.com/apps/graphics_pictures/icofx_portable)，或者功能强大的 [Axialis IconWorkshop](https://www.axialis.com/download/iw.html)，都可以完成制作专业化的图标文件的工作。

## 最终成品

我为了制作出和原本的图标风格一致的图标，在系统自带的 <span class="paths">imageres.dll</span> 文件里的图标的基础上，用网络图片和图标软件自制了放置代码的 Code 文件夹和用来与 GitHub 同步的 GitHub 文件夹的图标。

成品是这个效果：

<img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Quick_access_Folder_Icon_Changed.png" width="287" alt="快速访问(改)" />

在像素密度略低的显示器上，也有对应的变化：

<img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Quick_access_Folder_Icon_Changed_S.png" alt="快速访问(改)(低清)" />

这两个图标的成品文件我上传了，两种形态，有需要的可以自取：

- [Code 文件夹图标 1](https://raw.githubusercontent.com/shen-huang/img/master/Icon/SourceCodeFolder.ico)<br />
  <img src="https://raw.githubusercontent.com/shen-huang/img/master/Icon/SourceCodeFolder.ico" width="96" alt="SourceCodeFolder.ico" /><br />
  [https://github.com/shen-huang/img/blob/master/Icon/SourceCodeFolder.ico](https://github.com/shen-huang/img/blob/master/Icon/SourceCodeFolder.ico)  

- [Code 文件夹图标 2](https://raw.githubusercontent.com/shen-huang/img/master/Icon/SourceCode.ico)<br />
  <img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/source-code.png" width="96" alt="SourceCode.ico" /><br />
  [https://github.com/shen-huang/img/blob/master/Icon/SourceCode.ico](https://github.com/shen-huang/img/blob/master/Icon/SourceCode.ico)  

- [GitHub 文件夹图标 1](https://raw.githubusercontent.com/shen-huang/img/master/Icon/GitHubFolder.ico)<br />
  <img src="https://raw.githubusercontent.com/shen-huang/img/master/Icon/GitHubFolder.ico" width="96" alt="GitHubFolder.ico" /><br />
  [https://github.com/shen-huang/img/blob/master/Icon/GitHubFolder.ico](https://github.com/shen-huang/img/blob/master/Icon/GitHubFolder.ico)  
  
- [GitHub 文件夹图标 2](https://raw.githubusercontent.com/shen-huang/img/master/Icon/GitHub.ico)<br />
  <img src="https://raw.githubusercontent.com/shen-huang/img/master/Logo/GitHub-Mark-Black-L.png" width="96" alt="GitHub.ico" /><br />
  [https://github.com/shen-huang/img/blob/master/Icon/GitHub.ico](https://github.com/shen-huang/img/blob/master/Icon/GitHub.ico)

所用素材来自：

- Icons8 的 [Fluent Icons of Programming](https://icons8.com/icon/pack/programming/fluent)  
  [https://icons8.com/icon/pack/programming/fluent](https://icons8.com/icon/pack/programming/fluent)
- [GitHub Logos and Usage](https://github.com/logos)  
  [https://github.com/logos](https://github.com/logos)

**参考资料：**

- [《在快速访问中进行固定、删除和自定义》，Microsoft，2017 年 11 月 29 日](https://support.microsoft.com/zh-cn/help/4027032/windows-pin-remove-and-customize-in-quick-access)  
  [https://support.microsoft.com/zh-cn/help/4027032/windows-pin-remove-and-customize-in-quick-access](https://support.microsoft.com/zh-cn/help/4027032/windows-pin-remove-and-customize-in-quick-access)
- [*Pin, remove, and customize in Quick access*, Microsoft, 2017-11-21](https://support.microsoft.com/en-us/help/4027032/windows-pin-remove-and-customize-in-quick-access)  
  [https://support.microsoft.com/en-us/help/4027032/windows-pin-remove-and-customize-in-quick-access](https://support.microsoft.com/en-us/help/4027032/windows-pin-remove-and-customize-in-quick-access)
- [《看烦了 Windows 原生文件夹图标？收下这套最全的更换图标教程》，沨沄极客，2017 年 11 月 16 日](https://sspai.com/post/41824)  
  [https://sspai.com/post/41824](https://sspai.com/post/41824)
- [《图标显示不正常？试试强制刷新 Windows 图标缓存》，沨沄极客，2018 年 01 月 17 日](https://sspai.com/post/42874)  
  [https://sspai.com/post/42874](https://sspai.com/post/42874)
- [《个性化文件夹图标》，LanternD，2018 年 03 月 18 日](https://dlyang.me/customized-folder-icon/)  
  [https://dlyang.me/customized-folder-icon/](https://dlyang.me/customized-folder-icon/)
- [《Windows 10 自带那么多图标，去哪里找呢？》，吕毅，2018 年 02 月 27 日](https://blog.walterlv.com/post/where-is-the-windows-10-native-icons.html)  
  [https://blog.walterlv.com/post/where-is-the-windows-10-native-icons.html](https://blog.walterlv.com/post/where-is-the-windows-10-native-icons.html)