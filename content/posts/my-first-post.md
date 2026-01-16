---
date: '2026-01-07T15:45:12+09:00'
draft: false
title: '👋Hello World!｜hugo papermod主题搭建+装修01'
lastmod: '2026-01-16T00:00:00+09:00'
tags: 
  - blog装修
  - 码农笔记
---
## 0前言

记录下代码0基础的blog搭建步骤，和（成功/想要）实现的功能。

{{< collapse title="碎碎念（点击展开）" >}}
1.零基础搭自己的blog网站很难。经常为了实现一个功能搜很多文章+AI老师反复修改。一个晚上能改好一个功能很不容易，当然也很棒。

2.为什么要建自己的blog有好几个原因。第一，觉得有自己的博客很酷；第二，看了[椒盐豆豉老师的文章](https://blog.douchi.space/2023-why-you-need-a-blog/#gsc.tab=0)，总结回顾和塑造自己；第三，工作是转码，提前用自己感兴趣的方式接触下代码；第四，想要在一个不受审查和算法的地方生长……

3.第一篇文章大概花了一周时间来写，进度缓慢让我一度怀疑自己是不是又是3分钟热度。最近准备把博客的重点从装修转到多发点文章。
{{< /collapse >}}

## 1步骤
### 1.1准备工作
  平台：MAC

  使用软件：terminal

  基础环境搭建：

  1.准备基础工具： 打开terminal，运行 `xcode-select --install`

  2.安装管家 Homebrew： 标准包管理器，有了它，安装任何软件只是一行命令的事。
  `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" `
  完成后务必按照终端提示执行那两行 echo 命令配置环境变量。

  3.安装核心组件：
  `bash brew install git hugo`

  *第一个软件git（版本控制工具）: 虽然 Xcode 带了一个 Git，但通过 Homebrew 安装的版本更新、更标准。第二个软件hugo（博客生成器）: Homebrew 默认安装的通常是Extended版。推荐Extended版本，因为现在主流hugo主题大多依赖Sass/SCSS 处理样式，只有 Extended 版才支持。*

  4.装编辑器： 下载并安装VSCode，并在其 Command Palette 中安装 code 命令。
  具体步骤打开VSCode，点击view -> Command Palette...，输入 Shell Command: Install 'code' command in PATH 并回车。

### 1.2创建网站
  参考了[Hugo官方指南](https://gohugo.io/getting-started/quick-start/)和[papermod主题的安装指南](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/)，基本看这两个文档就没问题了。使用的theme是：[papermod](https://themes.gohugo.io/themes/hugo-papermod/)。可以在hugo官网的主题中挑选自己喜欢的，每个主题的配置，稍微有些不同，请参考相关主题的教程。

  Step1 检查Hugo版本，需大于等于Hugo v0.146.0 `hugo version`

  Step2 安装主题

  1.进入想要存放blog根目录的文件，比如我放在了桌面`cd ~/Desktop`。运行下述命令创建本地网站
  ```
  hugo new site demo --format yaml #将demo换成自己的网站名字，将默认的toml文件转换成yaml，据说yaml更容易读
  cd demo
  git init #初始化一个空的git仓库
  git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod #克隆主题到theme目录
  ```
  *更推荐用submodule的方法而不是clone，具体原因是，submodule是“订阅制”，clone是“买断制”。使用clone当作者后续修复bug或新增功能时，很难把更新拉取回来。*

  2.在网站配置文件中，hugo.yaml添加
  `theme: ["PaperMod"]`

### 1.3个性化主题
  首先我们的根目录包含以下文件,让gemini老师跑了个简单易懂的解释。
  ```
    .
    ├── archetypes 文章的新建模版，
    ├── assets 私人定制的软装材料。自己写的css脚本等，会覆盖主题默认样式
    ├── content 房子的家具和物品。写的所有md文章
    ├── data 储藏室的数据单。一般不会用到
    ├── hugo.yaml 房子的总控开关。
    ├── i18n 多语言翻译官。存放不同语言的菜单名
    ├── layouts 改动房屋结构图
    ├── static 直接搬进屋的重物。放图片，pdf等
    └── themes 房子的装修样板间。
  ```
  在terminal运行 `hugo server`，打开local的网址可以看到是空白的，接下来我们进行功能的设置。

  一个省事儿的方法，直接参考同样主题的yaml文件，复制黏贴，我的参考是[sulv](https://github.com/xyming108/sulv-hugo-papermod)。
  
  运行hugo server可以发现已经有了基础的架子了，下面是我自己想要的功能的具体操作和代码。可以一边修改代码，一边看local网页做出来的样子。

#### 1.3.1修改post模版
  archetype只在一件事上生效：执行 hugo new ... 创建文件的那一刻。在archetypes里，default.md 是Hugo的兜底模板。所以我们需要新建post.md来存放post的模版。
  ```
    mkdir -p archetypes        # 进入目标目录，-p的意思是不存在就一起创建
    touch archetypes/posts.md  # 创建文件
    code archetypes/posts.md   # 用VS Code打开
  ```
  然后在post.md里加入下面的代码
  ```
  ---
  title: '{{ replace .File.ContentBaseName "-" " " | title }}'
  date: {{ .Date }}
  lastmod:  {{ .Date }}
  author: ""
  description: ""
  tags: [] #标签

  draft: false
  showToc: true # 显示目录
  TocOpen: true # 自动展开目录
  hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
  comments: true #本页面是否显示评论
  ---
  ```
#### 1.3.2添加友链
 利用shortcode功能。在layouts/shortcodes新建并打开links.html，links.html负责定义单张卡片的html结构。放入内容。

 在assets/css/extended里新建links.css。css文件定义效果，放入代码。

 创建完成后在content/links.md加入内容

 具体代码请参考：[sulv](https://github.com/xyming108/sulv-hugo-papermod)。
  
#### 1.3.3 链接在新界面跳转并且外部链接后面会显示图标
  通过css代码可以非常简陋的实现这个功能。在assets里新建css/extended/custom.css，然后添加：
  ```
    .post-content a[href^="http"]:not([href*="localhost"]):not([href*="bnhnp.netlify.com"])::after {
    content: " ↗";
    font-size: 0.8em;
    vertical-align: super;
    opacity: 0.6;
    margin-left: 2px;
    }
  ```
  content是后面会显示的内容

## 2上线
  选择部署平台就像是选“物业管理”。最开始打算选GitHub Pages，但找了很多攻略看起来比较麻烦，为了自动化选择了Netlify。

  STEP1 上传到GitHub。

  在github新建repository，给个名字，选择public其他不要动，点create后会生成.git的链接。复制这个链接

  然后打开mac终端，进入博客文件夹，初始化Git仓库并检查.gitignore 文件。这一步是防止public文件夹或者系统垃圾文件上传。输入`nano .gitignore`。查看是否有以下内容，如果没有复制黏贴进去然后Ctrl+O 保存，Ctrl+X 退出
  ```
    public
    resources
    .DS_Store
    .hugo_build.lock
  ```

  下一步提交代码
  ```
  git add .
  git commit -m "初次提交博客代码"
  ```
  最后推送到GitHub，这一步准备好最开始复制的链接进行替换。
  ```
  git branch -M main
  git remote add origin https://github.com/你的用户名/my-blog.git
  git push -u origin main
  ```
  如果是第一次用 GitHub，它可能会弹出一个窗口让你输入账号密码。照做即可。注意密码是token，不是账号密码。
  
  STEP2部署到Netlify

  登录[Netlify](https://www.netlify.com/)，点击 "Add new site" -> "Import an existing project"。授权并选择 GitHub。在搜索框里选择刚才创建的仓库名。
  
  然后构建设置，Netlify 通常能自动识别 Hugo，但最好检查下面这几项，Branch: main，Build command: hugo --gc --minify，Publish directory: public
  
  最后设置环境变量。点击 "Add environment variables"。Key: HUGO_VERSION。Value: 0.154.2（填入自己的版本号）

  注：记得在hugo.yaml修改baseURL，用Netlify分配的网站替换。然后进行推送三部曲，
  ```
    git add .
    git commit -m "Fix: update baseURL to netlify address"
    git push
  ```
  m后面的内容是提交说明。

## 3后续
  还有很多想装修的地方，以后写别的post继续。 