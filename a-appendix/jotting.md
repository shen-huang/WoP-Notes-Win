# 随记

这里是一些我在学习过程中“注意力漂移”的记录。

## 2020-08-01

发现了一个使用零宽字符（零宽空格、零宽连字、零宽不连字）在文章中藏匿信息的方法，具体操作可见 Jad 在 2018 年 4 月 13 日发布的[《我仔细看了半天，才从字缝里看出字来……》](https://imjad.cn/archives/code/hide-text-typecho-plugin/)一文。

另外明确了一下，不要使用“H5”来简称“HTML5”，细节可见 [JS小组](https://weibo.com/baidujs) 在 2015 年 7 月 5 日发布的[《为何不要用「h5」这个简称？》](https://mp.weixin.qq.com/s/AZ4gKhPRmIV2poHgURbVYA)一文。

**参考资料**

- [Be careful what you copy: Invisibly inserting usernames into text with Zero-Width Characters. Tom Ross, 2018-04-03.](https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66)  
  [https://link.medium.com/zKcoNeBPy8](https://medium.com/@umpox/be-careful-what-you-copy-invisibly-inserting-usernames-into-text-with-zero-width-characters-18b4e6f17b66)

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

我另外阅读了 Harry Roberts 在 2020 年 5 月 19 日撰写的《[最快的 Google Fonts](cloud.tencent.com/developer/news/643958)》（[*The Fastest Google Fonts*](https://csswizardry.com/2020/05/the-fastest-google-fonts/)）一文，Harry Roberts 经过了一系列的测试，建议使用如下代码段提升使用了 Google Fonts 的网页的性能：

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

**参考资料**

- [《前端 CDNJS 库及 Google Fonts、Ajax 和 Gravatar 国内加速服务》，郭秀峰，2018-08-18。](https://sb.sb/blog/css-cdn/)  
  [https://sb.sb/blog/css-cdn/](https://sb.sb/blog/css-cdn/)
- [《最快的 Google Fonts》，Harry Roberts，王强译，2020-05-19。](https://cloud.tencent.com/developer/news/643958)  
  [https://www.infoq.cn/article/FVV9eEYjr3F8Tov2qYqP](https://www.infoq.cn/article/FVV9eEYjr3F8Tov2qYqP)
- [《国内外优秀前端 CDN，Google Fonts 国内镜像》，占奇，2017-04-25。](https://zhanqi.net/post/170425/)  
  [https://zhanqi.net/post/170425/](https://zhanqi.net/post/170425/)
- [《LUG@USTC Google Fonts 加速服务》，杨博远，2014-12-17。](https://lug.ustc.edu.cn/wiki/lug/services/googlefonts)  
  [https://lug.ustc.edu.cn/wiki/lug/services/googlefonts](https://lug.ustc.edu.cn/wiki/lug/services/googlefonts)
- [《Google 字体加速添加缓存》，高一凡，2015-09-24。](https://servers.ustclug.org/2015/09/google-revproxy-add-cache/)  
  [https://servers.ustclug.org/2015/09/google-revproxy-add-cache/](https://servers.ustclug.org/2015/09/google-revproxy-add-cache/)
- [《隆重介绍 思源黑体：一款Pan-CJK 开源字体》，Caleb Belohlavek，2014-07-15。](https://blog.typekit.com/alternate/source-han-sans-chs/)  
  [https://blog.typekit.com/alternate/source-han-sans-chs/](https://blog.typekit.com/alternate/source-han-sans-chs/)
- [《Source Han Serif 思源宋体：开源的泛 CJK 字体》，Adobe Systems Incorporated，2017。](https://source.typekit.com/source-han-serif/cn/)  
  [https://source.typekit.com/source-han-serif/cn/](https://source.typekit.com/source-han-serif/cn/)
- [《关于如何在网页中引入思源字体：漫谈 Typekit》，Jad，2018-07-02。](https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/)  
  [https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/](https://imjad.cn/archives/lab/how-to-introduce-source-han-fonts-into-web-pages-through-typekit/)
- [《走近 90 后创业者》，若涵，2014-03-28。](http://tech.sina.com.cn/i/special/startup90/)  
  [http://tech.sina.com.cn/i/special/startup90/](http://tech.sina.com.cn/i/special/startup90/)

## 2020-07-30

查资料的时候意外（又）注意到了 jsDelivr，研究了一下，了解到它可以给任何 GitHub 上的文件提供免费的 CDN 加速。

比如说，要用 jsDelivr 给 GitHub 上的某张图片加速，只需要使用 <span class="paths">https://cdn.jsdelivr.net/gh/用户名/图床仓库名/图片路径</span> 引用这张图片就行了。

一个具体的例子——

GitHub 的原始链接是这样的：

<span class="paths">https://raw.githubusercontent.com/shen-huang/img/master/2020-07/Visual_Studio_Code_Main_page.png</span>

对应的 jsDelivr 的加速链接则是这个：

<span class="paths">https://cdn.jsdelivr.net/gh/shen-huang/img/2020-07/Visual_Studio_Code_Main_page.png</span>

或者添加了版本的这个：

<span class="paths">https://cdn.jsdelivr.net/gh/shen-huang/img@master/2020-07/Visual_Studio_Code_Main_page.png</span>

如果设置了 Release 的版本，还可以引用对应版本的文件。

**参考资料**

- [《GitHub + jsDelivr + PicGo 打造稳定快速、高效免费图床》，TRHX，2019-08-01。](https://www.itrhx.com/2019/08/01/A27-image-hosting/)  
  [https://www.itrhx.com/2019/08/01/A27-image-hosting/](https://www.itrhx.com/2019/08/01/A27-image-hosting/)
- [《用 GitHub + PicGo + jsDelivr 打造高效的写作工作流，发布全平台》，Mask，2020-01-11。](https://www.jianshu.com/p/a78f558a74dc)  
  [https://www.jianshu.com/p/a78f558a74dc](https://www.jianshu.com/p/a78f558a74dc)
- [《记一下 jsDelivr 踩的坑》，石运鸿，2020-03-15。](https://blog.shiyunhong.com/3353.html)  
  [https://blog.shiyunhong.com/3353.html](https://blog.shiyunhong.com/3353.html)
- [《jsdelivr 加速资源加载：raw.github 被 ban 之后如何访问 GitHub 资源》，单林敏，2020-03-12。](https://blog.csdn.net/neve_give_up_dan/article/details/104817638)  
  [https://blog.csdn.net/neve_give_up_dan/article/details/104817638](https://blog.csdn.net/neve_give_up_dan/article/details/104817638)

## 2020-07-29

研究了一下 Jekyll、Hexo、Hugo，考虑将来用 Hugo 搭个 Blog。

**参考资料**

- [《Jekyll / Hugo / Hexo 比较》，曹历鑫，2019-10-30。](https://lexcao.github.io/zh/posts/jekyll-hugo-hexo)  
  [https://lexcao.github.io/zh/posts/jekyll-hugo-hexo](https://lexcao.github.io/zh/posts/jekyll-hugo-hexo)
- [Hugo Themes](https://themes.gohugo.io)  
  [https://themes.gohugo.io](https://themes.gohugo.io)

<!-- 
Fox.ONE 的大群机器人新增了视频直播回看的功能，我看了一下源代码，发现视频是 blob 加密的，好在可以直接打开开发工具、刷新页面、从 Network 分页里搜索“m3u8”找到原始链接，跟着用个 M3U8 的下载工具（我用的是稞麦）下载就行了。

**参考资料**

- [《下载blob加密的视频以及m3u8下载姿势合集》，yamakuchi，2019-05-11。](https://zhuanlan.zhihu.com/p/65425801)  
  [https://zhuanlan.zhihu.com/p/65425801](https://zhuanlan.zhihu.com/p/65425801)
- [《下载 blob视频, 如何下载网站中的blob:https:// 视频》，Gideon，2019-10-04。](https://justcode.ikeepstudying.com/2019/10/%E4%B8%8B%E8%BD%BD-blob%E8%A7%86%E9%A2%91-%E5%A6%82%E4%BD%95%E4%B8%8B%E8%BD%BD%E7%BD%91%E7%AB%99%E4%B8%AD%E7%9A%84blobhttps-%E8%A7%86%E9%A2%91/)  
  [https://justcode.ikeepstudying.com/2019/10/下载-blob视频-如何下载网站中的blobhttps-视频/](https://justcode.ikeepstudying.com/2019/10/%E4%B8%8B%E8%BD%BD-blob%E8%A7%86%E9%A2%91-%E5%A6%82%E4%BD%95%E4%B8%8B%E8%BD%BD%E7%BD%91%E7%AB%99%E4%B8%AD%E7%9A%84blobhttps-%E8%A7%86%E9%A2%91/)
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

**参考资料**

- [《CSS 世界》，张鑫旭，北京：人民邮电出版社，2017-12-01。](https://www.epubit.com/bookDetails?id=N2983)  
  [https://www.epubit.com/bookDetails?id=N2983](https://www.epubit.com/bookDetails?id=N2983)
- [《iCSS<span class="chs">·</span>谈谈一些有趣的CSS题目（1）——左边框的多种实现方式》，ChokCoco，2019-03-18。](https://github.com/chokcoco/iCSS/issues/51)  
  [https://github.com/chokcoco/iCSS/issues/51](https://github.com/chokcoco/iCSS/issues/51)
- [《Web 开发技术<span class="chs">·</span>CSS（层叠样式表）<span class="chs">·</span>z-index》，Mozilla 贡献者，2020-07-02。](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)  
  [https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)
- [《CSS：你真的会用 z-index 吗？》，WebJ2EE，2019-05-30。](https://juejin.im/post/5cee53f9f265da1bbd4b5746)  
  [https://juejin.im/post/5cee53f9f265da1bbd4b5746](https://juejin.im/post/5cee53f9f265da1bbd4b5746)
- [《Pro Git (2nd Edition)<span class="chs">·</span>2.5 Git 基础 - 远程仓库的使用》，Scott Chacon，Ben Straub，2014。](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)  
  [https://git-scm.com/book/zh/v2/Git-基础-远程仓库的使用](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)
- [git-remote, In *Reference of Git*. Retrieved 2020-07-28.](https://git-scm.com/docs/git-remote)  
  [https://git-scm.com/docs/git-remote](https://git-scm.com/docs/git-remote)
- [《git 中本地与远程库的关联与取消》，WuShiyuan，2016-01-24。](https://blog.csdn.net/wsycsdn19930512/article/details/50574217)  
  [https://blog.csdn.net/wsycsdn19930512/article/details/50574217](https://blog.csdn.net/wsycsdn19930512/article/details/50574217)
- [《成语运用二则：“不忍卒读”“不赞一词”》，赵丕杰，语文建设，2011年第1期。](http://www.yuyingchao.com/beike/html_qikan/yuwenjianshe_6/138959.html)  
  [http://www.yuyingchao.com/beike/html_qikan/yuwenjianshe_6/138959.html](http://www.yuyingchao.com/beike/html_qikan/qikanlunwen_138959.html)

## 2020-07-26

这个页面越写越长了，我想把它拆分一下，就建立了个文件夹，按天建立了一系列 Markdown 文件，结果导航栏变得相当难看。调试了一会儿没能搞定，只好退回了原有的版本。

考虑到可能只是暂时搁置，我没有删掉新建的文件夹和文件，而是在根目录新建了一个 <span class="paths">.gitignore</span> 文件，把现在不用的文件夹写了进去，避免将其上传到 GitHub。

由于间隔号（<span class="chs">·</span>）在<span class="typo-em">默认状态</span>下会用英文字体呈现，看上去不大美观，特别新增了一个样式 `.chs` 用来强制将某些文字使用中文字体呈现。

在折腾间隔号的时候，看到了“[漢字標準格式](https://hanzi.pro/)”（陳奕鈞 等，2015-10-27）、“[中文网页重设与排版：typo.css](https://typo.sofi.sh/)”（林建锋〔Sofish Lin〕，2019-01-21）等中文样式的优化方案，继而注意到了 [The Type (Type is Beautiful)](https://www.thetype.com/) 网站对超链接的处理——超链接文字颜色与正文基本一致，加灰色下划线进行标注，鼠标悬停时加深文字和下划线的颜色。对比所有超链接都用不同颜色加以修饰的做法，The Type 最后呈现的效果显得干净清晰又不突兀。

为了搞清楚要改什么地方，我做了一系列的样式跟踪，最后调整了主题当中 `--link-border-bottom`、 `--link-border-bottom--hover`、 `--link-color`、 `--link-color--hover` 几项的设置，另外给 `a` 和 `a:hover` 增加了样式，加大了 `padding-bottom`，完成后的观感还算令人满意。

在“[中文网页重设与排版：typo.css](https://typo.sofi.sh/)”处学到了着重号的设置方法，添加了 `.typo-em` 和 `.typo-em:after` 样式，实现了给中文加<span class="typo-em">着重号</span>的效果。

**参考资料**

- [《Git 教程<span class="chs">·</span>自定义 Git<span class="chs">·</span>忽略特殊文件》，廖雪峰，\[2020-07-26\]。](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)  
  [https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)
- [《为什么在有些软件环境下中文里的中圆点（间隔号）是半角的？》，梁海，2014-11-26。](https://www.zhihu.com/question/20271115/answer/14565424)  
  [https://www.zhihu.com/question/20271115/answer/14565424](https://www.zhihu.com/question/20271115/answer/14565424)
- [《GB/T 15834—2011 标点符号用法》，中华人民共和国国家质量监督检验检疫总局，2011-12-30。](http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf)  
  [http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf](http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf)
- [《HTML 下划线》，蓝蓝，2019-12-17。](https://lanlan2017.github.io/blog/9f0a034b/)  
  [https://lanlan2017.github.io/blog/9f0a034b/](https://lanlan2017.github.io/blog/9f0a034b/)
- [《零宽度字符：和谐？屏蔽？不存在的》，Yuan Fu，2018-09-03。](https://juejin.im/post/5b87a6e26fb9a019b953ee8b)  
  [https://juejin.im/post/5b87a6e26fb9a019b953ee8b](https://juejin.im/post/5b87a6e26fb9a019b953ee8b)
- [《饿了么如何落地和管理「大前端」团队？》，林建锋，2017/3/17。](https://sofi.sh/p/%E9%A5%BF%E4%BA%86%E4%B9%88%E5%A6%82%E4%BD%95%E8%90%BD%E5%9C%B0%E5%92%8C%E7%AE%A1%E7%90%86%E3%80%8C%E5%A4%A7%E5%89%8D%E7%AB%AF%E3%80%8D%E5%9B%A2%E9%98%9F%EF%BC%9F/)  
  [https://sofi.sh/p/饿了么如何落地和管理「大前端」团队？/](https://sofi.sh/p/%E9%A5%BF%E4%BA%86%E4%B9%88%E5%A6%82%E4%BD%95%E8%90%BD%E5%9C%B0%E5%92%8C%E7%AE%A1%E7%90%86%E3%80%8C%E5%A4%A7%E5%89%8D%E7%AB%AF%E3%80%8D%E5%9B%A2%E9%98%9F%EF%BC%9F/)
- [g0v 零&#8203;時&#8203;政&#8203;府](https://g0v.tw/zh-TW/)  
  [https://g0v.tw](https://g0v.tw/zh-TW/)
- [萌典](https://www.moedict.tw/)  
  [https://www.moedict.tw](https://www.moedict.tw/)

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

为了读写直观，参考[《创建漂亮的 CSS 按钮的 10 个代码片段》（Jake Rocheleau 著，IT程序狮子烨译，2017-03-06）](https://zhuanlan.zhihu.com/p/25597059)给 [docsify][] 加了按钮样式。

- 有些范例代码的样式和原本的样式冲突了，导致了意外的覆盖
    - 想要调整一下内容区的宽度，按照原始设计，只要修改 `--content-max-width` 的定义就可以了，但怎么改都不生效
    - 跟踪样式表，发现按钮样式里定义了 `.content` 的最大宽度，注释掉后正常了
- 因为现有样式的影响，按钮样式并没有完全按预定效果呈现，不过现有的效果已经足够用了
- 范例是用 `<a>` 来实现按钮的，实际用的时候改成了 `<button>`
- 顺便调整了“键盘按键”（`<kbd>`）的表现，参考了 [*Nice effect with the KBD tag* \(Réal Gagnon, 2012-12-26\)](https://www.rgagnon.com/jsdetails/js-nice-effect-the-KBD-tag.html)、[*CSS for the new \<kbd\> style* \(Israel Galvez, 2012-05-05\)](https://meta.superuser.com/questions/4788/css-for-the-new-kbd-style)

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
                        - 也可以在指令前添加 `sudo ` 来一次性地调用管理员权限执行命令
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
          可启动一个本地服务器，实时预览效果，默认访问地址为 [http://localhost:3000](http://localhost:3000)
        - 参考[docsify 官方文档][]（[https://docsify.js.org/#/zh-cn/](https://docsify.js.org/#/zh-cn/)）完成基础设置
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

**参考资料**

- [《基于Github Pages + docsify，我花了半天就搭建好了个人博客》，二营长，2020-01-05。](https://blog.csdn.net/m0_37965018/article/details/103841362)  
  [https://blog.csdn.net/m0_37965018/article/details/103841362](https://blog.csdn.net/m0_37965018/article/details/103841362)
- [《淺談新版 GitBook（GitBook V2）——失去交流開放精神的企業導向產品》，Yuni，2019-08-28。](https://www.onejar99.com/gitbook-v2-comment/)  
  [https://www.onejar99.com/gitbook-v2-comment/](https://www.onejar99.com/gitbook-v2-comment/)
- [《如何看待 GitBook 的改版？》，Lellansin Huang，2018-04-11。](https://www.zhihu.com/question/271881476)  
  [https://www.zhihu.com/question/271881476](https://www.zhihu.com/question/271881476)
- [《關於 GitBook 平台的改版與 GitLab 替代的考量》，王克明，2018-09-27。](https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/)  
  [https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/](https://www.kenming.idv.tw/about_gitbook-v2_and_gitlab_alternative/)
- [《CSS中的 “var()” 和 “:root”》，ArvinWoo，2018-11-26。](https://blog.csdn.net/qq_37595946/article/details/84531311)  
  [https://blog.csdn.net/qq_37595946/article/details/84531311](https://blog.csdn.net/qq_37595946/article/details/84531311)
- [《Web 开发技术<span class="chs">·</span>CSS（层叠样式表）<span class="chs">·</span>var()》，Mozilla 贡献者，2019-11-13。](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)  
  [https://developer.mozilla.org/zh-CN/docs/Web/CSS/var](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)

## 2020-07-16

为了方便使用，把课程和笔记相关的文件夹固定到了资源管理器的快速访问区，然后就觉得那两个默认图标不大协调，就转去研究自定义文件夹图标了，搞清楚设置过程没花太多时间，但搞好要用的图标费了不少劲。

最后自制了四个图标，基本上够用了，还有一点没什么影响的瑕疵，暂时我也不想再折腾了。

具体过程整理成了[《设置文件夹》](/a-appendix/setting-folders.md)一文，可供参考。

## 2020-07-14

用了两天多的时间做功课，参考[《GitBook 教程（小白入坑 GitBook 全过程）》（Broken故城，2020-02-20）](https://www.jianshu.com/p/0388d8bb49a7)、[《GitBook 使用教程》（yulilong，2019-01-21）](https://segmentfault.com/a/1190000017960359)，在 GitBook 新建了一个“Space”（[https://shen-huang.gitbook.io/wop-notes-win/](https://shen-huang.gitbook.io/wop-notes-win/)），关联到了 GitHub 仓库。

## 2020-07-13

为了在苹果 App Store 美国区买应用，完整地跑了一遍用信用卡在[苹果官网买电子版礼品卡](https://www.apple.com/shop/gift-cards)的流程，不必登录账号，直接用访客身份购买即可，地址要写美国免税州里的（只有 5 个：Alaska、Delaware、Montana、New Hampshire、Oregon，Alaska 和 Montana 可能还有潜在税收，尽量不要写这两个），用 [Fake Address Generator](https://www.fakeaddressgenerator.com/) 生成即可。

**参考资料**

- [《通过购买礼品卡（Gift Cards）给美国 Apple ID 充值方法》，陈浩，2019-08-09](https://www.hurbai.com/iOS/182)  
  [https://www.hurbai.com/iOS/182](https://www.hurbai.com/iOS/182)
- [The 5 U.S. States Without a Statewide Sales Tax: Where to Do Your Purchasing in the U.S., In *The Balance*. Retrieved 2020-07-14.](https://www.thebalance.com/states-without-a-sales-tax-3193305)  
  [https://www.thebalance.com/states-without-a-sales-tax-3193305](https://www.thebalance.com/states-without-a-sales-tax-3193305)
- [《苹果突然封号，iPhone 这个漏洞，千万别碰》，雷科技，2020-01-22。](https://36kr.com/p/1725033807873)  
  [https://mp.weixin.qq.com/s/gBVQcv7cIYLalqbhV8pvOw](https://mp.weixin.qq.com/s/gBVQcv7cIYLalqbhV8pvOw)

## 2020-07-12

想好好给李骏老师的课程《进入编程世界》写个笔记，2019 年做类似事情的时候，我就在 GitHub 仓库的 <span class="paths">README.md</span> 里写了，写了一阵子发现多少有点不方便：单页难以检索，分页跳转麻烦，样式限制很多，扩展能力孱弱。毕竟，<span class="paths">README.md</span> 不是用来写复杂文档的。

我首先想到的替代方案，是 GitBook。2015 年的时候李笑来老师用 GitBook 做了在线版本的[《把时间当作朋友（第 3 版）》](https://legacy.gitbook.com/book/xiaolai/ba-shi-jian-dang-zuo-peng-you/details)，当时还基于它搞了“知笔墨”（已停止运维，旧页面可以从互联网档案馆的[网站时光机相关快照](https://web.archive.org/web/20180806235112/http://www.zhibimo.com/explore/books)里查看），我也因此对 GitBook 有了些感性认识。

完整地看了几遍[《GitBook 文档（中文版）》（Samy Pessé 等著，沈煜 译，2016-12-12）](https://chrisniael.gitbooks.io/gitbook-documentation/content/)，打算明后天着手正式搭建。

## 2020-07-11

为了醒目、好看，我以往记录快捷键的时候如果遇到“Windows 键”，可能会额外多贴一个小图来表示：<kbd>![Win][Windows_Logo_12px] Win</kbd>，今天发现维基百科的处理方式是借用字符“⊞”，写成<kbd>⊞ Win</kbd>，看上去也能接受，不失为一种处理方法。

**参考资料**

- [Windows key, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Windows_key)  
  [https://en.wikipedia.org/wiki/Windows_key](https://en.wikipedia.org/wiki/Windows_key)
- [Is there a unicode character for the Windows key? Gabriel Fair, 2017-04-09.](https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key)  
  [https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key](https://superuser.com/questions/1247382/is-there-a-unicode-character-for-the-windows-key)
- [The Ultimate Guide to Windows Keyboard Shortcuts. HelloTech, 2017-01-16.](https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts)  
  [https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts](https://www.hellotech.com/blog/every-switchers-guide-to-windows-10-shortcuts)

## 2020-07-10

Windows Terminal 对操作系统版本有要求（至少 18362.0，也就是 1903），这引发了一系列问题。

为了用起来稳定、方便维护，我的台式机使用了从 VHDX 启动的 Windows 10 Enterprise 2019 LTSC，这个 Windows 10 分支的主版本是 1809，就算另外加装了 Microsoft Store 也装不了 Windows Terminal，LTSC 版和 VHDX 又都会导致无法进行大版本升级。

我把系统转换成了 Windows 10 Pro，避开了 LTSC 的限制，但 VHDX 升级的限制没法绕过去。我只好在硬盘另外划分出来了一个分区，把 VHDX 的内容用分区复制的方式倒了进去，然后用这个新分区启动。启动、升级完成后，我想把这个系统再倒回 VHDX 里，用不同的分区复制的方式试验了数次，都无法启动，最终放弃了，决定就在这个用实体分区启动的 Windows 10 Pro 上完成课程的学习。

**参考资料**

- [《将 Windows 10 LTSC 版转换为专业版激活，使用纯净无预装的 Windows 10》，王洪峰，2019-04-12。](https://wanghongfeng.cn/LTSC2019.html)  
  [https://wanghongfeng.cn/LTSC2019.html](https://wanghongfeng.cn/LTSC2019.html)

## 2020-07-09

怎么都搞不定 macOS 上 Python 3.x 软链接的建立，按照说明折腾了一阵子，`python` 命令调用的一直是系统自带的 Python 2.7.3，虽然用 `python3` 也能解决问题，但我就是不服气，于是就干了“撞破南墙”的事情。

我找到了系统自带的 Python 2.7.3 的位置：<span class="paths">/usr/bin/python</span>，但这个位置是系统管理的，用户不能直接操作，为了动它，我重开机，用 <kbd>⌘ Command</kbd> + <kbd>R</kbd> 进了 macOS 实用工具，然后运行 `csrutil disable` 关闭了 SIP（System Integrity Protection），然后获取了 <span class="paths">/usr/bin/ 的最高权限（777），把 <span class="paths">/usr/bin/python</span> 这个软链接删了，在原位置建立了到 <span class="paths">/usr/local/bin/python3</span> 的软链接。

这么弄完，`python` 命令调用的确实是 Python 3.x 了，可是李骏老师告知我这个方法大错特错——macOS 不让用户动某些东西是有道理的，而且确实不应该动。我在老师的帮助下，明确了原本系统的软链接的路径，但由于我动了底层的设置，Terminal 无法正常工作了，在 macOS 实用工具里也处理不了……

为了能正常用 Terminal，我手动建立了 root 账号，在其中还原了最初的软链接，又重新打开了 SIP，删掉了 root 账号，这才回到了起点。

我无奈之下提了个 Issue：“[无法在 macOS 的 Terminal 使用 `python` 指令调用 Python 3.7.x](https://github.com/neolee/wop-community/issues/88)”，经过一系列排查和尝试，最后靠强制建立软链接搞好了，但这应该也不是问题的根源，李骏老师最后说：因为现场很难还原，当时到底发生了什么已不可考，施主请放下吧……

**参考资料**

- [《5 分钟让你明白“软链接”和“硬链接”的区别》，Cyandev，2016-07-08。](https://www.jianshu.com/p/dde6a01c4094)  
  [https://www.jianshu.com/p/dde6a01c4094](https://www.jianshu.com/p/dde6a01c4094)
- [Fix Terminal “Operation not permitted” Error in MacOS Mojave. Paul Horowitz, 2018-10-09.](https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/)  
  [https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/](https://osxdaily.com/2018/10/09/fix-operation-not-permitted-terminal-error-macos/)
- [How to Disable System Integrity Protection (rootless) in Mac OS X. Paul Horowitz, 2015-10-05.](https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/)  
  [https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/](https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/)
- [《macOS 开启或关闭 SIP》，雪谋，2019-06-07。](https://sspai.com/post/55066)  
  [https://sspai.com/post/55066](https://sspai.com/post/55066)
- [《MacOS (Catalina)：显示 Read-only file system 的对应方法》，liumiaocn，2020-02-15。](https://blog.csdn.net/liumiaocn/article/details/104324664)  
  [https://blog.csdn.net/liumiaocn/article/details/104324664](https://blog.csdn.net/liumiaocn/article/details/104324664)
- [《macOS Catalina 无法删除 /usr/bin/ 下面的文件》，高金，2019-10-10。](https://igaojin.me/2019/10/10/Mac-catalina-%E6%97%A0%E6%B3%95%E5%88%A0%E9%99%A4-usr-bin-%E4%B8%8B%E9%9D%A2%E7%9A%84%E6%96%87%E4%BB%B6/)  
  [https://igaojin.me/2019/10/10/Mac-catalina-无法删除-usr-bin-下面的文件/](https://igaojin.me/2019/10/10/Mac-catalina-%E6%97%A0%E6%B3%95%E5%88%A0%E9%99%A4-usr-bin-%E4%B8%8B%E9%9D%A2%E7%9A%84%E6%96%87%E4%BB%B6/)
- [《macOS 修改 /usr/bin/ 权限后导致控制台无法使用》，迷途中的小码农，2019-04-18。](https://blog.csdn.net/ethan__xu/article/details/89390220)  
  [https://blog.csdn.net/ethan__xu/article/details/89390220](https://blog.csdn.net/ethan__xu/article/details/89390220)

## 2020-07-08

了解了一下 Shell、Bash、Zsh 等概念，顺带明确了 <span class="paths">.bash_profile</span>、<span class="paths">.bashrc</span>、<span class="paths">.zshrc</span> 这几个文件的关系。考虑到很多同学可能并没有从 Bash 切换到 Zsh，我就暂时停在了 Bash，主要调整了 <span class="paths">.bash_profile</span> 文件，加入了代理和关闭 Zsh 升级提示的设置，打算明天再分享一次，附带说明一下怎么可以“一劳永逸”地解决 macOS 的 Terminal 的网络代理设置问题。

编辑 <span class="paths">.bash_profile</span> 文件可能会遇到麻烦（很多文档都教读者用 VIM 来做这事，对初学者真的……不够友好），这事可以用 Visual Studio Code（下简称 VS Code）来做，在 Terminal 里输入并运行 `code ~/.bash_profile` 就能用 VS Code 打开这个文件了。如果因为种种原因，还没装 VS Code，则可以在 Terminal 里输入并运行 `open ~/.bash_profile`，这样会使用 macOS 自带的“文本编辑”打开这个文件，编辑起来会比 VIM 容易上手一些。

**参考资料**

- [《你明白 Shell、Bash 和 Zsh 等词的真正含义吗？》，阿德，2018-03-03。](https://zhuanlan.zhihu.com/p/34197680)  
  [https://zhuanlan.zhihu.com/p/34197680](https://zhuanlan.zhihu.com/p/34197680)
- [《终极 Shell》，池建强，2013-07-23。](http://macshuo.com/?p=676)  
  [http://macshuo.com/?p=676](http://macshuo.com/?p=676)
- [《让你的 Mac 提前用上 macOS Catalina 的 Shell —— Oh My Zsh 配置指南》，Steven，2019-06-12。](https://sspai.com/post/55176)  
  [https://sspai.com/post/55176](https://sspai.com/post/55176)
- [《关于“.bash_profile”和“.bashrc”区别的总结》，史晨，2017-04-20。](https://blog.csdn.net/sch0120/article/details/70256318)  
  [https://blog.csdn.net/sch0120/article/details/70256318](https://blog.csdn.net/sch0120/article/details/70256318)
- [《Mac 更新之后使用终端提示：The default interactive shell is now zsh.》，深碍，2019-12-26。](https://www.jianshu.com/p/26d365078081)  
  [https://www.jianshu.com/p/26d365078081](https://www.jianshu.com/p/26d365078081)
- [Bash, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Bash_(Unix_shell))  
  [https://en.wikipedia.org/wiki/Bash_(Unix_shell)](https://en.wikipedia.org/wiki/Bash_(Unix_shell))
- [Z shell, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-08.](https://en.wikipedia.org/wiki/Z_shell)  
  [https://en.wikipedia.org/wiki/Z_shell](https://en.wikipedia.org/wiki/Z_shell)

## 2020-07-07

计划在 Mixin Messenger 群里开个分享，讲讲如何解决编程课遭遇的各种网络问题，为了应对更多的需求，专门把 macOS 上的情况也测试了一遍，然后发现 macOS Catalina (10.15) 有个“无法验证开发者就阻止程序运行”的坑。

“无法验证开发者”的问题，可以在访达的“应用程序”里，按住 <kbd>Control</kbd> 的同时，用鼠标左键单击需要打开的应用的图标，再单击 <span class="menutext">打开</span>，就会弹出可供跳过验证、打开应用的对话框了。

## 2020-07-06

想要搞一下 Windows Terminal 的美化，然后就陷入了巨量的选项之中。

首先看到了[李欢](https://www.zhihu.com/people/lihuan123) 2020 年 4 月 27 日写的[《简单配置与美化 PowerShell 和 Terminal》](https://zhuanlan.zhihu.com/p/104720872)，和 [Clint Richardson](https://twitter.com/clinterich) 2019 年 8 月 2 日写的[《*The New Windows Terminal – Install, Interact, and Customize*》](https://www.appliedis.com/the-new-windows-terminal-install-interact-and-customize/)。

跟着研究了一下 [posh-git](https://github.com/dahlbyk/posh-git)，以及 [Windows Terminal Themes](https://atomcorp.github.io/themes/) 里让人眼花缭乱的主题配色，还参考了 [Thomas Maurer](https://www.thomasmaurer.ch/) 2020 年 6 月 14 日的相关推荐文章[《*My Windows Terminal Color Schemes*》](https://www.thomasmaurer.ch/2020/06/my-windows-terminal-color-schemes/)。

这些折腾完，就轮到了字体，用于代码的等宽字体其实有不少可选项，但一混上中文情况就不妙了，理想的情况是 1 个中文字宽等于 2 个英文字宽，中英文混杂的行也能够纵向对齐，实际上这很难准确实现。我试了民间自制的 YaHei Consolas Hybrid（微软雅黑和 Consolas 的混合字体）、Microsoft Yahei Mono（也是微软雅黑和 Consolas 的混合字体）、Yahei Source Code Pro（微软雅黑和 Source Code Pro 的混合字体），都对不齐。专门用于这一目的制作的“等距更纱黑体”，对齐倒是很完美，但英文部分实在是显得太窄了，看着累人，最后我选择了保持原状，将来再折腾吧…… 

**参考资料**

- [《美化 Windows Terminal（iTerm2-Color-Schemes)》，Jioho_chen，2019-09-08。](https://blog.csdn.net/Jioho_chen/article/details/100624029)  
  [https://blog.csdn.net/Jioho_chen/article/details/100624029](https://blog.csdn.net/Jioho_chen/article/details/100624029)
- [《Retina 屏幕上的最佳编程字体》，Lenciel，2014-07-13。](https://lenciel.com/2014/07/font-for-programming/)  
  [https://lenciel.com/2014/07/font-for-programming/](https://lenciel.com/2014/07/font-for-programming/)
- [《推荐的编程字体》，余淦成，2015-08-08。](https://www.ifeegoo.com/recommended-programming-fonts.html)  
  [https://www.ifeegoo.com/recommended-programming-fonts.html](https://www.ifeegoo.com/recommended-programming-fonts.html)
- [What are the best programming fonts? *Slant*, Retrieved 2020-07-06.](https://www.slant.co/topics/67/~best-programming-fonts)  
  [https://www.slant.co/topics/67/~best-programming-fonts](https://www.slant.co/topics/67/~best-programming-fonts)
- [《编程字体》，bayhiker，2019-09-25。](https://blog.rule55.com/coding-fonts/)  
  [https://blog.rule55.com/coding-fonts/](https://blog.rule55.com/coding-fonts/)
- [《推荐几款连字字体，在代码编辑器中启用连字字体（Visual Studio Code）》，吕毅，2019-09-27。](https://blog.csdn.net/WPwalter/article/details/101512456)  
  [https://blog.csdn.net/WPwalter/article/details/101512456](https://blog.csdn.net/WPwalter/article/details/101512456)
- [《CSS font-family 常见中文字体对应的英文名称》，张鑫旭，2017-03-25。](https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/)  
  [https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/](https://www.zhangxinxu.com/wordpress/2017/03/css-font-family-chinese-english/)
- [《Fira Code | 为写程序而生的字体》，Mogeko，2017-09-16。](https://www.jianshu.com/p/266b4fa2c446)  
  [https://mogeko.me/2017/006/](https://mogeko.me/2017/006/)
- [《Fira Code: 一个有趣而实用的编程字体》，Luo Jia，2018-06-20。](https://luojia.cc/2018/06/20/font-fira-code/)  
  [https://luojia.cc/2018/06/20/font-fira-code/](https://luojia.cc/2018/06/20/font-fira-code/)
- [《分享一下自己修改的字体~ Yahei Source Code Pro v1.23》，DeepKolos，2017-07-15。](https://www.jianshu.com/p/28acf9226ddb)  
  [https://www.jianshu.com/p/28acf9226ddb](https://www.jianshu.com/p/28acf9226ddb)
- [YaHei Consolas Hybrid 和 Yahei Source Code Pro 的下载页面](https://github.com/yyxyz/OSOperateSkills/find/master)  
  [https://github.com/yyxyz/OSOperateSkills/find/master](https://github.com/yyxyz/OSOperateSkills/find/master)
- [更纱黑体主仓库](https://github.com/be5invis/Sarasa-Gothic)  
  [https://github.com/be5invis/Sarasa-Gothic](https://github.com/be5invis/Sarasa-Gothic)
- [Iosevka 字体主页](https://typeof.net/Iosevka/)  
  [https://typeof.net/Iosevka/](https://typeof.net/Iosevka/)

## 2020-07-05

有同学称自己安装 Scoop 的时候被杀毒软件挡住了，查了一下，发现是“联想杀毒 Plus”和“联想电脑管家”，进一步挖掘得知，联想杀毒 Plus 是基于 McAfee 的，联想电脑管家是基于火绒的，类似于加壳改名。据说这两个软件都不算好用，甚至有联想客服建议卸载随机自带的联想杀毒 Plus。

将这两个软件卸载并启用 Windows 10 自带的 Defender 后，问题解决。

**参考资料**

- [《联想杀毒 PLUS》，wildtree23，2020-06-05。](https://bbs.kafan.cn/thread-2183667-1-1.html)  
  [https://bbs.kafan.cn/thread-2183667-1-1.html](https://bbs.kafan.cn/thread-2183667-1-1.html)
- [《【联想客服内部超级爆料】你的联想杀毒 Plus 安全软件卸载了没有？》，1T科技，2020-06-14。](https://www.bilibili.com/video/BV1Bk4y1z7d5)  
  [https://www.bilibili.com/video/BV1Bk4y1z7d5](https://www.bilibili.com/video/BV1Bk4y1z7d5)

## 2020-07-04

在交流群里有人问命令开头那个 `$` 是什么意思，被告知是“提示符”，也就是系统告诉你可以输入命令了。很多人搞不清楚这件事，照着说明把 `$` 一起敲进命令里运行，跟着就出错。

不过我因此生出了另一个问题：为什么是 `$`？

在网上做了一阵子功课后发现，`$` 的使用可以追溯到 1979 年发布的 Version 7 Unix 系统，这个选择可能来自于早在 1963 年就面世的电传打字机 Teletype Model 33 ASR (**A**utomatic **S**end and **R**eceive)——由于其键盘上可用的符号很少，提示符又需要“尽量简短”且“不易混淆”，最终，工程师挑选了 `$`。另一个可能来源，是 1962 年 IBM 推出的 FORTRAN IV，那个时期的计算机还没有键盘和显示器，所有的程序输入都靠打孔卡片实现，程序输出则靠打印机实现，在输出的时候，FORTRAN IV 使用了 `$` 来标记那些输入的命令。

在 1979 年之前，Unix 系统使用的 Shell 是“C Shell”，其默认的提示符是“`%`”，Version 7 Unix 系统使用了 Stephen Bourne 开发的“Bourne Shell”，其默认提示符选择了“`$`”，在随后的时光中，Version 7 Unix 系统产生了巨大的影响，`$` 也成为了 Unix 系统和类 Unix 系统惯用的提示符。macOS 的内核是从 Unix 的分支开发而来的，也就继承了使用 `$` 的传统。

Version 7 Unix 系统还给出了“次要提示符”“`>`”，我们可以进行一点合理推测——这就是 DOS（1981 年推出）和之后的 Windows（1985 年推出）默认的提示符的起源。

除了 `$`、`%`、`>` 之外，`#` 也在某些情况下被用作提示符，可以想见，其实任何“尽量简短”且“不易混淆”的符号在这个上下文中都是合理的，我们现在看到的境况，与其说是有意的设计，不如说是历史的选择，而这种选择，有着各种各样的机缘和巧合。

**参考资料**

- [What is the origin of the UNIX $ (dollar) prompt? Max Howell, 2009-10-19.](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)  
  [https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)
- [Why was the dollar sign chosen as the Unix shell prompt? Eduardo Sangiorgio Dobay, 2015-07-21.](https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt)  
  [https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt](https://www.quora.com/Why-was-the-dollar-sign-chosen-as-the-Unix-shell-prompt)
- [Teletype Model 33, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Teletype_Model_33)  
  [https://en.wikipedia.org/wiki/Teletype_Model_33](https://en.wikipedia.org/wiki/Teletype_Model_33)
- [What does the $ mean when running commands? Joshua Paul A. Chan, 2013-11-14.](https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands)  
  [https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands](https://stackoverflow.com/questions/19986306/what-does-the-mean-when-running-commands)
- [SH(1), In *UNIX Programmer’s Manual, Seventh Edition, Volume 1*. Bell Telephone Laboratories, Incorporated. 1979-01.](https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf)  
  [https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf](https://s3.amazonaws.com/plan9-bell-labs/7thEdMan/v7vol1.pdf)
- [Digital computing, FORTRAN IV, WATFIV, and MTS (with \*FTN and \*WATFIV). Brice Carnahan, James O. Wilkes. Ann Arbor: Chemical Engineering Dept., University of Michigan. 1976. p. 2-76.](https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false)  
  [https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false](https://books.google.com/books?id=59NWAAAAMAAJ&pg=SA2-PA76&lpg=SA2-PA76&source=bl&ots=bcFlvL4yoD&sig=5fp9RRtAzPfUzTWGgpXWrXXLojw&hl=en&sa=X&redir_esc=y#v=onepage&q&f=false)
- [Command-line interface, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Command-line_interface#Command_prompt)  
  [https://en.wikipedia.org/wiki/Command-line_interface](https://en.wikipedia.org/wiki/Command-line_interface)
- [Unix, In *Wikipedia, the free encyclopedia*. Retrieved 2020-07-04.](https://en.wikipedia.org/wiki/Unix)  
  [https://en.wikipedia.org/wiki/Unix](https://en.wikipedia.org/wiki/Unix)
- [DOS 1.0 booted. Michal Necasek, 2011-08-03.](http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/)  
  [http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/](http://www.os2museum.com/wp/dos/dos-1-0-and-1-1/dos-1-0-boot/)
- [ALL VERSIONS OF MS-DOS (1.0-8.0). Windows Expert, 2019-08-02.](https://www.youtube.com/watch?v=5cS-PIuyEhU)  
  [https://www.youtube.com/watch?v=5cS-PIuyEhU](https://www.youtube.com/watch?v=5cS-PIuyEhU)
- [《Unix, Linux 和 macOS》，keith，2019-05-11。](https://juejin.im/post/5cd5d1b4518825686761cc1f)  
  [https://juejin.im/post/5cd5d1b4518825686761cc1f](https://juejin.im/post/5cd5d1b4518825686761cc1f)

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

<!-- 
图片
 -->

[Windows_Logo_20px]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/20px-Windows_logo_2012-Black.svg.png
[Windows_Logo_16px]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Windows_logo_2012-Black.svg/16px-Windows_logo_2012-Black.svg.png
[Windows_Logo_12px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_12px.svg?sanitize=true
[Windows_Logo_8px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_8px.svg?sanitize=true
[Windows_Logo_6px]: https://raw.githubusercontent.com/shen-huang/img/master/Logo/Windows_logo_2012-Black_6px.svg?sanitize=true
