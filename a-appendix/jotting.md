# 随记

这里是一些我在学习过程中“注意力漂移”的记录。

## 2020-07-22

在搜索资料的时候撞进了 MegaEase 创始人陈皓的个人网站“[酷壳](https://coolshell.cn/)”（[CoolShell.cn](https://coolshell.cn/)），发现这是个颇有能力的人，他 2019 年 12 月 1 日的一篇文章[《别让自己“墙”了自己》](https://coolshell.cn/articles/20276.html)非常值得一读，另一篇写于 2019 年 11 月 3 日的[《UNIX 50 年：KEN THOMPSON 的密码》](https://coolshell.cn/articles/19996.html)也很有意思。

[《如何写出无法维护的代码》（陈皓，2011-06-03）](https://coolshell.cn/articles/4758.html)很契合本次课程的学习，作为一篇“反面教材”，这篇文章里展现的种种行为可谓令人印象深刻。

## 2020-07-20

2020 年 1 月 15 日，微软正式推出了以 Chromium 为内核的新版 Microsoft Edge。我想使用新版的 Edge，又不想就此抛弃 EdgeHTML 内核，就没有使用直接升级的办法，而是使用了 [PortableSoft][] 提供的基于启动器的 [Microsoft Edge 绿色版](https://www.portablesoft.org/microsoft-edge-portable/)（此处为最新版，过去的版本可以在“[Microsoft Edge 历史版本/旧版本下载](https://www.portablesoft.org/microsoft-edge-old-version/)”页面下载）。

近几日 Edge 一直提示我要升级，PortableSoft 的这个启动器没有提供自动升级功能，只能下载新版手工处理升级，处理之余，我翻了翻 PortableSoft，发现这个站也把其提供的 [ABBYY FineReader PDF](https://pdf.abbyy.com/) 的链接换成了思杰马克丁的版本，估计可能是因为想避免麻烦。

苏州的思杰马克丁公司，是家很有特色的公司，从知乎的一个问答“[如何评价苏州思杰马克丁软件公司？](https://www.zhihu.com/question/46746200)”中就可见一斑，虽然很多事情我已经有所了解了，但还是忍不住又花了些时间更新了一下相关信息，顺带又浏览了一遍 [FXXKMAKEDING](https://www.fxxkmakeding.xyz/)。

## 2020-07-18

因为觉得 [docsify][] 的 [docsify-themeable 主题][]原始的配色稍微有些不合心意，又因此做了一串功课。

- 尝试找出原始的配色，但是用 `:root` 和 `var()` 写出来的样式表调试不难、阅读不易，前前后后找了好久，还动用了浏览器的“开发人员工具”（快捷键 <kbd>F12</kbd> 或者 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>），对样式做了一系列的跟踪才最终确定。
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
    - GitBook 现在的免费的“空间”数量非常有限，这显然是受到了 GitBook 商业化运营的影响
    - 网上大量 GitBook 的资讯现在都已经严重过时，新版的帮助文档也不够完整好用
    - GitBook 对样式的过滤和 GitHub 一样严格，连给文字加个颜色都没办法
- 放弃 GitBook，备份、删库，做了些功课后决定改用 [docsify][]
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
- [《CSS中的 “var()” 和 “:root”》，ArvinWoo，2018-11-26。](https://blog.csdn.net/qq_37595946/article/details/84531311)  
  [https://blog.csdn.net/qq_37595946/article/details/84531311](https://blog.csdn.net/qq_37595946/article/details/84531311)
- [《var()》，Mozilla 贡献者，2019-11-13。](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)  
  [https://developer.mozilla.org/zh-CN/docs/Web/CSS/var](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)

## 2020-07-16

## 2020-07-14

想好好给李骏老师的课程《进入编程世界》写个笔记，参考[《GitBook 教程（小白入坑 GitBook 全过程）》（Broken故城，2020-02-20）](https://www.jianshu.com/p/0388d8bb49a7)、[《GitBook 使用教程》（yulilong，2019-01-21）](https://segmentfault.com/a/1190000017960359)，在 GitBook 新建了一个“Space”，关联到了 GitHub 的仓库。

## 2020-07-09

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

这些折腾完，就轮到了字体，用于代码的等宽字体其实有不少可选项，但一混上中文情况就不妙了，理想的情况是 1 个中文字宽等于 2 个英文字宽，中英文混杂的行也能够纵向对齐，实际上这很难准确实现。我试了民间自制的 YaHei Consolas Hybrid（微软雅黑和 Consolas 的混合字体）、Microsoft Yahei Mono（也是微软雅黑和 Consolas 的混合字体）、Yahei Source Code Pro（微软雅黑和 Source Code Pro 的混合字体），都对不齐。专门用于这一目的制作的“等距更纱黑体”，对齐倒是很完美，但英文部分实在是显得太窄了，看着累人，最后我使用了 Fira Code 和汉仪旗黑的搭配。 

**参考资料**

- [《美化 Windows Terminal（iTerm2-Color-Schemes)》，Jioho_chen，2019-09-08。](https://blog.csdn.net/Jioho_chen/article/details/100624029)  
  [https://blog.csdn.net/Jioho_chen/article/details/100624029](https://blog.csdn.net/Jioho_chen/article/details/100624029)
- [《Retina 屏幕上的最佳编程字体》，Lenciel，2014-07-13。](https://lenciel.com/2014/07/font-for-programming/)  
  [https://lenciel.com/2014/07/font-for-programming/](https://lenciel.com/2014/07/font-for-programming/)
- [《推荐的编程字体》，余淦成，2015-08-08。](https://www.ifeegoo.com/recommended-programming-fonts.html)  
  [https://www.ifeegoo.com/recommended-programming-fonts.html](https://www.ifeegoo.com/recommended-programming-fonts.html)
- [What are the best programming fonts? *Slant*, Retrieved 2020-07-06.](https://www.slant.co/topics/67/~best-programming-fonts)  
  [https://www.slant.co/topics/67/~best-programming-fonts](https://www.slant.co/topics/67/~best-programming-fonts)
- [《Fira Code | 为写程序而生的字体》，Mogeko，2017-09-16。](https://www.jianshu.com/p/266b4fa2c446)  
  [https://mogeko.me/2017/006/](https://mogeko.me/2017/006/)
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

在网上做了一阵子功课后发现，`$` 的使用可以追溯到 1979 年发布的 Version 7 Unix 系统，这个选择可能来自于早在 1963 年就面世的电传打字机 Teletype Model 33 ASR (**A**utomatic **S**end and **R**eceive)——由于其键盘上可用的符号很少，提示符又需要“尽量简短”且“不易混淆”，最终，工程师挑选了 `$`。另一个可能来源，是 1962 年 IBM 推出的 FORTRAN IV，那个时期的计算机还没有键盘和显示器，所有的程序输入打孔卡片实现，程序输出则靠打印机实现，在输出的时候，FORTRAN IV 使用了 `$` 来标记那些输入的命令。

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

- Windows Terminal 对操作系统版本有要求（至少 18362.0，也就是 1903），这引发了一系列问题
    - 为了用起来稳定一些，我使用了 Windows 10 Enterprise 2019 LTSC，它的主版本是 1809，就算另外加装了 Microsoft Store 也装不了 Windows Terminal
    - 为了升级，我把系统转换成了 Windows 10 Pro，但因为之前为了方便维护，我是从 VHDX 启动的系统，这样的系统没法进行大版本升级
    - 在硬盘另外划分出来了一个分区，把 VHDX 的内容用分区复制的方式倒了进去，然后用这个新分区启动
    - 启动、升级完成后，我想把这个系统再倒回 VHDX 里，用不同的分区复制的方式试验了数次，都无法启动，最终放弃了
- Scoop 安装的时候要访问 [raw.githubusercontent.com](raw.githubusercontent.com)，这可能遭遇各种网络问题
    - 改本地 hosts 无效
    - 修改 DNS 服务器设置无效
    - Windows Terminal 是个 UWP 应用，默认没法加本地代理，最后用 Clash for Windows 带的 AppContainer Loopback Exemption Utility（又称 UWP Loopback Helper）给它加上了代理
- Homebrew 的安装遇到了和 Scoop 一样的网络问题
    - 可以用 `export` 命令给 Terminal 设置代理
    - 为了将来方便，把代理设置写入了 <span class="paths">.bash_profile</span>
- 在 macOS 上为 `python` 建立软链接的时候怎么都无法生效
    - 打破了 macOS Catalina 设置的各种权限，最终替掉了系统自带的 Python 2.7 的软链接
    - 由于对系统核心的设置进行了修改，Terminal 无法正常工作了
    - 单独建立了 root 账户，把系统还原
    - 使用强制建立软链接的方式实现了最初的目的
    - 删除软链接、再使用原本的方式建立软链接，也没问题了
    - 故障原因最终未查明

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