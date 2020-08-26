# 设置 Visual Studio Code

Visual Studio Code（简称 VS Code）是功能非常丰富的一个开源现代编辑器，用好它可以大大地提升写代码和写文档的效率。


## VS Code 的安装升级

![Visual Studio Code 主页][Visual_Studio_Code_Main_page]

访问 [Visual Studio Code 的主页][]（<a href="https://code.visualstudio.com"><span class="paths">https://code.visualstudio.com/</span></a>），点击<button class="btn blue mini">Download for Windows</button>即可下载安装文件，下载完成后，运行并按默认设置完成安装即可。

启动 VS Code 后，会显示欢迎页——

![Visual Studio Code 欢迎页][Visual_Studio_Code_welcome_page]

点击菜单 <span class="menutext">Help</span> - <span class="menutext">Check for Updates...</span>，即可检查版本情况。VS Code 的更新频率很高，建议根据提示及时升级。

![Visual Studio Code 检查升级][Visual_Studio_Code_Check_for_Updates]


## VS Code 的外观调试

### 中文界面

为了方便使用，可以给 VS Code 加装中文语言扩展，把 VS Code 的界面改为中文。

点击侧边的<button class="btn gray mini">Extensions</button>按钮（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd>）打开扩展面板，在写有“Search Extensions in Marketplace”提示的搜索框中点击，输入“Chinese”，可以看到一系列与中文相关的扩展——

![Visual Studio Code 中文扩展][Visual_Studio_Code_Extensions_Chinese]

点击搜索列表中的“[Chinese (Simplified) Language Pack for Visual Studio Code][]”，右侧窗口会显示出相关信息，由此可以得知这是微软官方为 VS Code 制作的中文语言包。点击页面中绿色的<button class="btn green mini">Install</button>按钮，安装该语言包。

![Visual Studio Code 中文语言包][Visual_Studio_Code_Extensions_Chinese_Language_Pack]

安装完成后，原本的<button class="btn green mini">Install</button>按钮会变为蓝色的<button class="btn blue mini">Uninstall</button>按钮，并提示 VS Code 需要重启来使语言包生效，点击提示对话框中的<button class="btn blue mini">Restart Now</button>按钮重启。

![Visual Studio Code 安装中文语言包][Visual_Studio_Code_Extensions_Chinese_Language_Pack_Install]

重启后 VS Code 会自动切换为中文界面，下文内容以中文界面为准。

![Visual Studio Code 中文界面][Visual_Studio_Code_Chinese_Interface]

### 字体

写代码和写其他内容相比，有一个特点：**代码中的每个字都很重要，有些语言（比如 Python）的代码中连空格都很重要。**

也因为这个特点，读写代码对所用的字体有一些要求：

