# 格式化文本测试

## 使用 `<span>` 添加样式

```html
<span style="color:red;">红色文字</span>
```

<span style="color:red;">红色文字</span>

```html
<span style="border: medium solid red;">边框</span>
```

<span style="border: medium solid red;">边框</span>

## 使用 `<font>` 添加格式（不推荐）

```html
<font color="#f00;">红色文字</font>
```

<!-- <font color="#f00;">红色文字</font> -->

## 路径

```html
<span class="paths">%SystemRoot%\System32\\</span>
```

<span class="paths">%SystemRoot%\System32\\</span>

## 中文标点

```html
<span class="chs">“‘’”</span>
```

<span class="chs">“‘’”</span>

## 间隔号

```html
<span class="chs">·</span>
```

<span class="chs">·</span>

间隔号也可使用日文的 `・`（U+30FB Katakana Middle Dot）来代替  
・

## 着重号

```html
<span class="typo-em">字下加点</span>
```

<span class="typo-em">字下加点</span>

## 注释

```html
<span class="commentary">文内注释</span>
```

<span class="commentary">文内注释</span>

## 引用

```markdown
一段普通的正文

> 常见的  
> **多行**  
> 引用文本  
>
> 以及可能包含中文、*English*、平仮名（ひらがな）、片仮名（カタカナ）、<span style="font-family: 'Times New Roman'; font-style: italic;">ру́сский язы́к</span>、עִבְרִית‬ 等多种文字，来自政界、学界、军界、文化界、艺术界等领域的各类人士，长达数行甚至数个段落的观点、论辩、评价等内容。
> <footer>及其<a href="#">来源</a></footer>

另一段普通的正文  
正文的第二行  
和第三行
```

一段普通的正文

> 常见的  
> **多行**  
> 引用文本
>
> 以及可能包含中文、*English*、平仮名（ひらがな）、片仮名（カタカナ）、<span style="font-family: 'Times New Roman'; font-style: italic;">ру́сский язы́к</span>、עִבְרִית‬ 等多种文字，来自政界、学界、军界、文化界、艺术界等领域的各类人士，长达数行甚至数个段落的观点、论辩、评价等内容。
> <footer>及其<a href="#">来源</a></footer>

另一段普通的正文  
正文的第二行  
和第三行

<figure class="quote">
  <blockquote>
    But web browsers aren’t like web servers. If your back-end code is getting so big that it’s starting to run noticeably slowly, you can throw more computing power at it by scaling up your server. That’s not an option on the front-end where you don’t really have one run-time environment—your end users have their own run-time environment with its own constraints around computing power and network connectivity.
  </blockquote>
  <figcaption>
    <!-- &mdash; Jeremy Keith, <cite>Mental models</cite> -->
    Jeremy Keith, <cite>Mental models</cite>
  </figcaption>
</figure>

## 菜单

```html
<span class="menutext">Help</span>
```

<span class="menutext">Help</span>

## 按钮

```html
<button class="btn green mini">Button</button>
<button class="btn blue mini">Button</button>
<button class="btn red mini">Button</button>
<button class="btn purple mini">Button</button>
<button class="btn cyan mini">Button</button>
<button class="btn yellow mini">Button</button>
<button class="btn gray mini">Button</button>
```

<button class="btn green mini">Button</button>
<button class="btn blue mini">Button</button>
<button class="btn red mini">Button</button>
<button class="btn purple mini">Button</button>
<button class="btn cyan mini">Button</button>
<button class="btn yellow mini">Button</button>
<button class="btn gray mini">Button</button>
