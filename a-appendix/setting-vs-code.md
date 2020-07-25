# 设置 Visual Studio Code

Visual Studio Code（简称 VS Code）是功能非常丰富的一个开源现代编辑器，用好它可以大大地提升写代码和写文档的效率。


## VS Code 的安装和升级

![Visual Studio Code 主页][Visual_Studio_Code_Main_page]

访问 [Visual Studio Code 的主页][]（[https://code.visualstudio.com](https://code.visualstudio.com/)），点击<button class="btn blue mini">Download for Windows</button>即可下载安装文件，下载完成后，运行并按默认设置完成安装即可。

启动 VS Code 后，会显示欢迎页——

![][Visual_Studio_Code_welcome_page]

此时，点击菜单 <span class="menutext">Help</span> - <span class="menutext">Check for Updates...</span>，即可检查版本情况，建议根据提示进行升级。

![Visual Studio Code 检查升级][Visual_Studio_Code_Check_for_Updates]


## VS Code 的外观调试

### 中文界面

为了方便使用，可以给 VS Code 加装中文语言插件，把 VS Code 的界面改为中文。

点击侧边的<button class="btn gray mini">Extensions</button>按钮（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd>）打开扩展面板，在写有“Search Extensions in Marketplace”提示的搜索框中点击，输入“Chinese”，可以看到一系列与中文相关的插件——

![][Visual_Studio_Code_Extensions_Chinese]

点击搜索列表中的“[Chinese (Simplified) Language Pack for Visual Studio Code][]”，右侧窗口会显示出相关信息，由此可以得知这是微软官方为 VS Code 制作的中文语言包。点击页面中绿色的<button class="btn green mini">Install</button>按钮，安装该语言包。

![][Visual_Studio_Code_Extensions_Chinese_Language_Pack]

安装完成后，原本的<button class="btn green mini">Install</button>按钮会变为蓝色的<button class="btn blue mini">Uninstall</button>按钮，并提示 VS Code 需要重启来使语言包生效，点击提示对话框中的<button class="btn blue mini">Restart Now</button>按钮重启。

![][Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install]

重启后 VS Code 会自动切换为中文界面，下文内容以中文界面为准。

![][Visual_Studio_Code_Chinese_Interface]

### 主题、图标

VS Code 的应用商店中有着大量可以选择的扩展，主题和图标就是其中数目众多的两类，它们可以改变 VS Code 的“外貌”，让 VS Code 更适合具体用户的口味。

和安装中文语言包一样，点击侧边的<button class="btn gray mini">扩展</button>按钮（快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd>）打开扩展面板，搜索“Theme”就能看到大量可选择的主题。

![][Visual_Studio_Code_Extensions_Theme] 

点击面板中的主题名称，就可以看到主题的详细情况：

![][Visual_Studio_Code_Extensions_Theme_Preview]

这些搜索结果是按照用户评价的综合得分排列的，所以开头列出的这些都值得一试，点击页面中绿色的<button class="btn green mini">安装</button>按钮，即可安装主题。

安装完成后，点击 VS Code 左侧工具栏里的 <span class="menutext">管理</span> 按钮，再点击 <span class="menutext">颜色主题</span>（快捷键为先按 <kbd>Ctrl</kbd> + <kbd>K</kbd>，再按 <kbd>Ctrl</kbd> + <kbd>T</kbd>），会弹出对话框，使用 <kbd>↑</kbd> 和 <kbd>↓</kbd> 可以预览主题，点击即为选用。

好主题很多，挨个安装、切换、调试这些主题，也是件费时费力的事情。为了挑选起来轻松一点，我参考了 Geoff Stevens 在 2020 年 1 月 6 日写的[《50 VS Code themes for 2020》](https://dev.to/thegeoffstevens/50-vs-code-themes-for-2020-45cc)（[原发表于 Software.com](https://www.software.com/src/50-vs-code-themes-for-2020)），这篇文章还给出了三个方便测试的“合集”：
- [深色主题包（Best Dark Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-dark-themes-pack)
- [浅色主题包（Best Light Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-light-themes-pack)
- [多色主题包（Best Light Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-colorful-themes-pack)

图标的设定和主题很相似，使用关键字“Icon”在扩展面板里搜索、安装即可。安装后点击 <span class="menutext">管理</span> 按钮，再点击 <span class="menutext">文件图标主题</span>，就会弹出供预览、选择的对话框。

我最后选择了 [One Monokai](https://marketplace.visualstudio.com/items?itemName=azemoh.one-monokai) 主题，和 [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) 图标包。

### 字体

与主题

<!-- TODO -->

<!-- 我使用了 Fira Code 和汉仪旗黑的搭配 -->


<!-- 插图 -->

[Visual_Studio_Code_Main_page]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Main_page.png
[Visual_Studio_Code_welcome_page]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_welcome_page.png
[Visual_Studio_Code_Check_for_Updates]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Check_for_Updates.png
[Visual_Studio_Code_Extensions_Chinese]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Extensions_Chinese.png
[Visual_Studio_Code_Extensions_Chinese_Language_Pack]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Extensions_Chinese_Language_Pack.png
[Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install.png
[Visual_Studio_Code_Chinese_Interface]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Chinese_Interface.png
[Visual_Studio_Code_Extensions_Theme]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Extensions_Theme.png
[Visual_Studio_Code_Extensions_Theme_Preview]: https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Extensions_Theme_Preview.png

<!-- 
https://raw.githubusercontent.com/shen-huang/img/master/2020-07/
 -->

<!-- 链接 -->

[Visual Studio Code 的主页]: https://code.visualstudio.com/
[Chinese (Simplified) Language Pack for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans