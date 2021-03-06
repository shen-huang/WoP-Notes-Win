# 随记

这里是一些我在学习过程中“注意力漂移”的记录。

## 2020-08-14

<!-- TODO -->

<!-- SVG 图片尺寸的修改，与 Windows Logo 有关 -->

## 2020-08-13

装了 Code Spell Checker 后报了一堆提示，基本上都是人名之类的，真正的拼写错误只有一处，还是我从其他地方引用来的内容。

不管也挺难看的，就花了不少时间挨个处理了。

相关的设置在工作区文件夹的 <span class="paths">.vscode\\settings.json</span> 中。主要包括

```json
{
    "cSpell.ignoreWords": [ ],
    "cSpell.words": [ ],
}
```

`"cSpell.ignoreWords"` 用来存放忽略掉的单词，`"cSpell.words"` 用来存放自定义的单词。

另外在 VS Code 的主配置中添加了字典相关的设置：

```json
{
    "cSpell.language": "en, fonts",
    "cSpell.languageSettings": [
        { "languageId": "*", "dictionaries": ["fonts"] }
    ],
}
```

Code Spell Checker 还引起了 VS Code 访问 [githubusercontent.com](githubusercontent.com) 域失败的警报，启用全局代理也没能把警报消除，好在 Clash for Windows 提供了 HTTP 代理，在 VS Code 的设置里把代理设成“<span class="paths">http://127.0.0.1:7890</span>”后问题就解决了。

**参考资料：**