1. 相似的字符必须容易区分（如 0、O、o，I、l、1、L、|，i、j，u、v，:、;，“、” 等）；
2. 空格的个数必须容易判别；
3. 包含尽可能多的字符（至少支持 [EASCII](https://en.wikipedia.org/wiki/Extended_ASCII)，最好支持 [UTF-8](https://en.wikipedia.org/wiki/UTF-8)）；
4. 字形尽量清晰易读；
5. 字符宽度最好一致。

如果不满足这些条件，那视觉效果可能“难以卒读”，为了更直观地理解相关情况，Windie Chai 制作了一个[极端的反例](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/)：

<!-- ![][Bad_Code_Font] -->

<!-- 
<p class="figwithback"><img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Bad_Code_Font.png" alt="不恰当的代码字体选择" /></p>

<div class="figtitle">不恰当的代码字体选择<span>&nbsp;</span><span class="figtitlevia">来源：Windie Chai</span></div>
 -->

<figure style="background-color: #E3D5C1;" class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Bad_Code_Font.png" alt="不恰当的代码字体选择"/>
  <figcaption class="figtitle">不恰当的代码字体选择<span>&nbsp;</span><span class="figtitlevia">来源：Windie Chai</span></figcaption>
</figure>

这个反例中，字母的“[大写字高](https://zh.wikipedia.org/wiki/%E5%A4%A7%E5%AF%AB%E9%AB%98%E5%BA%A6)”与“[x 字高](https://zh.wikipedia.org/wiki/X%E5%AD%97%E9%AB%98)”差距很大，致使小写字母整体上不易分辨；同时由于字形设计的缘故，多个字符难以分辨（小写字母`l`、大写字母`I`、数字`1`、符号`|`，大写字母`O`和数字`0`，小写字母`u`和`v`等）；部分标点的形态令人困惑（如下划线）；空格状况也不易确定。

另一段内容完全一样，只有字体不同的 Python 代码的对比也可以说明一些问题——

<figure class="codes">
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
</pre><figcaption class="figtitle">使用<a href="https://zh.wikipedia.org/wiki/%E6%AF%94%E4%BE%8B%E5%AD%97%E4%BD%93">比例字体（Proportional Font）</a>显示的一段 Python 代码<span>&nbsp;</span><span class="figtitlevia">来源：“Python 之禅”的源代码</span></figcaption></figure>

<figure class="codes">
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
</pre><figcaption class="figtitle">使用<a href="https://zh.wikipedia.org/wiki/%E7%AD%89%E5%AE%BD%E5%AD%97%E4%BD%93">等宽字体（Monospaced Font）</a>显示的一段 Python 代码<span>&nbsp;</span><span class="figtitlevia">来源：“Python 之禅”的源代码</span></figcaption></figure>

上面这两段代码中，最后一行的 `print` 前面都多了一个空格（这会导致代码无法正常运行），对比来说，**字符宽度一致**的“[等宽字体（Monospaced Font）](https://zh.wikipedia.org/wiki/%E7%AD%89%E5%AE%BD%E5%AD%97%E4%BD%93)”相较**字符宽度不同**的“[比例字体（Proportional Font）](https://zh.wikipedia.org/wiki/%E6%AF%94%E4%BE%8B%E5%AD%97%E4%BD%93)”更易发现这个问题。等宽字体也更便于处理代码里行内注释的纵向对齐。

了解了这些情况后，我们可以得出这样的结论：**在 VS Code 里写代码应该选择<span class="typo-em">设计优良</span>的等宽字体。**

点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">设置</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd>）打开设置页面，修改其中“Editor: **Font Family**”区域里的设置，就可以修改 VS Code 使用的字体。

![Visual Studio Code 设置][Visual_Studio_Code_Config]

此处默认设置为 `Consolas, 'Courier New', monospace`，这表示 VS Code 在显示某个字符的时候，首先尝试使用 <span style="font-family: Consolas, monospace;">Consolas</span> 字体，如果系统没有安装 <span style="font-family: Consolas, monospace;">Consolas</span> 字体或 <span style="font-family: Consolas, monospace;">Consolas</span> 字体里没有该字符，则尝试使用 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体，如果系统没有安装 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体或 <span style="font-family: 'Courier New', monospace;">Courier New</span> 字体里没有该字符，则尝试使用系统默认的“等宽字体”（`monospace` 代指系统默认设定的等宽字体，并不是某个特定字体的名字），如果仍然不行，则尝试按照系统的设置使用其他字体，如果所有的尝试都失败了，则显示一个标明错误的符号。

由于 VS Code 采用了“逐一尝试”的字体选择逻辑，设置字体的时候就有几个要注意的点：

- 字体排序要按想要选择的顺序来设置，不同的字体间要用 `,` 隔开；
- 如果字体名称里有空格，那么要在字体名称的左右两边加上 `'` ；
- 中文字体可能需要使用对应的英文字体名称。

VS Code 默认的首选英文字体为 <span style="font-family: Consolas, monospace;">Consolas</span>，这是微软专门为代码显示设计的一款等宽字体，在大部分时间都挺合用的，但一混上中文情况就不妙了，由于 <span style="font-family: Consolas, sans-serif;">Consolas</span> 本身没有中文部分，其后的 <span style="font-family: 'Courier New', monospace;">Courier New</span> 也显示不出中文，跟着就是 <span style="font-family: monospace;">monospace</span>，这在简体中文版 Windows 10 上很可能会落到系统自带的“<span style="font-family: SimSun, STSong, monospace;">宋体</span>”上，也就会令 VS Code 默认使用<span style="font-family: SimSun, STSong, serif;">宋体</span>来显示中文，这看上去就不大协调。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Consolas_SimSun.png" alt="VS Code 默认使用 Consolas 字体和宋体"/>
  <figcaption class="figtitle">VS Code 默认使用 Consolas 字体和宋体</figcaption>
</figure>

删去 `monospace` 会让 VS Code 改为使用系统默认的中文字体——在简体中文版 Windows 10 上是“<span style="font-family: 'Microsoft Yahei', sans-serif;">微软雅黑</span>”——来显示中文，这貌似可以接受，可如果是中英文混杂的文本，此时会遭遇比较麻烦的对齐问题。

在理想状态下，代码中的 1 个中文字宽应该等于 2 个英文字宽，这样可以让中英文混杂的行纵向对齐，实际上这很难准确实现。

靠 VS Code 分别调用中英文字体，通常做不到中英文混杂内容的纵向对齐。一些专门为此制作的字体也不好用，我试了民间自制的 YaHei Consolas Hybrid（微软雅黑和 Consolas 的混合字体）、Microsoft Yahei Mono（也是微软雅黑和 Consolas 的混合字体）、Yahei Source Code Pro（微软雅黑和 Source Code Pro 的混合字体），都对不齐，Yahei Source Code Pro 在 VS Code 里自动折行的效果还有问题。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_YaHei_Consolas_Hybrid.png" alt="VS Code 使用 YaHei Consolas Hybrid 字体"/>
  <figcaption class="figtitle">VS Code 使用 YaHei Consolas Hybrid 字体</figcaption>
</figure>

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Microsoft_Yahei_Mono.png" alt="VS Code 使用 Microsoft Yahei Mono 字体"/>
  <figcaption class="figtitle">VS Code 使用 Microsoft Yahei Mono 字体</figcaption>
</figure>

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Yahei_Source_Code_Pro.png" alt="VS Code 使用 Yahei Source Code Pro 字体"/>
  <figcaption class="figtitle">VS Code 使用 Yahei Source Code Pro 字体</figcaption>
</figure>

专门针对多语种混合对齐这一目的制作的[“等距更纱黑体”](https://github.com/be5invis/Sarasa-Gothic)，对齐倒是很完美，但英文部分我觉得太窄了，看着有些累。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Sarasa_Term_SC.png" alt="VS Code 使用等距更纱黑体"/>
  <figcaption class="figtitle">VS Code 使用等距更纱黑体</figcaption>
</figure>

话虽如此，“等距更纱黑体”已经基本上是现在可用的最好的多语种文字等宽字体了。还不满意的话，只能暂且放下对多语种混合对齐的追求了。

放下执念之后，要做的就是挑一套相对合心意的字体组合。

在英文字体部分，我参考了社会化评测网站 [Slant][] 上的“[What are the best programming fonts?](https://www.slant.co/topics/67/~best-programming-fonts)”和“[What are the best monospace programming fonts with ligatures?](https://www.slant.co/topics/5611/~monospace-programming-fonts-with-ligatures)”页面，Charlee Li 在 2018 年 5 月 15 日发布的[《11 Best Programming Fonts》](https://itnext.io/11-best-programming-fonts-724283a9ed57)一文，以及 William Judd 在 2018 年 5 月 16 日发布的[《The 10 best fonts for programming: A guide》](https://developer-tech.com/news/2018/may/16/10-best-fonts-programming/)一文，经过一系列尝试，最后选择了 [Fira Code 字体](https://github.com/tonsky/FiraCode)。

Fira Code 字体满足写代码的各种需求，它还有一个额外的设计：提供了代码领域专用的“[合字（ligature）](https://zh.wikipedia.org/wiki/%E5%90%88%E5%AD%97)”。

<!-- 所谓“合字”，就是把两个甚至数个特定字符自动替换为另外的字符，如将“<code style="font-family: Inconsolata, Consolas, Menlo, Monaco, 'Andale Mono WT', 'Andale Mono', 'Lucida Console', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', Courier,  monospace">-></code>”自动替换为“<code><img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Fira_Code_Arrow_Ligature.svg?sanitize=true" alt="Fira Code Arrow Ligature" height=10.5px></code>”。具体效果可以参考官方的对比图： -->

所谓“合字”，就是把两个甚至数个特定字符自动替换为另外的字符，如将“<code style="font-family: Inconsolata, Consolas, Menlo, Monaco, 'Andale Mono WT', 'Andale Mono', 'Lucida Console', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', Courier,  monospace">-></code>”自动替换为“`⟶`”。具体效果可以参考[官方的对比图](https://github.com/tonsky/FiraCode#whats-in-the-box)：

![Fira Code 字体连字范例](https://cdn.jsdelivr.net/gh/shen-huang/FiraCode@master/extras/ligatures.png)

以及在不同语言中呈现的效果样例：

![Fira Code 字体连字在程序语言中的显示](https://cdn.jsdelivr.net/gh/shen-huang/FiraCode@master/extras/samples.png)

合字好不好，是个见仁见智的问题。有的人认为它让代码变得更加直观，方便阅读；有的人认为它改变了字符原本的形态，干扰书写。我觉得至少可以试试，怎么都不习惯的话，把这个特性关掉就是了。

开关合字的具体方法是：点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">设置</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd>）打开设置页面，点击 <span class="menutext">文本编辑器</span> - <span class="menutext">字体</span>，在“**Font Ligatures**”区域点击“<u>在 settings.json 中编辑</u>”。

![Visual Studio Code 设置连字][Visual_Studio_Code_Settings_Font_Ligatures]

随后会打开 <span class="paths">settings.json</span> 文件，将其中的 `"editor.fontLigatures":` 后面设为 `true,` 就是启用合字，设为 `false,` 就是停用合字。

![Visual Studio Code 启用连字][Visual_Studio_Code_Settings_Font_Ligatures_true]

在中文字体部分，很多人会习惯性地使用“微软雅黑”，但我觉得微软雅黑有个小问题：它的有些标点设计区分度不足，比如全宽的双引号（<code><span style="font-family: 'Microsoft Yahei', sans-serif;">“</span></code> 和 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">”</span></code>），单引号（<code><span style="font-family: 'Microsoft Yahei', sans-serif;">‘</span></code> 和 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">’</span></code>）间就很可能难以区分，如果再混上半宽的 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">"</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">'</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">`</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">′</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">″</span></code>，可能就会导致混乱；常用的全宽的 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">，</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">：</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">；</span></code> 和半宽的 <code><span style="font-family: 'Microsoft Yahei', sans-serif;">,</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">:</span></code>、<code><span style="font-family: 'Microsoft Yahei', sans-serif;">;</span></code> 等符号也存在可能不易看清的问题。

微软雅黑标点的问题，在搭配上 <span style="font-family: Consolas, monospace;">Consolas</span> 或者 <span style="font-family: 'Fira Code', Consolas, monospace;">Fira Code</span> 等字体后会有一定程度的缓解，引号的问题通常就没有了，但逗号、冒号、分号等的问题还是在的。

经过试验，我感觉和微软雅黑有些渊源关系的[方正兰亭黑](http://www.foundertype.com/index.php/FontInfo/index/id/216.html)和[汉仪旗黑](http://www.hanyi.com.cn/productdetail.php?id=832)可以一用。此外，开源免费的[思源黑体](https://github.com/adobe-fonts/source-han-sans/blob/master/README-CN.md)（该字体由 Adobe 和 Google 联合开发，Google 将其归在了“[Noto 字体系列](https://www.google.com/get/noto/)”，称为“Noto Sans”，针对中文简化字进行适配的版本称为“Noto Sans CJK SC”）的效果也还可以。

给 VS Code 设置中文字体的时候还有一个要注意的事情：可能需要使用字体的英文名称。

举几个例子。微软雅黑，可以将字体设置写为“`微软雅黑`”或“`Microsoft Yahei`”；等宽更纱黑体，建议写为“`Sarasa Term SC`”；思源黑体，若使用 Adobe 版的，可以写为“`思源黑体`”或“`Source Han Sans SC`”，但若是使用 Google 版的，就需要写为<wbr>“`Noto Sans CJK SC`”；汉仪旗黑需要带上字重，写成类似“`HYQihei 50S`”、“`HYQihei 55S`”的样子；方正兰亭黑会涉及到字重和编码，需要写成类似“`FZLanTingHei-R-GBK`”的样子。

更多的字体名称对应关系可参考[张鑫旭](https://www.zhangxinxu.com/life/about/) 2017 年 3 月 25 日专门为此撰写的[《CSS font-family 常见中文字体对应的英文名称》](https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/)一文。文中未涵盖的字体，可以用 [FontForge](https://fontforge.org/en-US/)、[FontCreator](https://www.high-logic.com/font-editor/fontcreator) 等工具，通过读取字体文件中的“字体族”（Typographic Family，该项为空的话则为 Font Family）字段来确认。

<!-- FontCreator 里为 Extended 中的 Typographic Family，该项为空的话则使用 Identification 中的 Font Family -->

我最后选择了 55 字重的汉仪旗黑来搭配 Fire Code。

设置页面中“Editor: **Font Size**”区域里的数字是控制 VS Code 所用字体的显示尺寸的，如果显示器较大或显示器的像素密度较高，适当调大这个数字可以让眼睛轻松一点。我将这一项设置为了 `16`。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Fira_Code_HYQihei_16.png" alt="VS Code 使用字号 16 的 Fira Code 字体和汉仪旗黑字体"/>
  <figcaption class="figtitle">VS Code 使用字号 16 的 Fira Code 字体和汉仪旗黑字体</figcaption>
</figure>

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Font_Settings.png" alt="VS Code 字体相关设置"/>
  <figcaption class="figtitle">VS Code 字体相关设置</figcaption>
</figure>

### 主题、图标

VS Code 的应用商店中有着大量可以选择的扩展，主题和图标就是其中数目众多的两类，它们可以改变 VS Code 的“外貌”，让 VS Code 更适合具体用户的口味。

和安装中文语言包一样，点击侧边的<button class="btn gray mini">扩展</button>按钮（快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd>）打开扩展面板，搜索“Theme”就能看到大量可选择的主题。

![Visual Studio Code 主题][Visual_Studio_Code_Extensions_Theme]

点击面板中的主题名称，就可以看到主题的详细情况：

![Visual Studio Code 主题介绍][Visual_Studio_Code_Extensions_Theme_Preview]

这些搜索结果是按照用户评价的综合得分排列的，所以开头列出的这些都值得一试，点击页面中绿色的<button class="btn green mini">安装</button>（或<button class="btn green mini">Install</button>）按钮，即可安装主题。

安装完成后，点击 VS Code 左侧工具栏里的 <span class="menutext">管理</span> 按钮，再点击 <span class="menutext">颜色主题</span>（快捷键为先按 <kbd>Ctrl</kbd> + <kbd>K</kbd>，再按 <kbd>Ctrl</kbd> + <kbd>T</kbd>），会弹出对话框，使用 <kbd>↑</kbd> 和 <kbd>↓</kbd> 可以预览主题，点击即为选用。

好主题很多，挨个安装、切换、调试这些主题，也是件费时费力的事情。为了挑选起来轻松一点，我参考了 Geoff Stevens 在 2020 年 1 月 6 日写的[《50 VS Code themes for 2020》](https://dev.to/thegeoffstevens/50-vs-code-themes-for-2020-45cc)（[原发表于 Software.com](https://www.software.com/src/50-vs-code-themes-for-2020)），这篇文章还给出了三个方便测试的“合集”：

- [深色主题包（Best Dark Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-dark-themes-pack)
- [浅色主题包（Best Light Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-light-themes-pack)
- [多色主题包（Best Light Themes Pack）](https://marketplace.visualstudio.com/items?itemName=thegeoffstevens.best-colorful-themes-pack)

图标的设定和主题很相似，使用关键字“Icon”在扩展面板里搜索、安装即可。安装后点击 <span class="menutext">管理</span> 按钮，再点击 <span class="menutext">文件图标主题</span>，就会弹出供预览、选择的对话框。

我最后选择了 [One Monokai](https://marketplace.visualstudio.com/items?itemName=azemoh.one-monokai) 主题，和 [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) 图标包。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Theme_and_Icons.png" alt="VS Code 使用 One Monokai 主题和 Material Icon Theme 图标包"/>
  <figcaption class="figtitle">VS Code 使用 One Monokai 主题和 Material Icon Theme 图标包</figcaption>
</figure>

## VS Code 的常用扩展

### Python

由于课程的原因，必装的扩展是“[Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)”。

这是微软为 Python 语言制作的扩展，提供了 Python 编程相关的自动完成、语法检查、代码分析、环境设置、代码重构等等功能，可以说如果打算使用 VS Code 进行 Python 编程，这个扩展是不可或缺的。

安装它之前需要装好（至少一个）Python 环境，如果已经使用 Scoop 安装过 Python，就可以安装这个扩展了。

它的安装方法和前文中语言包、主题、图标的安装类似，点击侧边的<button class="btn gray mini">扩展</button>按钮（快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd>）打开扩展面板，搜索“Python”就能看到，点击页面中绿色的<button class="btn green mini">安装</button>（或<button class="btn green mini">Install</button>）按钮，即可完成安装。后文中涉及的其他扩展的安装方法亦与此类似，故不再赘述。

![Visual Studio Code Python 扩展][Visual_Studio_Code_Python_extension]

Python 扩展安装完成，并找到系统中的 Python 环境后，通常就可以直接使用 VS Code 进行 Python 相关的工作了，更多的详细内容可以参考微软的相关教程[《Editing Python in Visual Studio Code》](https://code.visualstudio.com/docs/python/editing)（[Greg Van Liew](https://github.com/gregvanl) 等，2019-01-29）。

### Linter

和许多语言不同，Python 要求严格的代码缩进对齐，这导致有的时候仅仅是多了一个空格，代码就出现问题。有些时候问题出得还相当隐蔽，比如这样一段代码：

<pre v-pre="" data-lang="python" class="language-python"><code class="lang-python language-python"><span class="token keyword">if</span> <span class="token boolean">True</span><span class="token punctuation">:</span>
&#9;<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">)</span>
<span class="token keyword">else</span><span class="token punctuation">:</span>
&#9;<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"b"</span><span class="token punctuation">)</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"c"</span><span class="token punctuation">)</span></code><button class="docsify-copy-code-button"><span class="label">点击复制</span><span class="error">错误</span><span class="success">已复制</span></button></pre>

在网页上看似乎没有什么问题，但贴到 VS Code 里就无法正常运行。它在 VS Code 里可能长这样：  
![制表符和空格对比](https://cdn.jsdelivr.net/gh/shen-huang/img@master/2019-08/Tab_and_Space_0.png)

这里对齐出现了问题，这是由于代码编写时混用了制表符（<span class="unicode-number">U+0009</span> <span class="unicode-name">CHARACTER TABULATION</span>，即按 <kbd>Tab</kbd> 键输出的字符）和空格（<span class="unicode-number">U+0020</span> <span class="unicode-name">SPACE</span>，即按 <kbd>Space</kbd> 键输出的字符）的缘故。

这种情况在自己写代码的时候并不多见，VS Code 为了避免这种问题，特意在设置里默认把制表符替换成了空格（通过菜单 <span class="menutext">文件(F)</span> - <span class="menutext">首选项</span> - <span class="menutext">设置</span>，或按快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd> 就能看到）。但当我们从各种途径复制粘贴代码的时候，难免会把不同来源的代码混在一起，继而出现混用制表符和空格的问题。

要避免出现这种问题，首先得有认真细致的态度，同时相应的工具也是必不可少的。

最直观的方法，是在 VS Code 的设置里把空白字符的显示打开（在 <span class="menutext">文本编辑器</span> 的 <span class="menutext">Render Whitespace</span> 选项框下选择“boundary”或者“all”即可），靠肉眼看出问题。更高级的方法，是使用[“静态程序分析工具”（英文为 lint 或 linter）](https://en.wikipedia.org/wiki/Lint_(software))来辅助分析。

要在 VS Code 里设置静态程序分析工具，需要点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">命令面板...</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>），输入 `Linter`，点击“Python: 选择 Linter 插件”，再点击要启用的插件即可。可选择的插件中，“pylint”是 Python 扩展所带的插件，一般可以直接使用。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Select_Linter.png" alt="Python: Select Linter"/>
  <figcaption class="figtitle">调出“Python: 选择 Linter 插件”</figcaption>
</figure>

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Select_Linter_list.png" alt="Python: Select Linter - list"/>
  <figcaption class="figtitle">“Python: 选择 Linter 插件”的可选列表</figcaption>
</figure>

其他插件各有长处，可以按需选择，选择后可能会弹出提示告知需要安装，根据提示操作即可，设定完成后也可以随时切换。我个人使用了分析内容相对更多的“[Flake8](https://pypi.org/project/flake8/)”插件（除了语法检查外，还有代码风格检查）。

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Select_Linter_list_flake8_Install.png" alt="flake8 Install"/>
  <figcaption class="figtitle">Flake8 安装提示</figcaption>
</figure>

<figure class="image">
  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Select_Linter_list_flake8_Install_successful.png" alt="flake8 Successfully installed"/>
  <figcaption class="figtitle">Flake8 安装完成</figcaption>
</figure>

<div class="commentary">
此处可能会有系统环境变量（PATH）相关设置的提示，如果需要设置，可以这样操作：

1. 在系统的 <button class="btn gray mini"><img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/Logo/Windows_logo_2012-Black_16px.svg" height="16" alt="Win"/> 开始</button> 按钮上点击鼠标右键，点击 <span class="menutext">系统(Y)</span>；
2. 在弹出的窗口中点击窗口右侧的 <span class="menutext">系统信息</span>；
3. 在弹出的窗口中点击窗口左侧的 <span class="menutext">高级系统设置</span>；
4. 在弹出的窗口中点击 <span class="menutext">环境变量(N)...</span>；
5. 在“用户变量”区域双击“Path”；
6. 点击 <button class="btn gray mini">新建(N)</button>、<button class="btn gray mini">浏览(B)...</button> 添加需要的路径;
7. 依序点击 <button class="btn gray mini">确定</button> 完成设置。

</div>

启用了 Flake8 插件后，这段代码出现了多处报错（显示为黄色和红色的波浪线）：  
![制表符和空格对比报错](https://cdn.jsdelivr.net/gh/shen-huang/img@master/2019-08/Tab_and_Space_1.png)

混用了制表符和空格的代码，就算是看上去对齐了，也会报错：  
![制表符和空格对比报错](https://cdn.jsdelivr.net/gh/shen-huang/img@master/2019-08/Tab_and_Space_2.png)

把鼠标指针放到报错的地方，会有相应的错误提示：  
![制表符和空格对比报错提示](https://cdn.jsdelivr.net/gh/shen-huang/img@master/2019-08/Tab_and_Space_3.png)

其实，静态程序分析工具可以检查出的问题远不止缩进这一点点，错误的拼写、遗漏的符号、未定义的变量等等，都可以检查出来。有了这样的工具，就算是写代码的时候出了些差错，也不至于束手无策了。

### Markdown

[Markdown](https://daringfireball.net/projects/markdown/) 是[约翰・格鲁伯（John Gruber）](https://daringfireball.net/)为了能用易读易写的符号编写格式丰富的文档，在[亚伦・斯沃茨（Aaron Swartz）](http://www.aaronsw.com/)的帮助下开发的一种“[轻量级标记语言](https://zh.wikipedia.org/wiki/轻量级标记语言)”。

Markdown 实际上要解决的问题是“**内容的可读性和格式的丰富性的两难困境**”。

最简朴的文本文件可读性是最强的，但若是想要添加些格式——哪怕简单的强调（加粗）、引用（倾斜）——都很不方便；网络上常见的 HTML 文档可以呈现比较丰富的格式，但其中可能会充斥大量的结构标记或格式标记，这使得其直接阅读起来相对困难；[富文本格式（Rich Text Format，缩写为 RTF）](https://en.wikipedia.org/wiki/Rich_Text_Format)的文档也有相当丰富的格式，借助相应的软件对其进行编辑和阅读也很方便，但若是直接面对富文本格式文档的代码，那很可能让人头疼，如果其中包括非拉丁字符（比如中文字符），甚至会到达“人类不可读”的程度。

Markdown 则试图在内容和格式之间找到一个平衡点，它的策略是：借用了以往的电子邮件格式标记惯例（如用星号 `*` 表示强调）和 HTML 语言的现有实现，针对最常见的格式化需求，提供便于读写的语法，针对不大常用的格式化需求，则直接使用 HTML 代码，形成的文件实际上是文本文件，以 <span class="paths">.md</span> 的文件扩展名进行标记，文件编写时可使用任何文本编辑器，阅读时可直接观看原始代码或用相应工具转换成 HTML 文档后观看。

Markdown 的方案获得了巨大的成功，现在主要的网志平台基本上都接受 Markdown 格式，常见的源代码托管服务平台（如 GitHub）对 Markdown 的支持也很好，可使用 Markdown 格式的编程语言有十多种，在所有主要的计算机操作系统中都有设计优良的 Markdown 编辑器。

VS Code 对 Markdown 格式的支持度非常高，故而用 VS Code 编写 Markdown 格式文档是相当合适的。为了进一步提升编写体验，可以考虑安装一些相关扩展，如：

- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
- [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

Markdown All in One 提供了许多基础编辑功能，如快捷键、自动生成目录、自动生成/更新/删除章节序号、便捷的列表编辑、便捷的表格格式化、任务列表支持、自动完成等，完整的功能说明可以参考 [Markdown All in One 的官方主页](https://github.com/yzhang-gh/vscode-markdown)：[https://github.com/yzhang-gh/vscode-markdown](https://github.com/yzhang-gh/vscode-markdown)。

Markdown Preview Enhanced 提供了增强的即时预览、外部文件导入、多种格式导出、演示文稿生成、语法扩展、自定义样式、自动生成目录、<span class="texhtml" style="font-family: 'CMU Serif', cmr10, LMRoman10-Regular, 'Latin Modern Math', 'Nimbus Roman No9 L', 'Times New Roman', Times, serif;">L<span style="text-transform: uppercase; font-size: 57.851%; vertical-align: 0.205em; margin-left: -0.36em; margin-right: -0.15em; line-height: 0">a</span>T<span style="text-transform: uppercase; vertical-align: -0.2155em; margin-left: -0.125em; margin-right: -0.1667em; line-height: 0">e</span>X</span> 表达式渲染、多种类图形渲染等功能，官方还编写了相当完整的说明文档（[https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/)）以供参考。Markdown Preview Enhanced 强悍的地方更多地体现在本地编辑上，由于我现在主要是为了在 docsify 和 GitHub 上呈现内容而编写 Markdown 文档，故而我主要只用它来做侧边实时预览，并未使用其独有的特性功能。

markdownlint 与前文提到的 Flake8 类似，是一款针对 Markdown 文档的静态程序分析工具，安装后其即会开始对打开的 Markdown 文档进行分析并用波形下划线（﹏）标记出有问题的地方，相关的具体说明可以参考官方主页（[https://github.com/DavidAnson/vscode-markdownlint](https://github.com/DavidAnson/vscode-markdownlint)）和规则说明页（[https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md)）。默认的有些规则可能会带来一些麻烦，比如“[MD033 - 内联 HTML](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md#md033---inline-html)”就会标记出我为了语义正确而在 Markdown 文档中使用的所有 HTML 代码，这其实并无必要。要避免这些额外的提示，可以对其进行个性化处理：点击侧边的<button class="btn gray mini">管理</button>按钮，再点击 <span class="menutext">设置</span>（或使用快捷键 <kbd>Ctrl</kbd> + <kbd>,</kbd>）打开设置页面，然后点击 <span class="menutext">扩展</span> - <span class="menutext">markdownlint</span>，再在页面右侧点击 <span class="menutext">在 settings.json 中编辑</span> 打开设置文件。

我在设置文件中添加了如下内容，基本上略过了我现在可能遇到的非必要报错：

```json
"markdownlint.config": {
    "MD012": {"maximum": 2},
    "MD013": false,
    "MD033": {"allowed_elements": ["span", "div", "pre", "code", "p", "br", "a", "kbd", "button", "img", "figure", "figcaption", "blockquote", "cite", "footer", "u", "strong", "wbr"]},
    "MD034": false,
},
```

Code Spell Checker 提供了针对多种语言的“拼写检查”。将它启用后，可能是错误的英文单词下面会出现波形下划线，将光标移到标记出的单词处，按快捷键 <kbd>Ctrl</kbd> + <kbd>.</kbd> 就会弹出上下文菜单，提示可能正确的拼写，如果是地名、人名类，被错误标记了的专有名词，还可以选择 <span class="menutext">Add: "wrongword" to user dictionary</span> 将其添加到“用户词典”（对所有文档有效），或选择 <span class="menutext">Add: "wrongword" to workspace dictionary</span> 将其添加到“工作区词典”（对现在工作区中的文档有效）。

用户词典的设置在文件 <span class="paths">~\AppData\Roaming\Code\User\settings.json</span> 里，工作区词典的设置则在工作区的文件 <span class="paths">.vscode\settings.json</span> 里。我更倾向于将自定义的单词放在工作区词典，这样相对来说好控制影响范围，也便于备份。

Code Spell Checker 还可以加载其他的专门词典，比如德语、法语、俄语等等，具体的设置可以参考[官方页面](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)上的说明。

### Git

[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) 是搭配 Git 使用的一个重要的 VS Code 扩展，它增强了 VS Code 内置的 Git 功能，提供了作者显示、修改跟踪、仓库概览、历史查询、提交比较、提交搜索等等的功能。GitLens 安装完成后会自动弹出设置页面，通常情况下保持默认状态就可以了，我根据自己的习惯，把 <span class="menutext">Dates & Times</span> 区的日期格式设成了 `YYYY-MM-DD HH:mm:ss`，短日期格式设成了 `YYYY-MM-DD`。

GitLens 会在侧边添加一个自己的图标，点击之后会打开 GitLens 侧栏，在其中就可以方便地进行一系列的 Git 操作。GitLens 会主动提示文档的作者和修改时间，悬浮鼠标箭头还会弹出有着更详细内容的上下文菜单。

更具体的介绍可以参考[官方页面](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)上的说明。

![Visual Studio Code GitLens 扩展][Visual_Studio_Code_GitLens]

<!-- TODO -->

<!-- ### Excel Viewer -->

## VS Code 的其他设置

### VS Code 中 Python 的环境设置

如果已经安装了 Python 和 VS Code 的 Python 扩展，那么在 VS Code 的左下角会出现当前使用的 Python 环境的提示，点击即可进行相应设置。

![Visual Studio Code Python 环境设置][Visual_Studio_Code_Python_Env]

<!-- ### VS Code 中 Terminal 的选择设置 -->
<!-- ### VS Code 中的代理设置 -->

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
[Fira_Code_Arrow_Ligature]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Fira_Code_Arrow_Ligature.svg?sanitize=true
[Visual_Studio_Code_Fira_Code_HYQihei_16]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Fira_Code_HYQihei_16.png
[Visual_Studio_Code_Font_Settings]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Font_Settings.png
[Visual_Studio_Code_Extensions_Theme]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Theme.png
[Visual_Studio_Code_Extensions_Theme_Preview]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Extensions_Theme_Preview.png
[Visual_Studio_Code_Theme_and_Icons]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Theme_and_Icons.png
[Visual_Studio_Code_Python_extension]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_extension.png
[Visual_Studio_Code_Python_Env]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Env.png
[Visual_Studio_Code_Python_Select_Linter]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Python_Select_Linter.png
[Visual_Studio_Code_GitLens]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_GitLens.png

<!-- 
https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/

https://cdn.jsdelivr.net/gh/shen-huang/img@master
 -->

[Windows_Logo]: https://upload.wikimedia.org/wikipedia/commons/2/2b/Windows_logo_2012-Black.svg
[Windows_Logo_20px]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/20px-Windows_logo_2012-Black.svg.png
[Windows_Logo_16px_o]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/16px-Windows_logo_2012-Black.svg.png
[Windows_Logo_16px]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/Logo/Windows_logo_2012-Black_16px.svg?sanitize=true
[Windows_Logo_12px]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/Logo/Windows_logo_2012-Black_12px.svg?sanitize=true
[Windows_Logo_8px]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/Logo/Windows_logo_2012-Black_8px.svg?sanitize=true
[Windows_Logo_6px]: https://cdn.jsdelivr.net/gh/shen-huang/img@master/Logo/Windows_logo_2012-Black_6px.svg?sanitize=true

<!-- 链接 -->

[Visual Studio Code 的主页]: https://code.visualstudio.com/
[Chinese (Simplified) Language Pack for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans
[Slant]: https://www.slant.co/

<strong>参考资料</strong>

- [《让代码看起来更舒服（2）：选择适合的字体》，Windie Chai，2009-11-22。](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/)  <br>
  <!-- [http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/](http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/) -->
  <a href="http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/"><span class="paths">http://coding.windstyle.cn/make-your-code-more-comfortable-2-select-the-appropriate-font/</span></a>
- [What is the default serif, sans-serif and monospace font-family for Mac OS X? Jeff, 2012-08-24.](https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x)  <br>
  <!-- [https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x](https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x) -->
  <a href="https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x"><span class="paths">https://webmasters.stackexchange.com/questions/33793/what-is-the-default-serif-sans-serif-and-monospace-font-family-for-mac-os-x</span></a>
- [《CSS font-family 詳細介紹》，oxxo，2018-11-30。](https://www.oxxostudio.tw/articles/201811/css-font-family.html)  <br>
  <a href="https://www.oxxostudio.tw/articles/201811/css-font-family.html"><span class="paths">https://www.oxxostudio.tw/articles/201811/css-font-family.html</span></a>
- [《在 VSCode 中使用（汉字）等宽字体》，张慕晖，2018-11-19。](https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/)  <br>
  <a href="https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/"><span class="paths">https://zhanghuimeng.github.io/post/using-chinese-monospace-in-vscode/</span></a>
- [《获取中文字体的英文名字》，Xrated，2018-05-17。](https://zhuanlan.zhihu.com/p/36984949)  <br>
  <a href="https://zhuanlan.zhihu.com/p/36984949"><span class="paths">https://zhuanlan.zhihu.com/p/36984949</span></a>
- [《分享一下自己修改的字体~ Yahei Source Code Pro v1.23》，DeepKolos，2017-07-15。](https://www.jianshu.com/p/28acf9226ddb)  <br>
  <a href="https://www.jianshu.com/p/28acf9226ddb"><span class="paths">https://www.jianshu.com/p/28acf9226ddb</span></a>
- [YaHei Consolas Hybrid 和 Yahei Source Code Pro 的下载页面](https://github.com/yyxyz/OSOperateSkills/find/master)  <br>
  <a href="https://github.com/yyxyz/OSOperateSkills/find/master"><span class="paths">https://github.com/yyxyz/OSOperateSkills/find/master</span></a>
- [更纱黑体主仓库](https://github.com/be5invis/Sarasa-Gothic)  <br>
  <a href="https://github.com/be5invis/Sarasa-Gothic"><span class="paths">https://github.com/be5invis/Sarasa-Gothic</span></a>
- [Iosevka 字体主页](https://typeof.net/Iosevka/)  <br>
  <a href="https://typeof.net/Iosevka/"><span class="paths">https://typeof.net/Iosevka/</span></a>
