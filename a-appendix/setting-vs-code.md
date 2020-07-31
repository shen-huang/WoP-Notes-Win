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

### 字体

写代码和写其他内容相比，有一个特点：**代码中的每个字都很重要，有些语言（比如 Python）的代码中连空格都很重要。**

也因为这个特点，读写代码对所用的字体有一些要求：
1. 相似的字符必须容易区分（如 0、O、o，I、l、1、L、|，i、j，u、v，:、;，“、” 等）；
2. 空格的个数必须容易判别；
3. 包含尽可能多的字符（至少支持 [EASCII](https://en.wikipedia.org/wiki/Extended_ASCII)，最好支持 [UTF-8](https://en.wikipedia.org/wiki/UTF-8)）；
4. 字形尽量清晰易读；
5. 字符宽度最好一致。

如果不满足这些条件，那视觉效果可能“难以卒读”，为了更直观地理解相关情况，Windie Chai 制作了一个[极端的反例](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/)：

![][Bad_Code_Font]

<!-- 
<p class="figwithback"><img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Bad_Code_Font.png" alt="不恰当的代码字体选择" /></p>

<div class="figtitle">不恰当的代码字体选择<span>&nbsp;</span><span class="figtitlevia">来源：Windie Chai</span></div>
 -->

这个反例中，字母的“[大写字高](https://zh.wikipedia.org/wiki/%E5%A4%A7%E5%AF%AB%E9%AB%98%E5%BA%A6)”与“[x 字高](https://zh.wikipedia.org/wiki/X%E5%AD%97%E9%AB%98)”差距很大，致使小写字母整体上不易分辨；同时由于字形设计的缘故，多个字符难以分辨（小写字母`l`、大写字母`I`、数字`1`、符号`|`，大写字母`O`和数字`0`，小写字母`u`和`v`等）；部分标点的形态令人困惑（如下划线）；空格状况也不易确定。

另一段内容完全一样，只有字体不同的 Python 代码的对比也可以说明一些问题——

<pre style="font-family: 'Times New Roman', Times, SimSun, STSong, serif; background-color: var(--code-theme-background); color: var(--code-theme-text);">
s = """Gur Mra bs Clguba, ol Gvz Crgref

Ornhgvshy vf orggre guna htyl.
[...]
Anzrfcnprf ner bar ubaxvat terng vqrn -- yrg'f qb zber bs gubfr!"""

d = {}
for c in (65, 97):                          # 这部分负责将字符串
    for i in range(26):                     # 中的字母按照某一种
        d[chr(i+c)] = chr((i+13) % 26 + c)  # 特定方式进行转换。

 print("".join([d.get(c, c) for c in s]))
</pre>
<div class="figtitle">使用<a href="https://zh.wikipedia.org/wiki/%E6%AF%94%E4%BE%8B%E5%AD%97%E4%BD%93">比例字体（Proportional Font）</a>显示的一段 Python 代码<span>&nbsp;</span><span class="figtitlevia">来源：“Python 之禅”的源代码</span></div>

<pre style="font-family: Consolas, Monaco, 'Courier New', Courier, 'Noto Sans CJK SC', 'Source Han Sans SC', 'Source Han Sans CN', 'Microsoft Yahei', 'PingFang SC', 'STHeiti', 微软雅黑, monospace, sans-serif; background-color: var(--code-theme-background); color: var(--code-theme-text);">
s = """Gur Mra bs Clguba, ol Gvz Crgref

Ornhgvshy vf orggre guna htyl.
[...]
Anzrfcnprf ner bar ubaxvat terng vqrn -- yrg'f qb zber bs gubfr!"""

d = {}
for c in (65, 97):                          # 这部分负责将字符串
    for i in range(26):                     # 中的字母按照某一种
        d[chr(i+c)] = chr((i+13) % 26 + c)  # 特定方式进行转换。

 print("".join([d.get(c, c) for c in s]))
</pre>
<div class="figtitle">使用<a href="https://zh.wikipedia.org/wiki/%E7%AD%89%E5%AE%BD%E5%AD%97%E4%BD%93">等宽字体（Monospaced Font）</a>显示的一段 Python 代码<span>&nbsp;</span><span class="figtitlevia">来源：“Python 之禅”的源代码</span></div>

上面这两段代码中，最后一行的 `print` 前面都多了一个空格（这会导致代码无法正常运行），对比来说，**字符宽度一致**的“[等宽字体（Monospaced Font）](https://zh.wikipedia.org/wiki/%E7%AD%89%E5%AE%BD%E5%AD%97%E4%BD%93)”相较**字符宽度不同**的“[比例字体（Proportional Font）](https://zh.wikipedia.org/wiki/%E6%AF%94%E4%BE%8B%E5%AD%97%E4%BD%93)”更易发现这个问题。等宽字体也更便于处理代码里行内注释的纵向对齐。

了解了这些情况后，我们可以得出这样的结论：**在 VS Code 里写代码应该选择<span class="typo-em">设计优良</span>的等宽字体。** 

点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">设置</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd>）打开设置页面，修改其中“Editor: **Font Family**”区域里的设置，就可以修改 VS Code 使用的字体。

![][Visual_Studio_Code_Config]

此处默认设置为 `Consolas, 'Courier New', monospace`，这表示 VS Code 在显示某个字符的时候，首先尝试使用 <span style="font-family: Consolas, monospace;">Consolas</span> 字体，如果系统没有安装 <span style="font-family: Consolas, monospace;">Consolas</span> 字体或 <span style="font-family: Consolas, monospace;">Consolas</span> 字体里没有该字符，则尝试使用 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体，如果系统没有安装 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体或 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体里没有该字符，则尝试使用系统默认的“等宽字体”（`monospace` 代指系统默认设定的等宽字体，并不是某个特定字体的名字），如果仍然不行，则尝试按照系统的设置使用其他字体，如果所有的尝试都失败了，则显示一个标明错误的符号。

由于 VS Code 采用了“逐一尝试”的字体选择逻辑，设置字体的时候就有几个要注意的点：

- 字体排序要按想要选择的顺序来设置，不同的字体间要用 `,` 隔开；
- 如果字体名称里有空格，那么要在字体名称的左右两边加上 `'` ；
- 中文字体可能需要使用对应的英文字体名（可参考[张鑫旭](https://www.zhangxinxu.com/life/about/) 2017 年 3 月 25 日发布的[《CSS font-family 常见中文字体对应的英文名称》](https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/)一文）。

VS Code 默认的首选英文字体为 <span style="font-family: Consolas, monospace;">Consolas</span>，这是微软专门为代码显示设计的一款等宽字体，在大部分时间都挺合用的，但一混上中文情况就不妙了，由于 <span style="font-family: Consolas, sans-serif;">Consolas</span> 本身没有中文部分，其后的 <span style="font-family: 'Courier New', monospace;">Courier New</span> 也显示不出中文，跟着就是 <span style="font-family: monospace;">monospace</span>，这在简体中文版 Windows 10 上很可能会落到系统自带的“<span style="font-family: SimSun, STSong, monospace;">宋体</span>”上，也就会令 VS Code 默认使用<span style="font-family: SimSun, STSong, serif;">宋体</span>来显示中文，这看上去就不大协调。

![][Visual_Studio_Code_Consolas_SimSun]

<div class="figtitle">VS Code 默认使用 Consolas 字体和宋体</div>

删去 `monospace` 会让 VS Code 改为使用系统默认的中文字体——在简体中文版 Windows 10 上是“<span style="font-family: 'Microsoft Yahei', sans-serif;">微软雅黑</span>”——来显示中文，这貌似可以接受，可如果是中英文混杂的文本，此时会遭遇比较麻烦的对齐问题。

在理想状态下，代码中的 1 个中文字宽应该等于 2 个英文字宽，这样可以让中英文混杂的行纵向对齐，实际上这很难准确实现。

靠 VS Code 分别调用中英文字体，通常做不到中英文混杂内容的纵向对齐。一些专门为此制作的字体也不好用，我试了民间自制的 YaHei Consolas Hybrid（微软雅黑和 Consolas 的混合字体）、Microsoft Yahei Mono（也是微软雅黑和 Consolas 的混合字体）、Yahei Source Code Pro（微软雅黑和 Source Code Pro 的混合字体），都对不齐，Yahei Source Code Pro 在 VS Code 里自动折行的效果还有问题。

![][Visual_Studio_Code_YaHei_Consolas_Hybrid]

<div class="figtitle">VS Code 使用 YaHei Consolas Hybrid 字体</div>

![][Visual_Studio_Code_Microsoft_Yahei_Mono]

<div class="figtitle">VS Code 使用 Microsoft Yahei Mono 字体</div>

![][Visual_Studio_Code_Yahei_Source_Code_Pro]

<div class="figtitle">VS Code 使用 Yahei Source Code Pro 字体</div>

专门针对多语种混合对齐这一目的制作的[“等距更纱黑体”（`'Sarasa Term SC'`）](https://github.com/be5invis/Sarasa-Gothic)，对齐倒是很完美，但英文部分我觉得太窄了，看着有些累。

![][Visual_Studio_Code_Sarasa_Term_SC]

<div class="figtitle">VS Code 使用等距更纱黑体</div>

话虽如此，“等距更纱黑体”已经基本上是现在可用的最好的多语种文字等宽字体了。还不满意的话，只能暂且放下对多语种混合对齐的追求了。

放下执念之后，要做的就是挑一套相对合心意的字体组合。

在英文字体部分，我参考了社会化评测网站 [Slant][] 上的“[What are the best programming fonts?](https://www.slant.co/topics/67/~best-programming-fonts)”和“[What are the best monospace programming fonts with ligatures?](https://www.slant.co/topics/5611/~monospace-programming-fonts-with-ligatures)”页面，Charlee Li 在 2018 年 5 月 15 日发布的[《11 Best Programming Fonts》](https://itnext.io/11-best-programming-fonts-724283a9ed57)一文，以及 William Judd 在 2018 年 5 月 16 日发布的[《The 10 best fonts for programming: A guide》](https://developer-tech.com/news/2018/may/16/10-best-fonts-programming/)一文，经过一系列尝试，最后选择了 [Fira Code 字体](https://github.com/tonsky/FiraCode)。

Fira Code 字体满足写代码的各种需求，它还有一个额外的设计：提供了代码领域专用的“[合字（ligature）](https://zh.wikipedia.org/wiki/%E5%90%88%E5%AD%97)”。

所谓“合字”，就是把两个甚至数个特定字符自动替换为另外的字符，如将“`->`”自动替换为“`→`”。具体效果可以参考官方的对比图：

![](https://raw.githubusercontent.com/shen-huang/FiraCode/master/extras/ligatures.png)

以及在不同语言中呈现的效果样例：

![](https://raw.githubusercontent.com/shen-huang/FiraCode/master/extras/samples.png)

合字好不好，是个见仁见智的问题。有的人认为它让代码变得更加直观，方便阅读；有的人认为它改变了字符原本的形态，干扰书写。我觉得至少可以试试，怎么都不习惯的话，把这个特性关掉就是了。

开关合字的具体方法是：点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">设置</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd>）打开设置页面，点击 <span class="menutext">文本编辑器</span> - <span class="menutext">字体</span>，在“**Font Ligatures**”区域点击“<u>在 settings.json 中编辑</u>”。

![][Visual_Studio_Code_Settings_Font_Ligatures]

随后会打开 <span class="paths">settings.json</span> 文件，将其中的 `"editor.fontLigatures":` 后面设为 `true,` 就是启用合字，设为 `false,` 就是停用合字。

![][Visual_Studio_Code_Settings_Font_Ligatures_true]

在中文字体部分，很多人会习惯性地使用“微软雅黑”，但我觉得微软雅黑有个小问题：它的有些标点设计区分度不足，比如全宽的双引号（<code><span style="font-family: 'Microsoft Yahei', sans-serif;">“</span></code> 和 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">”</span></code>），单引号（<code><span style="font-family: 'Microsoft Yahei', sans-serif;">‘</span></code> 和 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">’</span></code>）间就很可能难以区分，如果再混上半宽的 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">"</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">'</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">`</span></code>，可就会导致混乱；常用的全宽的 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">，</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">：</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">；</span></code>等符号也存在可能不易看清的问题。

微软雅黑标点的问题，在搭配上 <span style="font-family: Consolas, monospace;">Consolas</span> 或者 <span style="font-family: 'Fira Code', Consolas, monospace;">Fira Code</span> 等字体后会有一定程度的缓解，引号的问题通常就没有了，但


设置页面中“Editor: **Font Size**”区域里的数字是控制 VS Code 所用字体的显示尺寸的，如果显示器较大或显示器的像素密度较高，适当调大这个数字可以让眼睛轻松一点。

<!-- TODO -->

<!-- 我使用了 Fira Code 和汉仪旗黑的搭配 -->

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

![][Visual_Studio_Code_Theme_and_Icons]
<div class="figtitle">VS Code 使用 One Monokai 主题和 Material Icon Theme 图标包</div>

<!-- TODO -->

<!-- 
PicGo
https://github.com/Molunerfinn/PicGo
https://github.com/PicGo/vs-picgo
https://marketplace.visualstudio.com/items?itemName=Spades.vs-picgo
 -->

<!-- 插图 -->

[Visual_Studio_Code_Main_page]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Main_page.png
[Visual_Studio_Code_welcome_page]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_welcome_page.png
[Visual_Studio_Code_Check_for_Updates]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Check_for_Updates.png
[Visual_Studio_Code_Extensions_Chinese]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Chinese.png
[Visual_Studio_Code_Extensions_Chinese_Language_Pack]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Chinese_Language_Pack.png
[Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install.png
[Visual_Studio_Code_Chinese_Interface]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Chinese_Interface.png

[Bad_Code_Font]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Bad_Code_Font.png
[Visual_Studio_Code_Config]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Config.png

[Visual_Studio_Code_Consolas_SimSun]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Consolas_SimSun.png
[Visual_Studio_Code_YaHei_Consolas_Hybrid]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_YaHei_Consolas_Hybrid.png
[Visual_Studio_Code_Microsoft_Yahei_Mono]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Microsoft_Yahei_Mono.png
[Visual_Studio_Code_Yahei_Source_Code_Pro]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Yahei_Source_Code_Pro.png
[Visual_Studio_Code_Sarasa_Mono_SC]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Sarasa_Mono_SC.png
[Visual_Studio_Code_Sarasa_Term_SC]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Sarasa_Term_SC.png
[Visual_Studio_Code_Settings_Font_Ligatures]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Settings_Font_Ligatures.png
[Visual_Studio_Code_Settings_Font_Ligatures_true]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Settings_Font_Ligatures_true.png

[Visual_Studio_Code_Extensions_Theme]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Theme.png
[Visual_Studio_Code_Extensions_Theme_Preview]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Theme_Preview.png
[Visual_Studio_Code_Theme_and_Icons]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Theme_and_Icons.png

<!-- 
https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/

https://raw.githubusercontent.com/shen-huang/img/master
 -->

<!-- 链接 -->

[Visual Studio Code 的主页]: https://code.visualstudio.com/
[Chinese (Simplified) Language Pack for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans
[Slant]: https://www.slant.co/

**参考资料**

- [《让代码看起来更舒服（2）：选择适合的字体》，Windie Chai，2009-11-22。](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/)  
  [http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/)
- [What is the default serif, sans-serif and monospace font-family for Mac OS X? Jeff, 2012-08-24.](https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x)  
  [https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x](https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x)
- [《CSS font-family 詳細介紹》，oxxo，2018-11-30。](https://www.oxxostudio.tw/articles/201811/css-font-family.html)  
  [https://www.oxxostudio.tw/articles/201811/css-font-family.html](https://www.oxxostudio.tw/articles/201811/css-font-family.html)
- [《在 VSCode 中使用（汉字）等宽字体》，张慕晖，2018-11-19。](https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/)  
  [https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/](https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/)
- [《分享一下自己修改的字体~ Yahei Source Code Pro v1.23》，DeepKolos，2017-07-15。](https://www.jianshu.com/p/28acf9226ddb)  
  [https://www.jianshu.com/p/28acf9226ddb](https://www.jianshu.com/p/28acf9226ddb)
- [YaHei Consolas Hybrid 和 Yahei Source Code Pro 的下载页面](https://github.com/yyxyz/OSOperateSkills/find/master)  
  [https://github.com/yyxyz/OSOperateSkills/find/master](https://github.com/yyxyz/OSOperateSkills/find/master)
- [更纱黑体主仓库](https://github.com/be5invis/Sarasa-Gothic)  
  [https://github.com/be5invis/Sarasa-Gothic](https://github.com/be5invis/Sarasa-Gothic)
- [Iosevka 字体主页](https://typeof.net/Iosevka/)  
  [https://typeof.net/Iosevka/](https://typeof.net/Iosevka/)