- [《为 Visual Studio Code PC 客户端设置代理》，Qianying，2020-04-09。](https://suiahae.me/Set-proxy-for-Visual-Studio-Code-on-Windows/)

## 2020-08-12

[前几天（2020-08-06）](/a-appendix/jotting?id=_2020-08-06)调试引用表现的时候，明确了一下语义问题，当时我读到了 [Bryan Braun 的论述](https://stackoverflow.com/a/44951884/13891206)（翻译摘录如下）：

<figure class="quote">
  <!-- <blockquote style="letter-spacing: 0rem;"> -->
  <blockquote>
  在 HTML 中给图片添加标题的正确方法是使用 <a href="http://html5doctor.com/the-figure-figcaption-elements/"><code>&lt;figure&gt;</code> 和 <code>&lt;figcaption&gt;</code> 标签</a>。

  Markdown 中没有与此等价的语法，所以如果只是偶尔添加个标题，建议直接在 Markdown 文档中插入相应的 HTML 代码。这一方案比折腾插件要简单得多。

  如果试图用其他的 Markdown 功能（如表格、星号等）来制作标题，那只是在尝试绕过 Markdown 原本设计的使用方法罢了。  
  </blockquote>
</figure>

在此之前，我通过使用

```markdown
![图片名称](图片地址)

<div class="figtitle">图片标题</div>
```

的方式给图片添加了标题，效果虽然没有问题，语义上是不大经得起推敲的。今天又要插入带标题的图片，我就决定趁此机会把之前的图片相关代码都改掉。

好在不大复杂，用正则表达式搜索

```regex
^!\[\]\[(.*)\]\n\n<div class="figtitle">(.*)</div>
```

替换成

```regex
<figure class="image">\n  <img src="https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/$1.png" alt="$2"/>\n  <figcaption class="figtitle">$2</figcaption>\n</figure>
```

就完成了。

另外，之前标题区域由于单独把“来源”的文字设置成了浮动右对齐，会在页面较窄的情况下出现错误的漂浮换行现象，这次调整的时候通过在父元素的样式里设置 `overflow: auto;` 的方法把这个问题调整了一下。

相关的完整规则集为：

```css
.figtitle {
    position: relative;
    overflow: auto;
    z-index: 100;
    margin-top: -0.5rem;
    margin-bottom: 1rem;
    margin-left: 0;
    padding: 0 0 0 10px;
    border-left: 5px solid rgba(0, 0, 0, 0.3);
    background-color: #dddddd;
    font-family: var(--font-hei);
    font-size: 0.8rem;
    font-weight: normal;
    color: rgba(0, 0, 0, 0.7);
}

.figtitlevia {
    float: right;
    padding-right: 10px;
}

```


## 2020-08-11

[docsify][] 在对整段代码进行格式化的时候似乎会主动进行一些修订，比如把行首的制表符（<span class="unicode-number">U+0009</span> <span class="unicode-name">CHARACTER TABULATION</span>）自动替换成空格（<span class="unicode-number">U+0020</span> <span class="unicode-name">SPACE</span>），这在提升代码质量方面是有价值的，但在特意要搞错误示范的时候就带来了麻烦。

我本想通过在一段 Python 代码中混用制表符和空格来说明“静态程序分析工具”的必要性，但像下面这样撰写代码无法如愿：

<pre v-pre="" data-lang="markdown" class="language-markdown"><code class="lang-markdown language-markdown">```python
if True:
&#9;print("a")
else:
&#9;print("b")
    print("c")
```</code><button class="docsify-copy-code-button"><span class="label">点击复制</span><span class="error">错误</span><span class="success">已复制</span></button></pre>

成型的网页上制表符都被替换成了空格，完全无法表达我原本的意思。

我只好用浏览器的开发人员工具把 [PrismJS](https://prismjs.com) 处理过的 HTML 代码复制出来，然后用 `&#9;` 来实现在网页的代码区域呈现制表符的目的。类似这样：

```html
<pre v-pre="" data-lang="python" class="language-python">
<code class="lang-python language-python">
<span class="token keyword">if</span> <span class="token boolean">True</span><span class="token punctuation">:</span>
&#9;<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">)</span>
<span class="token keyword">else</span><span class="token punctuation">:</span>
&#9;<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"b"</span><span class="token punctuation">)</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"c"</span><span class="token punctuation">)</span>
</code>
<button class="docsify-copy-code-button">
  <span class="label">点击复制</span>
  <span class="error">错误</span>
  <span class="success">已复制</span>
</button>
</pre>
```

<span class="commentary">注：由于这里使用了 `<pre>` 来格式化代码内容，而 `<pre>` 会保留空格和换行符，故而不能为了美观在 HTML 代码层面再搞什么标签对齐了。</span>

## 2020-08-07

试了一下，感觉 [docsify][] 用来实现代码高亮的插件 [PrismJS](https://prismjs.com) 使用的关键字大小写不敏感，以往我看到它的[语言支持列表](https://prismjs.com/#supported-languages) 中列出来的关键字都是小写，就没敢用大写，今天用到 `HTML`，实在不习惯全小写的写法，就用了大写，发现可行，遂将所有的代码块关键字都改了一遍。

改完之后发现 `Python` 和 `python` 呈现的效果不一样，只有 `python` 的显示是正确的，我只好搜索：

```regex
```(.*)\n
```

将它们替换成：

```regex
```\L$1\n
```

把代码块的关键字又改回来了。

但最初闹心的事情还没有解决，我琢磨了一下，觉得如果这个位置没法做大小写区分的话，那我个人更偏好全大写，就在自定义的样式中添加了把代码标记显示成大写字母的规则：

```css
.markdown-section pre[data-lang]::after {
    text-transform: uppercase;
}
```

<span class="commentary">注：此处若使用 `text-transform: capitalize;` 把标记设置成首字母大写是不合适的，因为“HTML”、“CSS”、“RegEx”这样的名称，全小写尚可以说成是一种排版风格，写成“Html”、“Css”、“Regex”就显得有些不伦不类了。</span>

又调了一下代码块的复制按钮，让它显得轻巧了一点：

```css
body .docsify-copy-code-button {
    font-size: 0.8rem;
    font-family: var(--code-font-family);
}
```

## 2020-08-06

[docsify-themeable 主题][]中，引用默认的呈现方式是灰底左侧带主题色边框的一个块，类似这样——

<div
  style="
        overflow: visible;
        margin: 2em 0;
        padding: 1.5em;
        border-style: solid;
        border-color: var(--theme-color);
        border-width: 0 0 0 4px;
        border-radius: 0 var(--border-radius-m) var(--border-radius-m) 0;
        background: var(--mono-tint3);
        ">
    <p>docsify-themeable 主题默认的引用表现</p>
</div>

在对主题整体做了比较大的调整之后，这个效果看上去感觉不大协调，遂着手修改。

研究了一下现有的样式，明确引用实际上是用 `<blockquote>` 包起来的一个块，它的大部分属性都挺好理解的，只是其中有一个 `quotes` 我没看明白，就 Google 了一下“blockquote quotes”。我首先被 [Jake Rocheleau](https://jakerocheleau.com/) 在 2018 年 9 月 3 日发布的[《10 Simple CSS Snippets for Creating Beautiful Blockquotes》](https://1stwebdesigner.com/css-snippets-blockquotes/)一文吸引了，把文中所有的链接都点开看了一下，其中 Derek Wheelden 的 [Blockquote Patterns](https://codepen.io/frxnz/pen/IvBCr)、Harm Putman 的 [Simple Block](https://codepen.io/harmputman/pen/IpAnb)、Lukas Dietrich 的 [Raised Blockquote](https://codepen.io/lukasdietrich/pen/KLJjy) 都比较和我的心意，我就结合了 [Blockquote Patterns](https://codepen.io/frxnz/pen/IvBCr) 的第一个和第三个案例折腾了一阵子，弄出来了一个这样的效果——

> 常见的  
> **多行**  
> 引用文本
>
> 以及可能包含中文、*English*、平仮名（ひらがな）、片仮名（カタカナ）、<span style="font-family: 'Times New Roman'; font-style: italic;">ру́сский язы́к</span>、עִבְרִית‬ 等多种文字，来自政界、学界、军界、文化界、艺术界等领域的各类人士，长达数行甚至数个段落的观点、论辩、评价等内容。
> <footer>及其<a href="#">来源</a></footer>

<br>
相关的代码为：

```markdown
> 常见的  
> **多行**  
> 引用文本
>
> 以及可能包含中文、*English*、平仮名（ひらがな）、片仮名（カタカナ）、<span style="font-family: 'Times New Roman'; font-style: italic;">ру́сский язы́к</span>、עִבְרִית‬ 等多种文字，来自政界、学界、军界、文化界、艺术界等领域的各类人士，长达数行甚至数个段落的观点、论辩、评价等内容。
> <footer>及其<a href="#">来源</a></footer>
```

跟着，我又读到了 [John Rhea](https://johnrhea.com/) 在 2019 年 12 月 10 日发布的[《Quoting in HTML: Quotations, Citations, and Blockquotes》](https://css-tricks.com/quoting-in-html-quotations-citations-and-blockquotes/)一文，其中详解了 `<blockquote>` 相关的各类用法，还强调了一个值得注意的事情：**语义**。按照该文的意见，使用 `<cite>` 来标记引文来源是不合语义的，`<cite>` [应该用来标明**作品**（如书籍，论文，文章，诗词，乐谱，歌曲，剧本，电影，电视节目，游戏，雕塑，画作，舞台剧，戏剧，歌剧，音乐剧，展览，法律案件报告​​，计算机程序等）的**标题**，而非作者](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-cite-element)。以此类推，`<footer>` [应该用来标记页脚](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer)，用它来标记引文来源也不是很合适，[MDN Web Docs](https://developer.mozilla.org/zh-CN/) 里 `<blockquote>` 的[范例](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/blockquote)也有点问题。

按照[《Quoting in HTML: Quotations, Citations, and Blockquotes》](css-tricks.com/quoting-in-html-quotations-citations-and-blockquotes/)中的建议，语义健康的引文标记应该采用这样的写法：

```html
<figure class="quote">
  <blockquote>
    But web browsers aren’t like web servers. If your back-end code is getting so big that it’s starting to run noticeably slowly, you can throw more computing power at it by scaling up your server. That’s not an option on the front-end where you don’t really have one run-time environment—your end users have their own run-time environment with its own constraints around computing power and network connectivity.
  </blockquote>
  <figcaption>
    &mdash; Jeremy Keith, <cite>Mental models</cite>
  </figcaption>
</figure>
```

在 [Stack Overflow][] 上与此话题相关的一个讨论 [“Using an image caption in Markdown Jekyll”](https://stackoverflow.com/questions/19331362/using-an-image-caption-in-markdown-jekyll) 中，[Bryan Braun](https://www.bryanbraun.com/) 在 2017 年 7 月 6 日也对类似的问题给出了逻辑清晰的“应该使用 `<figure>` 和 `<figcaption>`” 的说明——

<figure class="quote">
  <blockquote style="letter-spacing: 0rem;">
  The correct HTML to use for images with captions, is <a href="http://html5doctor.com/the-figure-figcaption-elements/"><code>&lt;figure&gt;</code> with <code>&lt;figcaption&gt;</code></a>.

  There's no Markdown equivalent for this, so if you're only adding the occasional caption, I'd encourage you to just add that HTML into your Markdown document:

  ```html
  Lorem ipsum dolor sit amet, consectetur adipiscing elit...

  <figure>
    <img src="{{site.url}}/assets/image.jpg" alt="my alt text"/>
    <figcaption>This is my caption text.</figcaption>
  </figure>

  Vestibulum eu vulputate magna...
  ```

  [The Markdown spec encourages you to embed HTML in cases like this](https://daringfireball.net/projects/markdown/syntax#html), so it will display just fine. It's also a lot simpler than messing with plugins.

  If you're trying to use other Markdown-y features (like tables, asterisks, etc) to produce captions, then you're just hacking around how Markdown was intended to be used.

  </blockquote>
  <figcaption> Bryan Braun, in <cite style="font-style: italic;"><a href="https://stackoverflow.com/a/44951884/13891206">Stack Overflow</a></cite>
  </figcaption>
</figure>

我因此又去调了一阵子样式，将 `<footer>` 切换成了 `<figcaption>`。

将来如果要在文章中快速地引用一段话，还是可以用 Markdown 的 `>` 语法，但若是要写出处，就得写成这样：

```markdown
<figure class="quote">
  <blockquote>
  引用内容。
  </blockquote>
  <figcaption>
  作者，<cite>出处</cite>
  </figcaption>
</figure>
```

好在 `<blockquote>` 都不是块级元素，所以在其中夹杂 Markdown 语法也行得通，不过若是要在 `<figure>` 里直接写内容或者是给 `<figcaption>` 标记的来源加链接，就得直接用 HTML 标签来写了：

```markdown
<figure class="quote">
  <blockquote>
  引用内容。  

  链接：  
  [链接名称](https://example.com)

  图片：  
  ![Octocat](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

  Windows 键：  
  <kbd>![Win][Windows_Logo_12px] Win</kbd>

  行间代码：`<html>`

  插入块状代码：

  `​`​`python
  print("Hello World!")
  `​`​`

  <br>
  </blockquote>
  <figcaption><a href="#">作者</a>，<cite><a href="#">出处</a></cite>
  </figcaption>
</figure>
```

<span class="commentary">注：本段代码出现了两层 <code>&grave;​&grave;​&grave;</code> 的嵌套，不处理的话会出现错误，为了令其正常显示，在内层 <code>&grave;​&grave;​&grave;</code> 的字符间插入了[零宽空格](https://zh.wikipedia.org/zh-hans/零宽空格)（<span class="unicode-number">U+200B</span> <span class="unicode-name">ZERO WIDTH SPACE</span>）。<br>
另外，想要给三个抑音符（<span class="unicode-number">U+0060</span> &grave;​ <span class="unicode-name">GRAVE ACCENT</span>）添加代码样式也是个麻烦事，因为不能直接写“<code>&grave;​&grave;​&grave;&grave;​&grave;</code>”，它显示出来会是“`````”这样，这里只靠 Markdown 是搞不定的，得直接用 HTML，写成 <code>&lt;code&gt;&amp;grave;​&amp;grave;​&amp;grave;&lt;/code&gt;</code> 才行。</span>

它呈现出来是这个样子：

<figure class="quote">
  <blockquote>
  引用内容。  

  链接：  
  [链接名称](https://example.com)

  图片：  
  ![Octocat](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

  Windows 键：  
  <kbd>![Win][Windows_Logo_12px] Win</kbd>

  行间代码：`<html>`

  块状代码：

  ```python
  print("Hello World!")
  ```

  <br>
  </blockquote>
  <figcaption><a href="#">作者</a>，<cite><a href="#">出处</a></cite>
  </figcaption>
</figure>

随后我又参考 [Raised Blockquote](https://codepen.io/lukasdietrich/pen/KLJjy) 给引用加了一个鼠标悬停的阴影效果，感觉可以告一段落，踏实用了。

**参考资料：**

- [Quoting in HTML: Quotations, Citations, and Blockquotes. John Rhea, 2019-12-10.](https://css-tricks.com/quoting-in-html-quotations-citations-and-blockquotes/)  
  <a href="https://css-tricks.com/quoting-in-html-quotations-citations-and-blockquotes/"><span class="paths">https://css-tricks.com/quoting-in-html-quotations-citations-and-blockquotes/</span></a>
- [10 Simple CSS Snippets for Creating Beautiful Blockquotes. Jake Rocheleau, 2018-09-03.](https://1stwebdesigner.com/css-snippets-blockquotes/)  
  <a href="https://1stwebdesigner.com/css-snippets-blockquotes/"><span class="paths">https://1stwebdesigner.com/css-snippets-blockquotes/</span></a>

## 2020-08-05

被点名了，于是写了挺长的一个回答，解释我为什么买了[三星 48.8英寸 曲面超宽显示器 C49RG90SSC](https://www.samsung.com/cn/monitors/monitor-c49rg90ssc/)。

<strong>今日话题: #让你感到显著提升工作效率(或生活质量)的物品#</strong>

我来分享一个我近期部署的好物：三星 48.8英寸 曲面超宽显示器 C49RG90SSC。

![三星 48.8英寸 曲面超宽显示器 C49RG90SSC](https://images.samsung.com/is/image/samsung/cn-feature-monitor-c49rg90ssc-153239166)

我大概从 2010 年开始使用双屏工作，一用就停不下来了——更多的屏幕面积减少了在可能的多个任务间的切换次数，从而明显地提升了效率。

很多人对“更多的屏幕”不以为然，这些人看到那些用双屏工作的人通常都表示“不理解”，认为“没必要”，甚至批评“装”。为了解释这个问题，我在这里稍微多写一点。

我们在计算机上工作的时候，常常会有在多个程序间切换的需求。比如，为了做好一个演示文稿，可能会同时打开数个文档、表格、网页，在其中挑拣自己需要的素材，在只有一个屏幕的时候，我们可能因为可用屏幕空间的限制，一次只看一个窗口的内容，就算是想办法平摊开，两三个窗口就很挤了，四个窗口差不多就是上限了。在这种现实中，我们会不得已地“反复在多个窗口中切换”，或者“调整软件所显示的区域”，这会显著地消耗大脑的“任务切换耗散（switching costs）”，继而出现效率降低。如果有两个屏幕，那一次看两个窗口就是常态，看三四个也不会太挤，一次看到的内容往往也比较宽裕，任务切换的次数也就可以降低一些，效率也就会有一定量的提升。

有趣的一点是，同样是面对任务切换消耗脑力的问题，有些人选择了另外一条路：主动不切换。

这个方案的核心是“一次只做一件事”，同样是做演示文稿的工作，不切换的人，选择的方法可能是这样：

1. 纸笔列出大纲；
2. 纸笔设计出演示文稿的主要内容；
3. 确定需要的文字内容并做相应整理；
4. 确定需要的图片内容并做相应整理；
5. 确定需要的图表内容并做相应整理；
6. 按照纸笔框架制作演示文稿，先处理文字，再插入图片和图表，最后整体调整。

这个方案可行吗？当然可行，它甚至还挺高效的，但它并不会影响“更多的屏幕会提升效率”这个论断。

考虑一下，在插入图片的时候，如果只有一个屏幕，那么可能是这么几种情况：

- 演示文稿软件窗口最大化，文件管理器窗口最大化
  1. 在文件管理器里选择图片
  2. 把图片拖到任务栏的演示文稿软件图标上做切换
  3. 把图片拖进演示文稿软件
- 演示文稿软件窗口最大化，文件管理器窗口最大化
  1. 在文件管理器里选择图片，复制
  2. 切换到演示文稿软件，粘贴
- 演示文稿软件窗口占一半，文件管理器窗口占一半
  1. 在文件管理器里选择图片，拖动到演示文稿软件

很明显，在演示文稿软件和文件管理器各占一半的情境中，步骤最少，效率也就最高。

如果多了一个屏幕呢？那就可以演示文稿软件和文件管理器各占一个屏幕了，演示文稿会变得更大更容易调整，文件管理器一次也能显示出更大或更多的图片，无论是制作还是调整，都会更轻松。

综合来讲，**无论是要做那种“灵活性比较强”的任务，还是要做那种“稳定性比较强”的任务，更多的屏幕都会带来好处。**

由于技术、资金、空间等等限制，我的屏幕面积是慢慢增加的，第二个屏幕最初是 17 英寸，然后换成 19 英寸、24 英寸、27 英寸。我的一个好友曾经花了挺大的篇幅和我论证了一下“显示器多大就足够了”，他的参考要素是“人眼可以掌控的范围”，最后结论是“在一般使用计算机的场景中，人和显示器的距离差不多就是半米到一米，此时人眼一次只能最多也就能看到 24 英寸面积的内容，所以更大的显示器没必要了，更多的面积也看不过来”。我觉得他说得有些道理，我也没那么富裕，就在了 27 英寸（比“最大”再大一点）这个尺寸上停留了很久。

直到 2019 年我才意识到问题——**“人眼可以掌控的范围”是有限的，但“大脑可以掌控的范围”是宽广的啊，我们会摊一桌子书本资料对照着看，没道理到了显示器上就不能这么做了。**

想明白之后，我就打算搞个更大的显示器，用以适配我“宽广的大脑”。

做了一系列功课，又关注了一阵子价格，我在一个购物节入手了“三星 48.8英寸 曲面超宽显示器”。这台显示器宽 1199.5mm，高 369.4mm，屏幕比例 32:9，它其实就相当于两台 16:9 的 27 英寸显示器横向拼起来。我在下手前还纠结了一阵子：为什么不买两台 27 英寸的显示器？最大的区别就是中间的那个缝，那个缝很关键吗？到手之后我明确了答案：那个缝挺关键的，而且，并不只是那个缝的事。

![三星 48.8英寸 曲面超宽显示器 C49RG90SSC 正视图](https://images.samsung.com/is/image/samsung/cn-monitor-c49rg90ssc-lc49rg90sscxxf-silver-153239098)

同样的面积，两台显示器会比一台多用一个显示输出端口，这在便携式计算机上挺重要的。操作系统对“两台显示器”的处理和“一台显示器”也不一样，在一台显示器上，窗口怎么拉伸都没问题，若是两台显示器，拉伸过那个“中缝”就比较麻烦。

有了这台显示器之后，我调整了 Windows 平台上常见的“最大化”习惯，把各种软件都摊开放了。现在，我并排放四五个网页那么多的内容，同时写东西，也不会挤。

最后再说一点细节。这显示器的价格通常在 8000 元人民币左右，贵的时候能到 9000 元，我在购物节加上各种折扣、返利、券，到手花了 6900 多元，这费用还是挺高的。它占的地方也不小，配上底座之后宽 × 高 × 深到达了 1199.5 × 523.1 × 349.7&nbsp;(mm)，没有足够的空间用起来会比较难受。它的分辨率为 5120 × 1440，这对显卡也有些压力，性能一般的计算机带起来可能会有些吃力。如果想入手，一定要明确资金、空间、配套的情况，避免“把好事办坏了”。

**参考资料：**

- Duncan, John. “The locus of interference in the perception of simultaneous stimuli.” *Psychological Review* 87.3 (1980): 272.
- Philipp, Andrea M., et al. “Mixing costs and switch costs when switching stimulus dimensions in serial predictions.” *Psychological Research* 72.4 (2008): 405-414.
- 三星, "48.8英寸 曲面超宽显示器 C49RG90SSC", [2020-08-05], <a href="https://www.samsung.com/cn/monitors/monitor-c49rg90ssc/"><span class="paths">https://www.samsung.com/cn/monitors/monitor-c49rg90ssc/</span></a>.
- OwlLite, “‘同时处理多个任务’对大脑来说难在哪里？”, 2015-11-12, <a href="https://www.zhihu.com/question/37131977/answer/71781000"><span class="paths">https://www.zhihu.com/question/37131977/answer/71781000</span></a>.

## 2020-08-04

我在撰写内容的时候，为了明确某些链接的具体指向，提供了链接的原始字符，观看页面的时候，觉得这些文字使用代码样式更合适些，就改用了“`<a>`”标签和“`<span>`”标签来写这些链接，改了两个，步骤太繁琐了，遂使用正则表达式进行了批量修改。

<!-- 
例如
- [Be careful what you copy: Invisibly inserting usernames into text with Zero-Width Characters. Tom Ross, 2018-04-03.](https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66)  
  [https://link.medium.com/zKcoNeBPy8](https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66)
 -->

搜索内容：

```regex
\[(http.*)\]\((http.*)\)
```

替换内容：

```regex
<a href="$1"><span class="paths">$2</span></a>
```

## 2020-08-02

经过了数次尝试，感觉正文使用思源宋体还不错的，就把主字体切换成了思源宋体，进一步编辑的时候觉得有点问题：

- “强调”的内容看上去不大明显；
- 图表的题目字号较小，应考虑使用无衬线体；
- 按钮、菜单、快捷键不够鲜明，应考虑使用无衬线体。

参考 [Zeno Zeng](https://blog.zenozeng.com/) 在 2018 年 3 月 11 日发布的[《Fonts.css——跨平台中文字体解决方案》](https://zenozeng.github.io/fonts.css/)，我向自定义的样式中添加了不同风格字体的规则集：

```css
:root {
    --font-hei: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Helvetica, "Nimbus Sans L", Arial, "Liberation Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "PingFang SC", "Hiragino Sans GB", "Noto Sans SC", "Source Han Sans CN", "Source Han Sans SC", "Microsoft YaHei", "Wenquanyi Micro Hei", "WenQuanYi Zen Hei", "ST Heiti", SimHei, "WenQuanYi Zen Hei Sharp", sans-serif;
    --font-song: "Noto Serif", Georgia, "Nimbus Roman No9 L", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Serif SC", "Songti SC", STSong, "AR PL New Sung", "AR PL SungtiL GB", NSimSun, SimSun, "TW\-Sung", "WenQuanYi Bitmap Song", "AR PL UMing CN", "AR PL UMing HK", "AR PL UMing TW", "AR PL UMing TW MBE", PMingLiU, MingLiU, serif;
    --font-kai: Baskerville, Georgia, "Liberation Serif", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Kaiti SC", STKaiti, "AR PL UKai CN", "AR PL UKai HK", "AR PL UKai TW", "AR PL UKai TW MBE", "AR PL KaitiM GB", KaiTi, KaiTi_GB2312, DFKai-SB, "TW\-Kai", serif;
    --font-fangsong: Baskerville, "Times New Roman", "Liberation Serif", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", STFangsong, FangSong, FangSong_GB2312, "CWTEX\-F", serif;
}

.font-hei {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Helvetica, "Nimbus Sans L", Arial, "Liberation Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "PingFang SC", "Hiragino Sans GB", "Noto Sans SC", "Source Han Sans CN", "Source Han Sans SC", "Microsoft YaHei", "Wenquanyi Micro Hei", "WenQuanYi Zen Hei", "ST Heiti", SimHei, "WenQuanYi Zen Hei Sharp", sans-serif;
}
.font-song {
    font-family: "Noto Serif", Georgia, "Nimbus Roman No9 L", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Serif SC", "Songti SC", STSong, "AR PL New Sung", "AR PL SungtiL GB", NSimSun, SimSun, "TW\-Sung", "WenQuanYi Bitmap Song", "AR PL UMing CN", "AR PL UMing HK", "AR PL UMing TW", "AR PL UMing TW MBE", PMingLiU, MingLiU, serif;
}
.font-kai {
    font-family: Baskerville, Georgia, "Liberation Serif", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Kaiti SC", STKaiti, "AR PL UKai CN", "AR PL UKai HK", "AR PL UKai TW", "AR PL UKai TW MBE", "AR PL KaitiM GB", KaiTi, KaiTi_GB2312, DFKai-SB, "TW\-Kai", serif;
}
.font-fang-song {
    font-family: Baskerville, "Times New Roman", "Liberation Serif", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", STFangsong, FangSong, FangSong_GB2312, "CWTEX\-F", serif;
}
```

之后调整了标题的样式：

```css
:root {
    --heading-h1-font-size              : var(--font-size-xxl);
    --heading-h1-font-weight            : bold;
    --heading-h2-font-size              : var(--font-size-xl);
    --heading-h2-font-weight            : 600;
    --heading-h3-font-size              : var(--font-size-l);
    --heading-h3-font-weight            : 600;
}
```

按键的样式：

```css
kbd, .markdown-section kbd {
    font-family: -apple-system, BlinkMacSystemFont, "Helvetica Neue", Helvetica, "Nimbus Sans L", Arial, "Liberation Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "PingFang SC", "Hiragino Sans GB", "Noto Sans SC", "Source Han Sans CN", "Source Han Sans SC", "Microsoft YaHei", "Wenquanyi Micro Hei", "WenQuanYi Zen Hei", "ST Heiti", SimHei, "WenQuanYi Zen Hei Sharp", sans-serif;
    box-shadow: 0px 2px 0px 0px rgba(0,0,0,0.2);
}
```

图表标题的样式：

```css
.figtitle {
    position: relative;
    z-index: 100;
    margin-top: -1.65em;
    margin-bottom: 1em;
    margin-left: 0;
    padding: 2px 0 2px 10px;
    border-left: 5px solid rgba(0, 0, 0, 0.3);
    background-color: #dddddd;
    font-family: var(--font-hei);
    font-size: 0.9em;
    font-weight: normal;
    color: rgba(0, 0, 0, 0.7);
}
```


## 2020-08-01

发现了一个使用零宽字符（零宽空格、零宽连字、零宽不连字）在文章中藏匿信息的方法，具体操作可见 Jad 在 2018 年 4 月 13 日发布的[《我仔细看了半天，才从字缝里看出字来……》](https://imjad.cn/archives/code/hide-text-typecho-plugin/)一文。

另外明确了一下，不要使用“H5”来简称“HTML5”，细节可见 [JS小组](https://weibo.com/baidujs) 在 2015 年 7 月 5 日发布的[《为何不要用「h5」这个简称？》](https://mp.weixin.qq.com/s/AZ4gKhPRmIV2poHgURbVYA)一文。

**参考资料：**

- [Be careful what you copy: Invisibly inserting usernames into text with Zero-Width Characters. Tom Ross, 2018-04-03.](https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66)  
  <a href="https://link.medium.com/zKcoNeBPy8"><span class="paths">https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66</span></a>

## 2020-07-31

想在网页上用 Fira Code、Noto Sans SC、Noto Serif SC 这几种字体，常规方案是用 [Google Fonts](https://fonts.google.com/) 导入，按照现在的情况，使用中国大陆地区的 DNS 解析 Google Fonts 链接会指向中国大陆地区的服务器，但我还是感觉比较悬，不敢直接就这么用。

做了一阵子功课，发现郭秀峰（[Showfom](github.com/Showfom)，又被称作“兽兽”）的捷速网络运营的 CDN 服务 [loli.net](https://loli.net/) 有 Google Fonts 的加速业务，只需要把链接里的 `fonts.googleapis.com` 替换为 `fonts.loli.net` 即可使用。

具体示例——

原始链接：

```html
<link href='https://fonts.googleapis.com/css?family=Open+Sans' rel='stylesheet'>
```

加速链接：

```html
<link href='https://fonts.loli.net/css?family=Open+Sans' rel='stylesheet'>
```

我另外阅读了 Harry Roberts 在 2020 年 5 月 19 日撰写的《[最快的 Google Fonts](https://cloud.tencent.com/developer/news/643958)（[The Fastest Google Fonts](https://csswizardry.com/2020/05/the-fastest-google-fonts/)）》一文，Harry Roberts 经过了一系列的测试，建议使用如下代码段提升使用了 Google Fonts 的网页的性能：

```html
<!--
  - 1. Preemptively warm up the fonts’ origin.
  -
  - 2. Initiate a high-priority, asynchronous fetch for the CSS file. Works in
  -    most modern browsers.
  -
  - 3. Initiate a low-priority, asynchronous fetch that gets applied to the page
  -    only after it’s arrived. Works in all browsers with JavaScript enabled.
  -
  - 4. In the unlikely event that a visitor has intentionally disabled
  -    JavaScript, fall back to the original method. The good news is that,
  -    although this is a render-blocking request, it can still make use of the
  -    preconnect which makes it marginally faster than the default.
  -->
<!-- [1] -->
<link rel="preconnect"
      href="https://fonts.gstatic.com"
      crossorigin />
<!-- [2] -->
<link rel="preload"
      as="style"
      href="$CSS&display=swap" />
<!-- [3] -->
<link rel="stylesheet"
      href="$CSS&display=swap"
      media="print" onload="this.media='all'" />
<!-- [4] -->
<noscript>
  <link rel="stylesheet"
        href="$CSS&display=swap" />
</noscript>
```

<span class="commentary">上面代码中的 `$CSS` 在使用时要替换成类似于 `https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400;1,700` 这样的实例。</span>

我需要使用的代码是：

```html
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap" rel="stylesheet">
```

配套的样式为：

```css
font-family: 'Fira Code', monospace;
font-family: 'Noto Sans SC', sans-serif;
font-family: 'Noto Serif SC', serif;
```

搭配上 loli.net 的 CDN，按照 Harry Roberts 建议，可以把代码写成：

```html
<link rel="preconnect" href="https://gstatic.loli.net" crossorigin>
<link rel="preload" as="style" href="https://fonts.loli.net/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap">
<link rel="stylesheet" href="https://fonts.loli.net/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap" media="print" onload="this.media='all'">
<noscript>
  <link rel="stylesheet" href="https://fonts.loli.net/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap">
</noscript>
```

中国科技大学也做了 Google Fonts 的代理服务，具体对应关系为：

| 原始地址 | 代理地址 |
| -------- | -------- |
| fonts.googleapis.com         | fonts.lug.ustc.edu.cn
| ajax.googleapis.com          | ajax.lug.ustc.edu.cn
| themes.googleusercontent.com | google-themes.lug.ustc.edu.cn
| fonts.gstatic.com            | fonts-gstatic.lug.ustc.edu.cn

故也可使用如下代码对 Google Fonts 实施加速：

```html
<link rel="preconnect" href="fonts-gstatic.lug.ustc.edu.cn" crossorigin>
<link rel="preload" as="style" href="https://fonts.lug.ustc.edu.cn/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap">
<link rel="stylesheet" href="https://fonts.lug.ustc.edu.cn/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap" media="print" onload="this.media='all'">
<noscript>
  <link rel="stylesheet" href="https://fonts.lug.ustc.edu.cn/css2?family=Fira+Code:wght@300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Noto+Sans+SC:wght@100;300;400;500;700;900&family=Noto+Serif+SC:wght@200;300;400;500;600;700;900&display=swap&display=swap">
</noscript>
```

**参考资料：**

- [《前端 CDNJS 库及 Google Fonts、Ajax 和 Gravatar 国内加速服务》，郭秀峰，2018-08-18。](https://sb.sb/blog/css-cdn/)  
  <a href="https://sb.sb/blog/css-cdn/"><span class="paths">https://sb.sb/blog/css-cdn/</span></a>
- [《最快的 Google Fonts》，Harry Roberts，王强译，2020-05-19。](https://cloud.tencent.com/developer/news/643958)  
  <a href="https://www.infoq.cn/article/FVV9eEYjr3F8Tov2qYqP"><span class="paths">https://www.infoq.cn/article/FVV9eEYjr3F8Tov2qYqP</span></a>
- [《国内外优秀前端 CDN，Google Fonts 国内镜像》，占奇，2017-04-25。](https://zhanqi.net/post/170425/)  
  <a href="https://zhanqi.net/post/170425/"><span class="paths">https://zhanqi.net/post/170425/</span></a>
- [《LUG@USTC Google Fonts 加速服务》，杨博远，2014-12-17。](https://lug.ustc.edu.cn/wiki/lug/services/googlefonts)  
  <a href="https://lug.ustc.edu.cn/wiki/lug/services/googlefonts"><span class="paths">https://lug.ustc.edu.cn/wiki/lug/services/googlefonts</span></a>
- [《Google 字体加速添加缓存》，高一凡，2015-09-24。](https://servers.ustclug.org/2015/09/google-revproxy-add-cache/)  
  <a href="https://servers.ustclug.org/2015/09/google-revproxy-add-cache/"><span class="paths">https://servers.ustclug.org/2015/09/google-revproxy-add-cache/</span></a>
- [《隆重介绍 思源黑体：一款Pan-CJK 开源字体》，Caleb Belohlavek，2014-07-15。](https://blog.typekit.com/alternate/source-han-sans-chs/)  
  <a href="https://blog.typekit.com/alternate/source-han-sans-chs/"><span class="paths">https://blog.typekit.com/alternate/source-han-sans-chs/</span></a>
- [《Source Han Serif 思源宋体：开源的泛 CJK 字体》，Adobe Systems Incorporated，2017。](https://source.typekit.com/source-han-serif/cn/)  
  <a href="https://source.typekit.com/source-han-serif/cn/"><span class="paths">https://source.typekit.com/source-han-serif/cn/</span></a>
- [《关于如何在网页中引入思源字体：漫谈 Typekit》，Jad，2018-07-02。](https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/)  
  <a href="https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/"><span class="paths">https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/</span></a>
- [《走近 90 后创业者》，若涵，2014-03-28。](http://tech.sina.com.cn/i/special/startup90/)  
  <a href="http://tech.sina.com.cn/i/special/startup90/"><span class="paths">http://tech.sina.com.cn/i/special/startup90/</span></a>

## 2020-07-30

查资料的时候意外（又）注意到了 jsDelivr，研究了一下，了解到它可以给任何 GitHub 上不超过 20 MB 的文件提供免费的 CDN 加速。

比如说，要用 jsDelivr 给 GitHub 上的某张图片加速，只需要使用 <span class="paths">https://cdn.jsdelivr.net/gh/用户名/图床仓库名/图片路径</span> 引用这张图片就行了。

一个具体的例子——

GitHub 的原始链接是这样的：

<span class="paths">https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Main_page.png</span>

对应的 jsDelivr 的加速链接则是这个：

<span class="paths">https://cdn.jsdelivr.net/gh/shen-huang/img/2020-07/Visual_Studio_Code_Main_page.png</span>

或者添加了版本的这个：

<span class="paths">https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Main_page.png</span>

如果设置了 Release 的版本，还可以引用对应版本的文件。

**参考资料：**

- [《GitHub + jsDelivr + PicGo 打造稳定快速、高效免费图床》，TRHX，2019-08-01。](https://www.itrhx.com/2019/08/01/A27-image-hosting/)  
  <a href="https://www.itrhx.com/2019/08/01/A27-image-hosting/"><span class="paths">https://www.itrhx.com/2019/08/01/A27-image-hosting/</span></a>
- [《用 GitHub + PicGo + jsDelivr 打造高效的写作工作流，发布全平台》，Mask，2020-01-11。](https://www.jianshu.com/p/a78f558a74dc)  
  <a href="https://www.jianshu.com/p/a78f558a74dc"><span class="paths">https://www.jianshu.com/p/a78f558a74dc</span></a>
- [《记一下 jsDelivr 踩的坑》，石运鸿，2020-03-15。](https://blog.shiyunhong.com/3353.html)  
  <a href="https://blog.shiyunhong.com/3353.html"><span class="paths">https://blog.shiyunhong.com/3353.html</span></a>
- [《jsdelivr 加速资源加载：raw.github 被 ban 之后如何访问 GitHub 资源》，单林敏，2020-03-12。](https://blog.csdn.net/neve_give_up_dan/article/details/104817638)  
  <a href="https://blog.csdn.net/neve_give_up_dan/article/details/104817638"><span class="paths">https://blog.csdn.net/neve_give_up_dan/article/details/104817638</span></a>

## 2020-07-29

研究了一下 Jekyll、Hexo、Hugo，考虑将来用 Hugo 搭个 Blog。

**参考资料：**

- [《Jekyll / Hugo / Hexo 比较》，曹历鑫，2019-10-30。](https://lexcao.github.io/zh/posts/jekyll-hugo-hexo)  
  <a href="https://lexcao.github.io/zh/posts/jekyll-hugo-hexo"><span class="paths">https://lexcao.github.io/zh/posts/jekyll-hugo-hexo</span></a>
- [Hugo Themes](https://themes.gohugo.io)  
  <a href="https://themes.gohugo.io"><span class="paths">https://themes.gohugo.io</span></a>

<!-- 
Fox.ONE 的大群机器人新增了视频直播回看的功能，我看了一下源代码，发现视频是 blob 加密的，好在可以直接打开开发工具、刷新页面、从 Network 分页里搜索“m3u8”找到原始链接，跟着用个 M3U8 的下载工具（我用的是稞麦）下载就行了。

**参考资料：**

- [《下载blob加密的视频以及m3u8下载姿势合集》，yamakuchi，2019-05-11。](https://zhuanlan.zhihu.com/p/65425801)  
  <a href="https://zhuanlan.zhihu.com/p/65425801"><span class="paths">https://zhuanlan.zhihu.com/p/65425801</span></a>
- [《下载 blob视频, 如何下载网站中的blob:https:// 视频》，Gideon，2019-10-04。](https://justcode.ikeepstudying.com/2019/10/%E4%B8%8B%E8%BD%BD-blob%E8%A7%86%E9%A2%91-%E5%A6%82%E4%BD%95%E4%B8%8B%E8%BD%BD%E7%BD%91%E7%AB%99%E4%B8%AD%E7%9A%84blobhttps-%E8%A7%86%E9%A2%91/)  
  <a href="https://justcode.ikeepstudying.com/2019/10/下载-blob视频-如何下载网站中的blobhttps-视频/"><span class="paths">https://justcode.ikeepstudying.com/2019/10/%E4%B8%8B%E8%BD%BD-blob%E8%A7%86%E9%A2%91-%E5%A6%82%E4%BD%95%E4%B8%8B%E8%BD%BD%E7%BD%91%E7%AB%99%E4%B8%AD%E7%9A%84blobhttps-%E8%A7%86%E9%A2%91/</span></a>
 -->

## 2020-07-28

写《设置 Visual Studio Code》，把写代码用的字体又整理了一遍，期间我注意到了一个有意思的字体：Input。

Input 由 [David Jonathan Ross](https://djr.com/) 设计，[设计师制作的展示页面（https://djr.com/input/）](https://djr.com/input/)上有很全的展示，[发行方制作的介绍页面（https://input.fontbureau.com/）](https://input.fontbureau.com/)上有灵活的预览和完整的下载（私人使用是免费的，公众使用要付授权费）。

David Jonathan Ross 提出了

## 2020-07-27

有些图片需要加个标题，为了醒目，我设计给标题配上和图片一样宽的灰色底色，紧贴在图片下方，左边再加个深色的竖线。落实的时候，标题总是和图片有个间距，把图片和标题的 `padding` 和 `margin` 手动设置成 `0` 都不行，查了一阵子资料，忽然想到，还可以设置成负值，将 `margin-top` 设置成了 `-1.65em` 后实现了最初的目的。

从他人处引用的图片还需要标注来源，为了好看，我给来源另外设了个样式，把它放在了标题行的右端。

尺寸不大的图片可能会和下方的标题不太搭，为了协调，可以考虑给这样的图片加个背景，为此单独设置了一个样式。为了使用这个样式，需要搭配 `<p>` 和 `<img>` 标签，不能直接使用 Markdown 的图片相关语法。如：

```html
<p class="figwithback">
  <img src="https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Bad_Code_Font.png" alt="不恰当的代码字体选择" />
</p>
```

添加了背景的图片可能会导致标题被背景遮盖，为标题的样式设置了 `position: relative;` 和 `z-index: 100;`。

与此相关的规则集：

```css
.figtitle {
    position: relative;
    z-index: 100;
    margin-top: -1.65em;
    margin-bottom: 1em;
    padding: 2px 0 2px 10px;
    border-left: 5px solid rgba(0, 0, 0, 0.3);
    background-color: rgba(0, 0, 0, 0.1);
    font-size: 0.9em;
    color: rgba(0, 0, 0, 0.7);
}

.figtitlevia {
    float: right;
    padding-right: 10px;
}

.figwithback {
    background-color: var(--code-theme-background);
}
```

过去放在 GitBook 上的笔记的库虽然已经删了，但本地文件的 Git 远程关联还在，这导致了一点混淆。在 Windows Terminal 里使用

```shell
git remote remove origin
```

移除了远程关联。

如果需要添加远程关联，可以使用

```shell
git remote add origin git@github.com:git_username/repository_name.git
```

明确了“不忍卒读”和“难以卒读”的分别（前者褒义后者贬义）。

**参考资料：**

- [《CSS 世界》，张鑫旭，北京：人民邮电出版社，2017-12-01。](https://www.epubit.com/bookDetails?id=N2983)  
  <a href="https://www.epubit.com/bookDetails?id=N2983"><span class="paths">https://www.epubit.com/bookDetails?id=N2983</span></a>
- [《iCSS・谈谈一些有趣的CSS题目（1）——左边框的多种实现方式》，ChokCoco，2019-03-18。](https://github.com/chokcoco/iCSS/issues/51)  
  <a href="https://github.com/chokcoco/iCSS/issues/51"><span class="paths">https://github.com/chokcoco/iCSS/issues/51</span></a>
- [《Web 开发技术・CSS（层叠样式表）・z-index》，Mozilla 贡献者，2020-07-02。](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)  
  <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index"><span class="paths">https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index</span></a>
- [《CSS：你真的会用 z-index 吗？》，WebJ2EE，2019-05-30。](https://juejin.im/post/5cee53f9f265da1bbd4b5746)  
  <a href="https://juejin.im/post/5cee53f9f265da1bbd4b5746"><span class="paths">https://juejin.im/post/5cee53f9f265da1bbd4b5746</span></a>
- [《Pro Git (2nd Edition)・2.5 Git 基础 - 远程仓库的使用》，Scott Chacon，Ben Straub，2014。](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)  
  <a href="https://git-scm.com/book/zh/v2/Git-基础-远程仓库的使用"><span class="paths">https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8</span></a>
- [git-remote, In *Reference of Git*. Retrieved 2020-07-28.](https://git-scm.com/docs/git-remote)  
  <a href="https://git-scm.com/docs/git-remote"><span class="paths">https://git-scm.com/docs/git-remote</span></a>
- [《git 中本地与远程库的关联与取消》，WuShiyuan，2016-01-24。](https://blog.csdn.net/wsycsdn19930512/article/details/50574217)  
  <a href="https://blog.csdn.net/wsycsdn19930512/article/details/50574217"><span class="paths">https://blog.csdn.net/wsycsdn19930512/article/details/50574217</span></a>
- [《成语运用二则：“不忍卒读”“不赞一词”》，赵丕杰，语文建设，2011年第1期。](http://www.yuyingchao.com/beike/html_qikan/yuwenjianshe_6/138959.html)  
  <a href="http://www.yuyingchao.com/beike/html_qikan/yuwenjianshe_6/138959.html"><span class="paths">http://www.yuyingchao.com/beike/html_qikan/qikanlunwen_138959.html</span></a>

## 2020-07-26

这个页面越写越长了，我想把它拆分一下，就建立了个文件夹，按天建立了一系列 Markdown 文件，结果导航栏变得相当难看。调试了一会儿没能搞定，只好退回了原有的版本。

考虑到可能只是暂时搁置，我没有删掉新建的文件夹和文件，而是在根目录新建了一个 <span class="paths">.gitignore</span> 文件，把现在不用的文件夹写了进去，避免将其上传到 GitHub。

由于间隔号（<span class="chs">·</span>）在<span class="typo-em">默认状态</span>下会用英文字体呈现，看上去不大美观，特别新增了一个样式 `.chs` 用来强制将某些文字使用中文字体呈现。

在折腾间隔号的时候，看到了“[漢字標準格式](https://hanzi.pro/)”（陳奕鈞 等，2015-10-27）、“[中文网页重设与排版：typo.css](https://typo.sofi.sh/)”（林建锋〔Sofish Lin〕，2019-01-21）等中文样式的优化方案，继而注意到了 [The Type (Type is Beautiful)](https://www.thetype.com/) 网站对超链接的处理——超链接文字颜色与正文基本一致，加灰色下划线进行标注，鼠标悬停时加深文字和下划线的颜色。对比所有超链接都用不同颜色加以修饰的做法，The Type 最后呈现的效果显得干净清晰又不突兀。

为了搞清楚要改什么地方，我做了一系列的样式跟踪，最后调整了主题当中 `--link-border-bottom`、 `--link-border-bottom--hover`、 `--link-color`、 `--link-color--hover` 几项的设置，另外给 `a` 和 `a:hover` 增加了样式，加大了 `padding-bottom`，完成后的观感还算令人满意。

在“[中文网页重设与排版：typo.css](https://typo.sofi.sh/)”处学到了着重号的设置方法，添加了 `.typo-em` 和 `.typo-em:after` 样式，实现了给中文加<span class="typo-em">着重号</span>的效果。过了一阵子我意识到这个着重号使用的点并不是间隔号常用的中间点`·`（<span class="unicode-number">U+00B7</span> <span class="unicode-name">MIDDLE DOT</span>），而是日文里的片假名中间点`・`（<span class="unicode-number">U+30FB</span> <span class="unicode-name">KATAKANA MIDDLE DOT</span>），它是日文里用片假名转写外文人名时用的间隔号，相比`·`（<span class="unicode-number">U+00B7</span> <span class="unicode-name">MIDDLE DOT</span>），`・`（<span class="unicode-number">U+30FB</span> <span class="unicode-name">KATAKANA MIDDLE DOT</span>）通常都会用中文或日文字体呈现，其尺寸是全宽的，拿来当作日常的间隔号使用相对方便，比较合适，同时也不需要另外调用样式了。

在各种场景中可能会混用的中间点（<span class="unicode-number">U+00B7</span> <span class="unicode-symbol">·</span> <span class="unicode-name">MIDDLE DOT</span>）、连字点（<span class="unicode-number">U+2027</span> <span class="unicode-symbol">‧</span> <span class="unicode-name">HYPHENATION POINT</span>）、全宽句号（<span class="unicode-number">U+FF0E</span> <span class="unicode-symbol">．</span> <span class="unicode-name">FULLWIDTH FULL STOP</span>）、片假名中间点（<span class="unicode-number">U+30FB</span> <span class="unicode-symbol">・</span> <span class="unicode-name">KATAKANA MIDDLE DOT</span>）在不同字体下的呈现情况：

[![四种点状符号在不同字体中的对比](https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/4_dots.png)](https://d.pr/i/T3is)

<div class="figtitle">中间点、连字点、全宽句号、片假名中间点在不同字体下的呈现情况<span>&nbsp;</span><span class="figtitlevia">来源：<a href="https://www.zhihu.com/question/20271115/answer/14565424">梁海</a></span></div>

**参考资料：**

- [《Git 教程・自定义 Git・忽略特殊文件》，廖雪峰，\[2020-07-26\]。](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)  
  <a href="https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208"><span class="paths">https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208</span></a>
- [《为什么在有些软件环境下中文里的中圆点（间隔号）是半角的？》，梁海，2014-11-26。](https://www.zhihu.com/question/20271115/answer/14565424)  
  <a href="https://www.zhihu.com/question/20271115/answer/14565424"><span class="paths">https://www.zhihu.com/question/20271115/answer/14565424</span></a>
- [《GB/T 15834—2011 标点符号用法》，中华人民共和国国家质量监督检验检疫总局，2011-12-30。](http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf)  
  <a href="http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf"><span class="paths">http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf</span></a>
- [Interpunct, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-26.](https://en.wikipedia.org/wiki/Interpunct)  
  <a href="https://en.wikipedia.org/wiki/Interpunct"><span class="paths">https://en.wikipedia.org/wiki/Interpunct</span></a>
- [《HTML 下划线》，蓝蓝，2019-12-17。](https://lanlan2017.github.io/blog/9f0a034b/)  
  <a href="https://lanlan2017.github.io/blog/9f0a034b/"><span class="paths">https://lanlan2017.github.io/blog/9f0a034b/</span></a>
- [《零宽度字符：和谐？屏蔽？不存在的》，Yuan Fu，2018-09-03。](https://juejin.im/post/5b87a6e26fb9a019b953ee8b)  
  <a href="https://juejin.im/post/5b87a6e26fb9a019b953ee8b"><span class="paths">https://juejin.im/post/5b87a6e26fb9a019b953ee8b</span></a>
- [《饿了么如何落地和管理「大前端」团队？》，林建锋，2017/3/17。](https://sofi.sh/p/%E9%A5%BF%E4%BA%86%E4%B9%88%E5%A6%82%E4%BD%95%E8%90%BD%E5%9C%B0%E5%92%8C%E7%AE%A1%E7%90%86%E3%80%8C%E5%A4%A7%E5%89%8D%E7%AB%AF%E3%80%8D%E5%9B%A2%E9%98%9F%EF%BC%9F/)  
  <a href="https://sofi.sh/p/饿了么如何落地和管理「大前端」团队？/"><span class="paths">https://sofi.sh/p/%E9%A5%BF%E4%BA%86%E4%B9%88%E5%A6%82%E4%BD%95%E8%90%BD%E5%9C%B0%E5%92%8C%E7%AE%A1%E7%90%86%E3%80%8C%E5%A4%A7%E5%89%8D%E7%AB%AF%E3%80%8D%E5%9B%A2%E9%98%9F%EF%BC%9F/</span></a>
- [g0v 零&#8203;時&#8203;政&#8203;府](https://g0v.tw/zh-TW/)  
  <a href="https://g0v.tw"><span class="paths">https://g0v.tw/zh-TW/</span></a>
- [萌典](https://www.moedict.tw/)  
  <a href="https://www.moedict.tw"><span class="paths">https://www.moedict.tw/</span></a>

## 2020-07-23

把之前所有值得记录一下的内容都补上了。

## 2020-07-22

在搜索资料的时候撞进了 MegaEase 创始人陈皓的个人网站“[酷壳](https://coolshell.cn/)”（[CoolShell.cn](https://coolshell.cn/)），发现这是个颇有能力的人，他 2019 年 12 月 1 日的一篇文章[《别让自己“墙”了自己》](https://coolshell.cn/articles/20276.html)非常值得一读，另一篇写于 2019 年 11 月 3 日的[《UNIX 50 年：KEN THOMPSON 的密码》](https://coolshell.cn/articles/19996.html)也很有意思。

[《如何写出无法维护的代码》（陈皓，2011-06-03）](https://coolshell.cn/articles/4758.html)很契合本次课程的学习，作为一篇“反面教材”，这篇文章里展现的种种行为可谓令人印象深刻。

## 2020-07-20

2020 年 1 月 15 日，微软正式推出了以 Chromium 为内核的新版 Microsoft Edge。我想使用新版的 Edge，又不想就此抛弃 EdgeHTML 内核的旧版 Edge，就没有使用直接升级的办法，而是使用了 [PortableSoft][] 提供的基于启动器的 [Microsoft Edge 绿色版](https://www.portablesoft.org/microsoft-edge-portable/)（此处为最新版，过去的版本可以在“[Microsoft Edge 历史版本/旧版本下载](https://www.portablesoft.org/microsoft-edge-old-version/)”页面下载）。

近几日 Edge 一直提示我要升级，PortableSoft 的这个启动器没有提供自动升级功能，只能下载新版手工处理升级，处理之余，我翻了翻 PortableSoft，发现这个站也把其提供的 [ABBYY FineReader PDF](https://pdf.abbyy.com/) 的链接换成了思杰马克丁的版本，估计可能是因为想避免麻烦。

苏州的思杰马克丁公司，是家很有特色的公司，从知乎的一个问答“[如何评价苏州思杰马克丁软件公司？](https://www.zhihu.com/question/46746200)”中就可见一斑，虽然很多事情我已经有所了解了，但还是忍不住又花了些时间更新了一下相关信息，顺带又浏览了一遍 [FXXKMAKEDING](https://www.fxxkmakeding.xyz/)。

## 2020-07-19

在找 [docsify][] 的相关文档时看到了 koala 在 2020 年 5 月 20 日写的[《使用 VuePress 搭建博客》](http://www.inode.club/webframe/tool/vuepressBlog.html)，这篇文章引用的官方文档[《VuePress 指南（中文版）》](https://v1.vuepress.vuejs.org/zh/guide/)（[真山](https://ulivz.com/)，2019-06-04）提到了这么个问题：

> **为什么不是 Docsify / Docute？**
>
> 这两个项目同样都是基于 Vue，然而它们都是完全的运行时驱动，因此对 SEO 不够友好。如果你并不关注 SEO，同时也不想安装大量依赖，它们仍然是非常好的选择！

对比来说，VuePress 使用的方式是“预先渲染”，这使得 VuePress 有相对更好的性能和更好的 SEO 特性，docsify 的优势则在于配置方便。

我考虑了一下，决定不折腾了，下次要写什么东西的时候再试 VuePress 吧，总会有用到的时候的。

## 2020-07-18

因为觉得 [docsify][] 的 [docsify-themeable 主题][]原始的配色稍微有些不合心意，又因此做了一串功课。

- 尝试找出原始的配色，但是用 `:root` 和 `var()` 写出来的样式表配置不难、阅读不易，前前后后找了好久，还动用了浏览器的“开发人员工具”（快捷键 <kbd>F12</kbd> 或者 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>），对样式做了一系列的跟踪才最终确定。
- 主题使用的颜色方案是 HSL，通过 [W3Schools][] 的 [Colors Tutorial](https://www.w3schools.com/colors/default.asp) 做了一系列的转换（主要是 RGB、HEX、HSL 间的），又通过 [Coolors][] 试了一些搭配。
- 有些临时用一下的颜色标记，我犯懒就没调样式表，直接写进文字里了，为了代码上好看一点，使用了“HTML 颜色名”，参考了 [HTML Color Codes][] 提供的非常好用的 [HTML 颜色名工具](https://htmlcolorcodes.com/color-names/)。

为了读写直观，参考[《创建漂亮的 CSS 按钮的 10 个代码片段》](https://zhuanlan.zhihu.com/p/25597059)（Jake Rocheleau 著，IT程序狮子烨译，2017-03-06）给 [docsify][] 加了按钮样式。

- 有些范例代码的样式和原本的样式冲突了，导致了意外的覆盖
  - 想要调整一下内容区的宽度，按照原始设计，只要修改 `--content-max-width` 的定义就可以了，但怎么改都不生效
  - 跟踪样式表，发现按钮样式里定义了 `.content` 的最大宽度，注释掉后正常了
- 因为现有样式的影响，按钮样式并没有完全按预定效果呈现，不过现有的效果已经足够用了
- 范例是用 `<a>` 来实现按钮的，实际用的时候改成了 `<button>`
- 顺便调整了“键盘按键”（`<kbd>`）的表现，参考了[《Nice effect with the KBD tag》](https://www.rgagnon.com/jsdetails/js-nice-effect-the-KBD-tag.html)（Réal Gagnon, 2012-12-26）、[《CSS for the new \<kbd\> style》](https://meta.superuser.com/questions/4788/css-for-the-new-kbd-style)（Israel Galvez, 2012-05-05）

每次向 GitHub 进行提交的时候，都要连着运行：

```powershell
git status
git add .
git commit -m"说明"
git push origin master
```

做多了多少有点烦，特别是连续更新某个文件的时候，于是了解了一下“[如何在 PowerShell 中连续执行命令](https://segmentfault.com/a/1190000007727032)”，用 `;` 把三条命令合并成了一条：

```powershell
git add . ; git commit -m"说明" ; git push origin master
```

## 2020-07-17

原本是想好好给《进入编程世界》写个笔记，方便自己也方便他人，结果为自己刨了一系列的坑。

最初的想法很简单：找个网络上方便更新、检索的地方，一直写就行了。

然后事情就成了这样——

- 在 GitHub 开个仓库写 <span class="paths">README.md</span> 可能就行了
  - 页面会拉得太长
  - 检索不够方便
  - 写到一半的部分放在那里不好看
- 找个和 GitHub 联动的发布工具，[GitBook](https://www.gitbook.com/) 可能就行了
  - GitBook 在 2018 年改了版，新版没有了引入自有样式的功能
  - GitBook 现在免费的“空间”数量非常有限，这显然是受到了 GitBook 商业化运营的影响
  - 网上大量 GitBook 的资讯现在都已经严重过时，新版的帮助文档也不够完整好用  
    <span class="commentary">意味着我读相关资料的时间都失去价值了，其实我先看英文资料就会发现这些情况的，可惜……</span>
  - GitBook 对样式的过滤和 GitHub 一样严格，连给文字加个颜色都没办法
- 放弃 GitBook，备份、删库，做了些功课后决定改用 [docsify][]  
  <span class="commentary">一个原因是李笑来老师现在在用 docsify 发布文章和书籍</span>
  - 安装
    - Node.js  

      ```powershell
      scoop install nodejs
      ```

    - npm
      - `npm` 命令跑不起来，连 `node` 命令都跑不起来
      - 检查了一下环境变量，看上去是好的
      - 前几天 `npm` 还是正常的，不知道是不是 Scoop 更新的时候哪里出了意外
      - Scoop 进行了一下更新，问题没有解决
      - 做了做功课，决定先用 [Yarn](https://yarnpkg.com/) 完成工作
    - Yarn  

      ```powershell
      scoop install yarn
      ```

      - 安装完后需要重启或另开 Windows Terminal 才能使用
    - docsify  

      ```powershell
      yarn global add docsify-cli
      ```

      - 用 Yarn 安装 docsify 还是要用 `node` 命令，还是要解决 npm 那里的问题
      - Scoop 做了一下自检  

        ```powershell
        scoop checkup
        ```

        - 3 个<span style="color: CORAL">警告</span> 1 个<span style="color: CRIMSON">错误</span>
          - 警告：Defender 可能会拖慢会中断安装进程，建议运行  

            ```powershell
            sudo Add-MpPreference -ExclusionPath 'C:\Users\[用户名]\scoop'
            ```

          - 警告：Defender 可能会拖慢会中断安装进程，建议运行  

            ```powershell
            sudo Add-MpPreference -ExclusionPath 'C:\ProgramData\scoop'
            ```

          - 警告：长路径支持未启用，建议运行  

            ```powershell
            Set-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem' -Name 'LongPathsEnabled' -Value 1
            ```

            - 因为这个命令要动注册表，所以直接运行可能会报“权限不足”的错误
            - 可以考虑用管理员身份运行一个 Windows Terminal 来执行命令
            - 也可以在指令前添加 <code>sudo </code> 来一次性地调用管理员权限执行命令
          - 错误：Inno Setup Unpacker 未安装，其用来解包 InnoSetup 文件，请运行  

            ```powershell
            scoop install innounp
            ```

      - 根据 Scoop 自检的建议，启用了长路径支持后，`node` 可以使用了
  - 设置
    - 在 GitHub 建立新库，克隆到本地
    - 在本地使用  

      ```powershell
      docsify init [文件夹]
      ```

      初始化项目
    - 运行  

      ```powershell
      docsify serve [文件夹]
      ```

      可启动一个本地服务器，实时预览效果，默认访问地址为 <a href="http://localhost:3000"><span class="paths">http://localhost:3000</span></a>
    - 参考[docsify 官方文档][]（<a href="https://docsify.js.org/#/zh-cn/"><span class="paths">https://docsify.js.org/#/zh-cn/</span></a>）完成基础设置
      - 添加侧边栏
      - 添加插件
        - 全文搜索
        - emoji
        - 外链脚本
        - 图片缩放
        - 复制到剪贴板
        - 分页导航
        - 代码高亮
          - 添加了 `bash`、`powershell`、`ini`、`python` 的语法支持
          - 顺带了解了一下 <span class="paths">.js</span> 和 <span class="paths">.min.js</span> 的分别：带“min”的是压缩过的 JavaScript 文件，体积更小，但不易读
      - 使用 [docsify-themeable 主题][]
        - 了解了一下 CSS 中 `:root` 和 `var()` 的用法
        - 添加自定义的样式表
          - 重新定义了字体
          - 重新定义了颜色
          - 重新定义了页面宽度
          - 重新定义了“键盘按键”的表现
          - 新增了“路径”、“菜单”、“按钮”的表现
  - 部署到 GitHub Pages
    - 在仓库的 <span class="menutext">Settings</span> 页面的 <span class="menutext">GitHub Pages</span> 区域，把 <span class="menutext">Source</span> 改为了 <span class="menutext">master branch</span>
    - 图片单独传到了 <span class="paths">img</span> 库里，方便管理和调用

可以暂时踏实写笔记了，不过现在很多样式是用 `<span>` 硬写进去的，这些内容在 Markdown 文档里有点“扎眼”，这个其实可以通过给 docsify 内置的 Markdown 解析器 [marked](https://github.com/markedjs/marked) 添加自定义规则进行改善，但这又是另外一大套功课，今天就先算了。

**参考资料：**

- [《基于Github Pages + docsify，我花了半天就搭建好了个人博客》，二营长，2020-01-05。](https://blog.csdn.net/m0_37965018/article/details/103841362)  
  <a href="https://blog.csdn.net/m0_37965018/article/details/103841362"><span class="paths">https://blog.csdn.net/m0_37965018/article/details/103841362</span></a>
- [《淺談新版 GitBook（GitBook V2）——失去交流開放精神的企業導向產品》，Yuni，2019-08-28。](https://www.onejar99.com/gitbook-v2-comment/)  
  <a href="https://www.onejar99.com/gitbook-v2-comment/"><span class="paths">https://www.onejar99.com/gitbook-v2-comment/</span></a>
- [《如何看待 GitBook 的改版？》，Lellansin Huang，2018-04-11。](https://www.zhihu.com/question/271881476)  
  <a href="https://www.zhihu.com/question/271881476"><span class="paths">https://www.zhihu.com/question/271881476</span></a>
- [《關於 GitBook 平台的改版與 GitLab 替代的考量》，王克明，2018-09-27。](https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/)  
  <a href="https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/"><span class="paths">https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/</span></a>
- [《CSS中的 “var()” 和 “:root”》，ArvinWoo，2018-11-26。](https://blog.csdn.net/qq_37595946/article/details/84531311)  
  <a href="https://blog.csdn.net/qq_37595946/article/details/84531311"><span class="paths">https://blog.csdn.net/qq_37595946/article/details/84531311</span></a>
- [《Web 开发技术・CSS（层叠样式表）・var()》，Mozilla 贡献者，2019-11-13。](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)  
  <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/var"><span class="paths">https://developer.mozilla.org/zh-CN/docs/Web/CSS/var</span></a>

## 2020-07-16

为了方便使用，把课程和笔记相关的文件夹固定到了资源管理器的快速访问区，然后就觉得那两个默认图标不大协调，就转去研究自定义文件夹图标了，搞清楚设置过程没花太多时间，但搞好要用的图标费了不少劲。

最后自制了四个图标，基本上够用了，还有一点没什么影响的瑕疵，暂时我也不想再折腾了。

具体过程整理成了[《设置文件夹》](/a-appendix/setting-folders.md)一文，可供参考。

## 2020-07-14

用了两天多的时间做功课，参考[《GitBook 教程（小白入坑 GitBook 全过程）》](https://www.jianshu.com/p/0388d8bb49a7)（Broken故城，2020-02-20）、[《GitBook 使用教程》](https://segmentfault.com/a/1190000017960359)（yulilong，2019-01-21），在 GitBook 新建了一个“Space”（<a href="https://shen-huang.gitbook.io/wop-notes-win/"><span class="paths">https://shen-huang.gitbook.io/wop-notes-win/</span></a>），关联到了 GitHub 仓库。

## 2020-07-13

为了在苹果 App Store 美国区买应用，完整地跑了一遍用信用卡在[苹果官网买电子版礼品卡](https://www.apple.com/shop/gift-cards)的流程，不必登录账号，直接用访客身份购买即可，地址要写美国免税州里的（只有 5 个：Alaska、Delaware、Montana、New Hampshire、Oregon，Alaska 和 Montana 可能还有潜在税收，尽量不要写这两个），用 [Fake Address Generator](https://www.fakeaddressgenerator.com/) 生成即可。

**参考资料：**

- [《通过购买礼品卡（Gift Cards）给美国 Apple ID 充值方法》，陈浩，2019-08-09](https://www.hurbai.com/iOS/182)  
  <a href="https://www.hurbai.com/iOS/182"><span class="paths">https://www.hurbai.com/iOS/182</span></a>
- [The 5 U.S. States Without a Statewide Sales Tax: Where to Do Your Purchasing in the U.S., In *The Balance*. Retrieved 2020-07-14.](https://www.thebalance.com/states-without-a-sales-tax-3193305)  
  <a href="https://www.thebalance.com/states-without-a-sales-tax-3193305"><span class="paths">https://www.thebalance.com/states-without-a-sales-tax-3193305</span></a>
- [《苹果突然封号，iPhone 这个漏洞，千万别碰》，雷科技，2020-01-22。](https://36kr.com/p/1725033807873)  
  <a href="https://mp.weixin.qq.com/s/gBVQcv7cIYLalqbhV8pvOw"><span class="paths">https://mp.weixin.qq.com/s/gBVQcv7cIYLalqbhV8pvOw</span></a>

## 2020-07-12

想好好给李骏老师的课程《进入编程世界》写个笔记，2019 年做类似事情的时候，我就在 GitHub 仓库的 <span class="paths">README.md</span> 里写了，写了一阵子发现多少有点不方便：单页难以检索，分页跳转麻烦，样式限制很多，扩展能力孱弱。毕竟，<span class="paths">README.md</span> 不是用来写复杂文档的。

我首先想到的替代方案，是 GitBook。2015 年的时候李笑来老师用 GitBook 做了在线版本的[《把时间当作朋友（第 3 版）》](https://legacy.gitbook.com/book/xiaolai/ba-shi-jian-dang-zuo-peng-you/details)，当时还基于它搞了“知笔墨”（已停止运维，旧页面可以从互联网档案馆的[网站时光机相关快照](https://web.archive.org/web/20180806235112/http://www.zhibimo.com/explore/books)里查看），我也因此对 GitBook 有了些感性认识。

完整地看了几遍[《GitBook 文档（中文版）》](https://chrisniael.gitbooks.io/gitbook-documentation/content/)（Samy Pessé 等著，沈煜 译，2016-12-12），打算明后天着手正式搭建。

## 2020-07-11

为了醒目、好看，我以往记录快捷键的时候如果遇到“Windows 键”，可能会额外多贴一个小图来表示：<kbd>![Win][Windows_Logo_12px] Win</kbd>，今天发现维基百科的处理方式是借用字符“⊞”，写成 <kbd>⊞ Win</kbd>，看上去也能接受，不失为一种处理方法。

**参考资料：**

- [Windows key, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Windows_key)  
  <a href="https://en.wikipedia.org/wiki/Windows_key"><span class="paths">https://en.wikipedia.org/wiki/Windows_key</span></a>
- [Is there a unicode character for the Windows key? Gabriel Fair, 2017-04-09.](https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key)  
  <a href="https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key"><span class="paths">https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key</span></a>
- [The Ultimate Guide to Windows Keyboard Shortcuts. HelloTech, 2017-01-16.](https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts)  
  <a href="https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts"><span class="paths">https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts</span></a>

## 2020-07-10

Windows Terminal 对操作系统版本有要求（至少 18362.0，也就是 1903），这引发了一系列问题。

为了用起来稳定、方便维护，我的台式机使用了从 VHDX 启动的 Windows 10 Enterprise 2019 LTSC，这个 Windows 10 分支的主版本是 1809，就算另外加装了 Microsoft Store 也装不了 Windows Terminal，LTSC 版和 VHDX 又都会导致无法进行大版本升级。

我把系统转换成了 Windows 10 Pro，避开了 LTSC 的限制，但 VHDX 升级的限制没法绕过去。我只好在硬盘另外划分出来了一个分区，把 VHDX 的内容用分区复制的方式倒了进去，然后用这个新分区启动。启动、升级完成后，我想把这个系统再倒回 VHDX 里，用不同的分区复制的方式试验了数次，都无法启动，最终放弃了，决定就在这个用实体分区启动的 Windows 10 Pro 上完成课程的学习。

**参考资料：**

- [《将 Windows 10 LTSC 版转换为专业版激活，使用纯净无预装的 Windows 10》，王洪峰，2019-04-12。](https://wanghongfeng.cn/LTSC2019.html)  
  <a href="https://wanghongfeng.cn/LTSC2019.html"><span class="paths">https://wanghongfeng.cn/LTSC2019.html</span></a>

## 2020-07-09

怎么都搞不定 macOS 上 Python 3.x 软链接的建立，按照说明折腾了一阵子，`python` 命令调用的一直是系统自带的 Python 2.7.3，虽然用 `python3` 也能解决问题，但我就是不服气，于是就干了“撞破南墙”的事情。

我找到了系统自带的 Python 2.7.3 的位置：<span class="paths">/usr/bin/python</span>，但这个位置是系统管理的，用户不能直接操作，为了动它，我重开机，用 <kbd>⌘ Command</kbd> + <kbd>R</kbd> 进了 macOS 实用工具，然后运行 `csrutil disable` 关闭了 SIP（System Integrity Protection），然后获取了 <span class="paths">/usr/bin/ 的最高权限（777），把 <span class="paths">/usr/bin/python</span> 这个软链接删了，在原位置建立了到 <span class="paths">/usr/local/bin/python3</span> 的软链接。

这么弄完，`python` 命令调用的确实是 Python 3.x 了，可是李骏老师告知我这个方法大错特错——macOS 不让用户动某些东西是有道理的，而且确实不应该动。我在老师的帮助下，明确了原本系统的软链接的路径，但由于我动了底层的设置，Terminal 无法正常工作了，在 macOS 实用工具里也处理不了……

为了能正常用 Terminal，我手动建立了 root 账号，在其中还原了最初的软链接，又重新打开了 SIP，删掉了 root 账号，这才回到了起点。

我无奈之下提了个 Issue：“[无法在 macOS 的 Terminal 使用 `python` 指令调用 Python 3.7.x](https://github.com/neolee/wop-community/issues/88)”，经过一系列排查和尝试，最后靠强制建立软链接搞好了，但这应该也不是问题的根源，李骏老师最后说：因为现场很难还原，当时到底发生了什么已不可考，施主请放下吧……

**参考资料：**

- [《5 分钟让你明白“软链接”和“硬链接”的区别》，Cyandev，2016-07-08。](https://www.jianshu.com/p/dde6a01c4094)  
  <a href="https://www.jianshu.com/p/dde6a01c4094"><span class="paths">https://www.jianshu.com/p/dde6a01c4094</span></a>
- [Fix Terminal “Operation not permitted” Error in MacOS Mojave. Paul Horowitz, 2018-10-09.](https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/)  
  <a href="https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/"><span class="paths">https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/</span></a>
- [How to Disable System Integrity Protection (rootless) in Mac OS X. Paul Horowitz, 2015-10-05.](https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/)  
  <a href="https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/"><span class="paths">https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/</span></a>
- [《macOS 开启或关闭 SIP》，雪谋，2019-06-07。](https://sspai.com/post/55066)  
  <a href="https://sspai.com/post/55066"><span class="paths">https://sspai.com/post/55066</span></a>
- [《MacOS (Catalina)：显示 Read-only file system 的对应方法》，liumiaocn，2020-02-15。](https://blog.csdn.net/liumiaocn/article/details/104324664)  
  <a href="https://blog.csdn.net/liumiaocn/article/details/104324664"><span class="paths">https://blog.csdn.net/liumiaocn/article/details/104324664</span></a>
- [《macOS Catalina 无法删除 /usr/bin/ 下面的文件》，高金，2019-10-10。](https://igaojin.me/2019/10/10/Mac-catalina-%E6%97%A0%E6%B3%95%E5%88%A0%E9%99%A4-usr-bin-%E4%B8%8B%E9%9D%A2%E7%9A%84%E6%96%87%E4%BB%B6/)  
  <a href="https://igaojin.me/2019/10/10/Mac-catalina-无法删除-usr-bin-下面的文件/"><span class="paths">https://igaojin.me/2019/10/10/Mac-catalina-%E6%97%A0%E6%B3%95%E5%88%A0%E9%99%A4-usr-bin-%E4%B8%8B%E9%9D%A2%E7%9A%84%E6%96%87%E4%BB%B6/</span></a>
- [《macOS 修改 /usr/bin/ 权限后导致控制台无法使用》，迷途中的小码农，2019-04-18。](https://blog.csdn.net/ethan__xu/article/details/89390220)  
  <a href="https://blog.csdn.net/ethan__xu/article/details/89390220"><span class="paths">https://blog.csdn.net/ethan__xu/article/details/89390220</span></a>

## 2020-07-08

了解了一下 Shell、Bash、Zsh 等概念，顺带明确了 <span class="paths">.bash_profile</span>、<span class="paths">.bashrc</span>、<span class="paths">.zshrc</span> 这几个文件的关系。考虑到很多同学可能并没有从 Bash 切换到 Zsh，我就暂时停在了 Bash，主要调整了 <span class="paths">.bash_profile</span> 文件，加入了代理和关闭 Zsh 升级提示的设置，打算明天再分享一次，附带说明一下怎么可以“一劳永逸”地解决 macOS 的 Terminal 的网络代理设置问题。

编辑 <span class="paths">.bash_profile</span> 文件可能会遇到麻烦（很多文档都教读者用 VIM 来做这事，对初学者真的……不够友好），这事可以用 Visual Studio Code（下简称 VS Code）来做，在 Terminal 里输入并运行 `code ~/.bash_profile` 就能用 VS Code 打开这个文件了。如果因为种种原因，还没装 VS Code，则可以在 Terminal 里输入并运行 `open ~/.bash_profile`，这样会使用 macOS 自带的“文本编辑”打开这个文件，编辑起来会比 VIM 容易上手一些。

**参考资料：**

- [《你明白 Shell、Bash 和 Zsh 等词的真正含义吗？》，阿德，2018-03-03。](https://zhuanlan.zhihu.com/p/34197680)  
  <a href="https://zhuanlan.zhihu.com/p/34197680"><span class="paths">https://zhuanlan.zhihu.com/p/34197680</span></a>
- [《终极 Shell》，池建强，2013-07-23。](http://macshuo.com/?p=676)  
  <a href="http://macshuo.com/?p=676"><span class="paths">http://macshuo.com/?p=676</span></a>
- [《让你的 Mac 提前用上 macOS Catalina 的 Shell —— Oh My Zsh 配置指南》，Steven，2019-06-12。](https://sspai.com/post/55176)  
  <a href="https://sspai.com/post/55176"><span class="paths">https://sspai.com/post/55176</span></a>
- [《关于“.bash_profile”和“.bashrc”区别的总结》，史晨，2017-04-20。](https://blog.csdn.net/sch0120/article/details/70256318)  
  <a href="https://blog.csdn.net/sch0120/article/details/70256318"><span class="paths">https://blog.csdn.net/sch0120/article/details/70256318</span></a>
- [《Mac 更新之后使用终端提示：The default interactive shell is now zsh.》，深碍，2019-12-26。](https://www.jianshu.com/p/26d365078081)  
  <a href="https://www.jianshu.com/p/26d365078081"><span class="paths">https://www.jianshu.com/p/26d365078081</span></a>
- [Bash, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Bash_(Unix_shell))  
  <a href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)"><span class="paths">https://en.wikipedia.org/wiki/Bash_(Unix_shell)</span></a>
- [Z shell, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Z_shell)  
  <a href="https://en.wikipedia.org/wiki/Z_shell"><span class="paths">https://en.wikipedia.org/wiki/Z_shell</span></a>

## 2020-07-07

计划在 Mixin Messenger 群里开个分享，讲讲如何解决编程课遭遇的各种网络问题，为了应对更多的需求，专门把 macOS 上的情况也测试了一遍，然后发现 macOS Catalina (10.15) 有个“无法验证开发者就阻止程序运行”的坑。

“无法验证开发者”的问题，可以在访达的“应用程序”里，按住 <kbd>Control</kbd> 的同时，用鼠标左键单击需要打开的应用的图标，再单击 <span class="menutext">打开</span>，就会弹出可供跳过验证、打开应用的对话框了。

## 2020-07-06

想要搞一下 Windows Terminal 的美化，然后就陷入了巨量的选项之中。

首先看到了[李欢](https://www.zhihu.com/people/lihuan123) 2020 年 4 月 27 日写的[《简单配置与美化 PowerShell 和 Terminal》](https://zhuanlan.zhihu.com/p/104720872)，和 [Clint Richardson](https://twitter.com/clinterich) 2019 年 8 月 2 日写的[《The New Windows Terminal – Install, Interact, and Customize》](https://www.appliedis.com/the-new-windows-terminal-install-interact-and-customize/)。

跟着研究了一下 [posh-git](https://github.com/dahlbyk/posh-git)，以及 [Windows Terminal Themes](https://atomcorp.github.io/themes/) 里让人眼花缭乱的主题配色，还参考了 [Thomas Maurer](https://www.thomasmaurer.ch/) 2020 年 6 月 14 日的相关推荐文章[《My Windows Terminal Color Schemes》](https://www.thomasmaurer.ch/2020/06/my-windows-terminal-color-schemes/)。

这些折腾完，就轮到了字体，用于代码的等宽字体其实有不少可选项，但一混上中文情况就不妙了，理想的情况是 1 个中文字宽等于 2 个英文字宽，中英文混杂的行也能够纵向对齐，实际上这很难准确实现。我试了民间自制的 YaHei Consolas Hybrid（微软雅黑和 Consolas 的混合字体）、Microsoft Yahei Mono（也是微软雅黑和 Consolas 的混合字体）、Yahei Source Code Pro（微软雅黑和 Source Code Pro 的混合字体），都对不齐。专门用于这一目的制作的“等距更纱黑体”，对齐倒是很完美，但英文部分实在是显得太窄了，看着累人，最后我选择了保持原状，将来再折腾吧……

**参考资料：**

- [《美化 Windows Terminal（iTerm2-Color-Schemes)》，Jioho_chen，2019-09-08。](https://blog.csdn.net/Jioho_chen/article/details/100624029)  
  <a href="https://blog.csdn.net/Jioho_chen/article/details/100624029"><span class="paths">https://blog.csdn.net/Jioho_chen/article/details/100624029</span></a>
- [《Retina 屏幕上的最佳编程字体》，Lenciel，2014-07-13。](https://lenciel.com/2014/07/font-for-programming/)  
  <a href="https://lenciel.com/2014/07/font-for-programming/"><span class="paths">https://lenciel.com/2014/07/font-for-programming/</span></a>
- [《推荐的编程字体》，余淦成，2015-08-08。](https://www.ifeegoo.com/recommended-programming-fonts.html)  
  <a href="https://www.ifeegoo.com/recommended-programming-fonts.html"><span class="paths">https://www.ifeegoo.com/recommended-programming-fonts.html</span></a>
- [What are the best programming fonts? *Slant*, Retrieved 2020-07-06.](https://www.slant.co/topics/67/~best-programming-fonts)  
  <a href="https://www.slant.co/topics/67/~best-programming-fonts"><span class="paths">https://www.slant.co/topics/67/~best-programming-fonts</span></a>
- [《编程字体》，bayhiker，2019-09-25。](https://blog.rule55.com/coding-fonts/)  
  <a href="https://blog.rule55.com/coding-fonts/"><span class="paths">https://blog.rule55.com/coding-fonts/</span></a>
- [《推荐几款连字字体，在代码编辑器中启用连字字体（Visual Studio Code）》，吕毅，2019-09-27。](https://blog.csdn.net/WPwalter/article/details/101512456)  
  <a href="https://blog.csdn.net/WPwalter/article/details/101512456"><span class="paths">https://blog.csdn.net/WPwalter/article/details/101512456</span></a>
- [《CSS font-family 常见中文字体对应的英文名称》，张鑫旭，2017-03-25。](https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/)  
  <a href="https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/"><span class="paths">https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/</span></a>
- [《Fira Code | 为写程序而生的字体》，Mogeko，2017-09-16。](https://www.jianshu.com/p/266b4fa2c446)  
  <a href="https://mogeko.me/2017/006/"><span class="paths">https://mogeko.me/2017/006/</span></a>
- [《Fira Code: 一个有趣而实用的编程字体》，Luo Jia，2018-06-20。](https://luojia.cc/2018/06/20/font-fira-code/)  
  <a href="https://luojia.cc/2018/06/20/font-fira-code/"><span class="paths">https://luojia.cc/2018/06/20/font-fira-code/</span></a>
- [《分享一下自己修改的字体~ Yahei Source Code Pro v1.23》，DeepKolos，2017-07-15。](https://www.jianshu.com/p/28acf9226ddb)  
  <a href="https://www.jianshu.com/p/28acf9226ddb"><span class="paths">https://www.jianshu.com/p/28acf9226ddb</span></a>
- [YaHei Consolas Hybrid 和 Yahei Source Code Pro 的下载页面](https://github.com/yyxyz/OSOperateSkills/find/master)  
  <a href="https://github.com/yyxyz/OSOperateSkills/find/master"><span class="paths">https://github.com/yyxyz/OSOperateSkills/find/master</span></a>
- [更纱黑体主仓库](https://github.com/be5invis/Sarasa-Gothic)  
  <a href="https://github.com/be5invis/Sarasa-Gothic"><span class="paths">https://github.com/be5invis/Sarasa-Gothic</span></a>
- [Iosevka 字体主页](https://typeof.net/Iosevka/)  
  <a href="https://typeof.net/Iosevka/"><span class="paths">https://typeof.net/Iosevka/</span></a>

## 2020-07-05

有同学称自己安装 Scoop 的时候被杀毒软件挡住了，查了一下，发现是“联想杀毒 Plus”和“联想电脑管家”，进一步挖掘得知，联想杀毒 Plus 是基于 McAfee 的，联想电脑管家是基于火绒的，类似于加壳改名。据说这两个软件都不算好用，甚至有联想客服建议卸载随机自带的联想杀毒 Plus。

将这两个软件卸载并启用 Windows 10 自带的 Defender 后，问题解决。

**参考资料：**

- [《联想杀毒 PLUS》，wildtree23，2020-06-05。](https://bbs.kafan.cn/thread-2183667-1-1.html)  
  <a href="https://bbs.kafan.cn/thread-2183667-1-1.html"><span class="paths">https://bbs.kafan.cn/thread-2183667-1-1.html</span></a>
- [《【联想客服内部超级爆料】你的联想杀毒 Plus 安全软件卸载了没有？》，1T科技，2020-06-14。](https://www.bilibili.com/video/BV1Bk4y1z7d5)  
  <a href="https://www.bilibili.com/video/BV1Bk4y1z7d5"><span class="paths">https://www.bilibili.com/video/BV1Bk4y1z7d5</span></a>

## 2020-07-04

在交流群里有人问命令开头那个 `$` 是什么意思，被告知是“提示符”，也就是系统告诉你可以输入命令了。很多人搞不清楚这件事，照着说明把 `$` 一起敲进命令里运行，跟着就出错。

不过我因此生出了另一个问题：为什么是 `$`？

在网上做了一阵子功课后发现，`$` 的使用可以追溯到 1979 年发布的 Version 7 Unix 系统，这个选择可能来自于早在 1963 年就面世的电传打字机 Teletype Model 33 ASR (**A**utomatic **S**end and **R**eceive)——由于其键盘上可用的符号很少，提示符又需要“尽量简短”且“不易混淆”，最终，工程师挑选了 `$`。另一个可能来源，是 1962 年 IBM 推出的 FORTRAN IV，那个时期的计算机还没有键盘和显示器，所有的程序输入都靠打孔卡片实现，程序输出则靠打印机实现，在输出的时候，FORTRAN IV 使用了 `$` 来标记那些输入的命令。

在 1979 年之前，Unix 系统使用的 Shell 是“C Shell”，其默认的提示符是“`%`”，Version 7 Unix 系统使用了 Stephen Bourne 开发的“Bourne Shell”，其默认提示符选择了“`$`”，在随后的时光中，Version 7 Unix 系统产生了巨大的影响，`$` 也成为了 Unix 系统和类 Unix 系统惯用的提示符。macOS 的内核是从 Unix 的分支开发而来的，也就继承了使用 `$` 的传统。

Version 7 Unix 系统还给出了“次要提示符”“`>`”，我们可以进行一点合理推测——这就是 DOS（1981 年推出）和之后的 Windows（1985 年推出）默认的提示符的起源。

除了 `$`、`%`、`>` 之外，`#` 也在某些情况下被用作提示符，可以想见，其实任何“尽量简短”且“不易混淆”的符号在这个上下文中都是合理的，我们现在看到的境况，与其说是有意的设计，不如说是历史的选择，而这种选择，有着各种各样的机缘和巧合。

**参考资料：**

- [What is the origin of the UNIX $ (dollar) prompt? Max Howell, 2009-10-19.](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)  
  <a href="https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt"><span class="paths">https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt</span></a>
- [Why was the dollar sign chosen as the Unix shell prompt? Eduardo Sangiorgio Dobay, 2015-07-21.](https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt)  
  <a href="https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt"><span class="paths">https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt</span></a>
- [Teletype Model 33, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Teletype_Model_33)  
  <a href="https://en.wikipedia.org/wiki/Teletype_Model_33"><span class="paths">https://en.wikipedia.org/wiki/Teletype_Model_33</span></a>
- [What does the $ mean when running commands? Joshua Paul A. Chan, 2013-11-14.](https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands)  
  <a href="https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands"><span class="paths">https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands</span></a>
- [SH(1), In *UNIX Programmer’s Manual, Seventh Edition, Volume 1*. Bell Telephone Laboratories, Incorporated. 1979-01.](https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf)  
  <a href="https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf"><span class="paths">https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf</span></a>
- [Digital computing, FORTRAN IV, WATFIV, and MTS (with \*FTN and \*WATFIV). Brice Carnahan, James O. Wilkes. Ann Arbor: Chemical Engineering Dept., University of Michigan. 1976. p. 2-76.](https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false)  
  <a href="https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false"><span class="paths">https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false</span></a>
- [Command-line interface, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Command-line_interface#Command_prompt)  
  <a href="https://en.wikipedia.org/wiki/Command-line_interface"><span class="paths">https://en.wikipedia.org/wiki/Command-line_interface</span></a>
- [Unix, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Unix)  
  <a href="https://en.wikipedia.org/wiki/Unix"><span class="paths">https://en.wikipedia.org/wiki/Unix</span></a>
- [DOS 1.0 booted. Michal Necasek, 2011-08-03.](http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/)  
  <a href="http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/"><span class="paths">http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/</span></a>
- [ALL VERSIONS OF MS-DOS (1.0-8.0). Windows Expert, 2019-08-02.](https://www.youtube.com/watch?v=5cS-PIuyEhU)  
  <a href="https://www.youtube.com/watch?v=5cS-PIuyEhU"><span class="paths">https://www.youtube.com/watch?v=5cS-PIuyEhU</span></a>
- [《Unix, Linux 和 macOS》，keith，2019-05-11。](https://juejin.im/post/5cd5d1b4518825686761cc1f)  
  <a href="https://juejin.im/post/5cd5d1b4518825686761cc1f"><span class="paths">https://juejin.im/post/5cd5d1b4518825686761cc1f</span></a>

## 2020-07-03

在开课之前打算先把环境搞好，本来不算麻烦的事，真正弄起来就遇到了各种意外。

<!-- - Windows Terminal 对操作系统版本有要求（至少 18362.0，也就是 1903），这引发了一系列问题
    - 为了用起来稳定一些，我使用了 Windows 10 Enterprise 2019 LTSC，它的主版本是 1809，就算另外加装了 Microsoft Store 也装不了 Windows Terminal
    - 为了升级，我把系统转换成了 Windows 10 Pro，但因为之前为了方便维护，我是从 VHDX 启动的系统，这样的系统没法进行大版本升级
    - 在硬盘另外划分出来了一个分区，把 VHDX 的内容用分区复制的方式倒了进去，然后用这个新分区启动
    - 启动、升级完成后，我想把这个系统再倒回 VHDX 里，用不同的分区复制的方式试验了数次，都无法启动，最终放弃了 -->

- Scoop 安装的时候要访问 [raw.githubusercontent.com](raw.githubusercontent.com)，这可能遭遇各种网络问题
  - 改本地 hosts 无效
  - 修改 DNS 服务器设置无效
  - Windows Terminal 是个 UWP 应用，默认没法加本地代理，最后用 Clash for Windows 带的 AppContainer Loopback Exemption Utility（又称 UWP Loopback Helper）给它加上了代理
- Homebrew 的安装遇到了和 Scoop 一样的网络问题
  - 可以用 `export` 命令给 Terminal 设置代理
  - 为了将来方便，把代理设置写入了 <span class="paths">~/.bash_profile</span>

<!-- 
- 在 macOS 上为 `python` 建立软链接的时候怎么都无法生效
    - 打破了 macOS Catalina 设置的各种权限，最终替掉了系统自带的 Python 2.7 的软链接
    - 由于对系统核心的设置进行了修改，Terminal 无法正常工作了
    - 单独建立了 root 账户，把系统还原
    - 使用强制建立软链接的方式实现了最初的目的
    - 删除软链接、再使用原本的方式建立软链接，也没问题了
    - 故障原因最终未查明
 -->

<!-- 
链接
 -->

[docsify]: https://docsify.js.org/
[docsify-themeable 主题]: https://jhildenbiddle.github.io/docsify-themeable/
[docsify 官方文档]: https://docsify.js.org/#/zh-cn/
[W3Schools]: https://www.w3schools.com/
[Coolors]: https://coolors.co/
[HTML Color Codes]: https://htmlcolorcodes.com/
[PortableSoft]: https://www.portablesoft.org/
[Stack Overflow]: https://stackoverflow.com/

<!-- 
图片
 -->

[Windows_Logo_20px]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/20px-Windows_logo_2012-Black.svg.png
[Windows_Logo_16px]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/16px-Windows_logo_2012-Black.svg.png
[Windows_Logo_12px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_12px.svg?sanitize=true
[Windows_Logo_8px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_8px.svg?sanitize=true
[Windows_Logo_6px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_6px.svg?sanitize=true
