+++
lastmod = "2022-12-11 22:58:24"
categories = ["Tool"]
draft = false
toc = true
+++

## Anki-BookxNote {#anki-bookxnote}


### Anki {#anki}

[ANKI-可以用一辈子的记忆学习工具](https://www.jianshu.com/p/8007014afb07)

```panitext

```

Sub2srs（影片切割导出截图和音频和台词）
英语单词制卡工具 6.0.xlsx（单词放进去可以导出释义例句等）
Anki 单词划词助手（chrome 插件）
Pdf.js（让 chrome 打开 pdf 也可以使用划词助手）
Image Occlusion（遮挡图片来填空）
\#+end_src


### plugin {#plugin}


#### Cardistry: Dynamically Adjust New Cards (recommend) {#cardistry-dynamically-adjust-new-cards--recommend}

-   Anki 动态调整新卡片数量
-   这个插件思路很简单，为 learning 卡片和 young 卡片数量之和设置个阈值，也即图中的 Lrn/Yng.
    -   如果数量超过这个阈值那么你今天新学习卡片的数量为零，而如果没超过这个阈值，新学习卡片数量等于阈值减去 learning 和 young 数量，当然最大不能超过牌组限制。

[Cardistry 2: Dynamically Adjust New Cards](https://ankiweb.net/shared/info/1535078906)


#### Customize Keyboard Shortcuts (recommend) {#customize-keyboard-shortcuts--recommend}

自定义快捷键实现通过 h,j,k,l 选择卡片

通过 ctrl+shift+a 快捷键，进入附加组件管理窗口,找到 Customize Keyboard Shortcuts 插件项，然后点击设置
[Customize Keyboard Shortcuts](https://ankiweb.net/shared/info/24411424)
install code: 24411424

"reviewer choice 1": "1",
"reviewer choice 2": "2",
"reviewer choice 3": "3",
"reviewer choice 4": "4",


#### Refocus Card when Reviewing (2.1) (optional) {#refocus-card-when-reviewing--2-dot-1----optional}

anki 中切换一张卡片后，当前窗口会失区焦点（好像是）, this 插件，可以实现卡片页面聚焦。


#### Advanced Review Bottom Bar (optional) {#advanced-review-bottom-bar--optional}

Anki review 界面增强, integrate  Large and Colorful Buttons()回答按钮增强 &amp; Extended Card Stats During Review(卡片信息统计).


#### Color Confirmation (recommend) {#color-confirmation--recommend}

回答反馈:每按下一个按钮时提供反馈，如果按错了及时改正即可。
(手指无意识自发选择，有时候难免会选错，而 Anki 本身并没有提供一个选择反馈，有时候我们选错了选项自己并没有意识到，这样对 Anki 主动召回法产生干扰，影响学习效果)

[Color Confirmation](https://ankiweb.net/shared/info/1084228676)  install code:1084228676


#### Speed Focus Mode (recommend) {#speed-focus-mode--recommend}

resolve 在学习内容较丰富的卡片的时候，可能很难保持绝对的专注，不经意间会花费比较多的时间。
[Speed Focus Mode](https://ankiweb.net/shared/info/1046608507) install code:1046608507


#### browser pugin - 在线词典助手(Anki 划词制卡助手) {#browser-pugin-在线词典助手--anki-划词制卡助手}


#### WordQuery - 批量导入单词 {#wordquery-批量导入单词}


#### AnkiConnect -&gt; quicker(recommand) {#ankiconnect-quicker--recommand}

[AnkiConnect](https://ankiweb.net/shared/info/2055492159) install code:2055492159


#### GODMODE faster shortcuts and cloze switching(recommand) {#godmode-faster-shortcuts-and-cloze-switching--recommand}

插件 ID：1508677152

这个插件中，挖空的快捷键被改成了 Win：Ctrl + E 和 Ctrl + S，Mac：Cmd + E 和 Cmd + S。

它解决了 Anki 的一个缺点：需要手动切换卡片类型。


#### Image Occlusion Enhanced for Anki 21 alpha {#image-occlusion-enhanced-for-anki-21-alpha}

插件码：1374772155

这个插件允许你在图片上挖空


#### Cloze Hide All(recommand) {#cloze-hide-all--recommand}

插件码：1709973686

这个插件是 Cloze 功能的增强。它会在你回答问题的时候把你挖的其他的空也给遮住。

使用方法和 Cloze 差不多，但是要选中 Cloze Hide All 的模板。


#### Mini Format Pack（recommand） {#mini-format-pack-recommand}

插件 ID：295889520

Anki 不支持排版？没关系，我们可以使用这个插件。它包含了背景高亮、数字列表、居中等诸多功能。


### **quicker** {#quicker}

[终极快速制卡](https://getquicker.net/Sharedaction?code=cf4ed7d7-403a-49fb-2610-08d7d1530b70&fromMyShare=true)


## browser search {#browser-search}


### google/bing {#google-bing}


#### general {#general}

谷歌会自动拆分空格前后的内容


#### link {#link}

<https://zhuanlan.zhihu.com/p/58124215>(谷歌搜索操作符大全（42 个高级操作符）)
<https://baijiahao.baidu.com/s?id=1610278932506239136&wfr=spider&for=pc> (精选 12 个最实用的 GOOGLE 搜索技巧)

Google 使用的通配符属于“全词通配符”,指代替一个单词,  \*（星号）

intitle:、site:等搜索语法中使用，如：

-   intitle:"the\*of new york"
-   site:us "\* \* search engine \* \*"
-   filetype:pdf


#### basic {#basic}

<https://blog.csdn.net/valecalida/article/details/94406924>

```cfg
+  ：强制包含在加号后面的内容
-  ：强制减去内容包含减号后面的内容
     *+-号前面有空格，+-号后面无空格，不然无效！*
.    : 取代一个字符
(*)  ：替代后面的所有内容,单独的星号
“”   ：表示强调(完全匹配)，一定程度上可以起到过滤作用

OR   : 返回的结果是包含 OR 两边的任意关键词
AND  : 返回的结果是包含 AND 两边的关键词
     *注意：OR, AND 必须是大写*
```


#### inurl {#inurl}

[inurl]+[:]+[关键字 1]+[空格]+[关键字 2]

inurl:amazon ppc   表示搜索 url 中含有"amazon"和"ppc"的网页


#### intitle {#intitle}

[intitle]+[:]+[关键字 1]+[空格]+[关键字 2]

在一个或几个关键词前加"intitle:"，可以限制只搜索网页标题中含有这些关键词的网页。title 是目前页面优化的最重要因素。

intitle:amazon ebay 表示搜索标题中含有关键词"amazon"和"ebay"的网页。 　


#### allintitle {#allintitle}

allintitle：搜索返回的是页面标题中包含多组关键词的文件。

allintitle:amazon ebay wish  就相当于: intitle:amazon intitle:ebay intitle:wish


#### intext {#intext}

intext: 指返回的页面正文中包含关键词的页面。


#### allintext {#allintext}

allintext：搜索返回的是页面正文中包含多组关键词的页面。

allintext:amazon ebay wish  就相当于：intext:amazon intext:ebay intext:wish


#### filetype {#filetype}

[关键字 1]+ [空格]+[filetype]+[:]+[文件类型标识]

SEO filetype:pdf 返回的就是包含 SEO 这个关键词的所有 PDF 文件。


#### site {#site}

[关键字]+[空格]+[site]+[:]+[网站名称或国别]

site 后的冒号":"可以是半角":"也可以是全角"："，

"site:"后不能有"<http://"前缀或"/%22%E5%90%8E%E7%BC%80>

site:bbs.ichuanglan.com 搜索 子域名 bbs.ichuanglan.com 的所有文件


#### related {#related}

查询与某个网站相关联或者相类似的页面

related:amazon.com，就得出了 Rakuten 等电商平台


#### index of {#index-of}

“index of”这个关键词可以直接进入网站首页下的所有文件和文件夹中， 不必通过 HTTP 的网页形式，从而避免了不少网站的限制，做到了突破限制 下载。

-   例如在搜索框上输入：“index of/”ppt，然后搜索，你就可以突破 网站入口下载 Powerpoint 作品；
-   在搜索框上输入：“index of/”mp3，然 后搜索，你就可以突破网站入口下载 mp3、rm 等影视作品；
-   在搜索框上输入：“index of/”﻿swf，然后搜索，你就可以突破网站入口下载 flash 作品。


#### 目录检索 {#目录检索}

如果你不想搜索广泛的网页，而是想寻找某些专题网站，可以访问 Google 的分类目录<http://directory.google.com/%E3%80%82%E5%88%86%E7%B1%BB%E7%9A%84%E7%BD%91%E7%AB%99%E7%9B%AE%E5%BD%95%E4%B8%80%E8%88%AC%E7%94%B1%E4%B8%93%E4%BA%BA%E8%B4%9F> 责，分类明确，信息集中。因此读者应该养成这样的习惯：首先考虑所需要的信息能否在一个专门主题的网站上找到。不过需要说明的是，用目录检索，往往需要用户对查询的领域很熟悉。


### SearchWebsite {#searchwebsite}

-   chognbuluo
-   <http://hao.199it.com/>  大数据导航


## baidu search {#baidu-search}

右上角的【设置】-【隐藏资讯】；在未登录状态下，点击【设置】-【关闭热榜】,【关闭资讯】

extensions：

-   Adblock Plus
-   AdGuard
-   Tapermonkey
    -   「AC-baidu」

quickSearch

-   筛选范围
-   布尔运
    -   与 eg.「水果 香蕉」（水果、空格、香蕉），则搜索结果中一般都会包含这两个关键词
    -   非 eg.「水果 -香蕉」（水果、空格、减号、香蕉），则可以获得包含「水果」但不包含「香蕉」关键词的的结果
    -   或 eg.「水果|香蕉|梨|李子」，搜索结果中至少会包含这些关键词当中的一个。
-   「水果香蕉」不属于布尔运算。不加空格的内容大多情况下会被默认为一个关键词,英文输入法状态下的半角「,」「&amp;」「+」等等符号一般都可以达到同样的效果.

-   **不推荐使用这些特殊符号,最好的方式是直接使用「高级搜索」功能。**
-   **在百度首页点击右上角的「设置」-「高级搜索」，这里的「搜索结果」选项中，除了「非」、「与」、「或」，还包括了「包含完整关键词」选项。**
    -   在「包含全部关键词」当中输入「苹果香蕉」，得到的结果中这两个词可能是拆分开的；
    -   在「包含完整关键词」中输入，得到的结果一般来说，是在一起的。
    -   百度首页点击右上角的「设置」-「搜索设置」;选择「全部语言」、「简体中文」和「繁体中文」,在搜索结果中，你也能打开「搜索工具」，通过具体的时间、格式和站点范围来进行搜索。
    -   谷歌搜索中，这一选项在右下角的「设置」-「高级搜索」中.
    -   filetype:pdf  xxxx
    -


## Capslock {#capslock}

```cfg
Capslock+ E / D / S / F（上 / 下 / 左 / 右）
Capslock+ I / K / J / L（上 / 下 / 左 / 右选中文字）
Capslock+ w / r（向左 / 右删除文字）
Capslock+ A / G（光标向左 / 右跳一个单词，对英文、代码特别有用）
Capslock+ ; / P（移动光标至行首 / 行末）
Capslock+ U / O（选中光标至行首 / 行末文字）
Capslock+ Backspace（删除光标所在行所有文字）
Capslock+ Enter（无论光标是否在行末都能新起一个换行而不截断原句子）

Qbar
Capslock+Q
bd xxx
gg xxx
tb xxx
wk xxx

独立剪贴板
Capslock+X / C / V 和 Capslock+LAlt+X / C / V 是两套独立的剪贴板，利用它们可以方便地交换文字，或者临时把一段文字保存起来重复使用，而又不影响正常复制粘贴。

Capslock + F1 打开文档页
Capslock + F2 计算器
Capslock + F3 调用了有道翻译的 api，实现了翻译功能：
Capslock + F4 可以让窗口半透明
Capslock + F6 可以让某窗口保持置顶

Capslock + Tab 补全记录
qm -> qqmial

Capslock + Win + 0~9 绑定窗口
```


## DownloadMnager {#downloadmnager}

-   IDM
-   NDM similar with IDM  sppourt extention
-   FDM download BT/Link  sppourt extention


## extensions {#extensions}


### google {#google}


### firefox {#firefox}

```cfg
All-in-One Sidebar：书签等侧边栏显示。
AutoPager： 自动载入网站的下一页。
FireGestures： 鼠标手势。
ScrapBook： 离线文章保存管理系统。
Tab Mix Plus：标签功能增强。
Quick Search Bar：搜索功能增强。
Download Statusbar
Better Gmail 2 + Better GCal:由 Lifehacker 推出两款针对 Gmail 和 Google Calendar 的优化插件。
Delicious Bookmarks
MeeTimer: 跟踪你的网页浏览量，从而帮助你更好的管理和利益时间
```


## fzf {#fzf}

<https://www.jianshu.com/p/b48131e4ad06>

```sh
# {} is replaced to the single-quoted string of the focused line
fzf --preview 'cat {}' # 预览文件内容
fzf --preview 'rg -F "def main(" -C 3 {}' # 预览 Python 文件 main 函数前后 3 行代码
```


## Git {#git}


### git-basic {#git-basic}

```sh
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

git clone /path/to/repository				#创建一个本地仓库的克隆版本
git clone username@host:/path/to/repository	                #conle 远端服务器上的仓库

git add .
git add --all

git remote add origin git@gitee.com:liaoxuefeng/learngit.git	#关联远程库
git remote -v
git remote rm origin

# ${工作流程}
working dir(工作目录)--add--> Index(缓存区)--commit--> HEAD(最 ithub.com/CosmosHua/locate.git new
git clone git://github.com/CosmosHua/locate new
git clone git://github.com/CosmosHua/locate.git new

# 2）常用协议
git clone git@github.com:fsliurujie/test.git         --SSHkod 协议 kpd
git clone git://github.com/fsliurujie/test.git          --GIT 协议
git clone https://github.com/fsliurujie/test.git      --HTTPS 协议
```


### git-remote {#git-remote}

```sh
同步本地仓库和 github/gitee，就需要用到 SSH Key，github 拿到了你的公钥就会知道内容是你推送的。
$ ssh-keygen -t rsa -C "注册邮箱" # 生成 id_rsa id_rsa.pub
$ start ~/.ssh/id_rsa.pub  # 打开.ssh 下的 id_rsa.pub 文件
  打开"SSH Keys"页面 https://github.com/settings/ssh ，setting--Add SSH key。

git remote add origin git@gitee.com:liaoxuefeng/learngit.git	#关联远程库
git remote -v

$ git push <远程主机名> <本地分支名>:<远程分支名>
git push -u
git push -u origin master
```


### git-ngr {#git-ngr}

```sh
make VERBOSE=1 V=1 调用 gcc 的命令行
cmake --version

git --version
git describe
git describe --tag
git show
git status
git branch
git diff HEAD^

apt-cache search linux-headers

cd ngr.git;
git checkout master
git show, 确认 j 当前是在 jmaster 分支上

ngr.git 目录下，执行 git reset --hard HEAD
git reset --hard HEAD^看到全部代码
```


### gitFileChange {#gitfilechange}

```sh
git log filename   查看某个文件的 commit 记录
git log -p filename     查看文件每次提交的 diff
git log --pretty=oneline filename 列出文件的所有改动历史
git show 提交生成的一次哈希值 filename   ${只查看某次提交的文件变化}
```


### gitquestion {#gitquestion}


#### warning {#warning}

```sh
# 1)warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.

---> 1
rm -rf .git  // 删除.git
git config --global core.autocrlf false  //禁用自动转换
git init
git add 文件名/.

for dir in $(ls);
do
  cd $dir;
  rm .git -rf;
  git config --global core.autocrlf false;
  git init;
  git add *;
  git commit -m "vimplugin";
  cd -;
done

```


#### show Chinese {#show-chinese}

```sh
# 2) git show Chineses

1 # window
Options−>Text−>local(本地): zh_CN
Options−>Text−>Charector set(字符集): UTF-8

2 # bash
git config --global i18n.commitencoding utf-8  --注释：该命令表示提交命令的时候使用 utf-8 编码集提交
git config --global i18n.logoutputencoding utf-8 --注释：该命令表示日志输出时使用 utf-8 编码集显示
export LESSCHARSET=utf-8  --注释：设置 LESS 字符集为 utf-8

```


#### ping github {#ping-github}

```sh
cat C:\Windows\System32\drivers\etc\hosts<< EOF
192.30.253.113    github.com
192.30.252.131 github.com
185.31.16.185 github.global.ssl.fastly.net
74.125.237.1 dl-ssl.google.com
173.194.127.200 groups.google.com
192.30.252.131 github.com
185.31.16.185 github.global.ssl.fastly.net
74.125.128.95 ajax.googleapis.com
EOF
```


## github-accelerate {#github-accelerate}


### google browser plugin {#google-browser-plugin}

github 加速


### HOSTS {#hosts}

```sh

# 第一步：获取 github 的 global.ssl.fastly 地址访问：
http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo 获取 cdn 和 ip 域名：
得到：199.232.69.194 https://github.global.ssl.fastly.net

# 第二步：获取 github.com 地址 访问：
https://github.com.ipaddress.com/#ipinfo 获取 cdn 和 ip：得到：140.82.114.4 http://github.com

# 第三步：修改 host 文件映射上面查找到的 IP
windows 系统：
C:\Windows\System32\drivers\etc\hosts
指定可写入：右击->hosts->属性->安全->编辑->点击 Upsers->在 Users 的权限“写入”后面打勾

# 末尾处添加以下内容：
199.232.69.194 github.global.ssl.fastly.net
140.82.114.4 github.com
```


### gitee.com/.../GitHub520 | SwitchHosts {#gitee-dot-com-dot-dot-dot-github520-switchhosts}

```cfg
Windows： 在 CMD 窗口输入：ipconfig /flushdns
Linux 命令：sudo rcnscd restart
Mac 命令：sudo killall -HUP mDNSResponder
```


## imgur {#imgur}


### ali OSS（Object Storage Service，OSS） {#ali-oss-object-storage-service-oss}

2015 年之后不免费.


### tencent (Cloud Object Service, COS) {#tencent--cloud-object-service-cos}

腾讯云 COS 存储的文件在 50GB 以下和 每月的下载流量小于 50GB 是免费的


### qiniu {#qiniu}

七牛云存储则提供永久的免费额度：10GB 存储空间、每月 10GB 下载流量、每月 10 万次 Put 请求、每月 100 万次 Get 请求。

七牛的镜像 CDN 加速支持一键切换 CDN，非常适合图片多的网站使用。目前七牛云存储已经有了 Wordpress、Ghost、Typecho、Discuz 等流行的应用插件，同时还有 SDK 应用开发包和 Linux、Windows 的 qrsbox 上传工具。


## Joplin {#joplin}


### theme {#theme}

<https://lightzhan.xyz/index.php/2020/02/29/joplinintroduction/>


#### plugin {#plugin}

[Joplin插件使用方法详解](https://lightzhan.xyz/index.php/2020/03/26/the-reason-of-low-download-speed-and-solutions/)


## Keepass {#keepass}


### URL {#url}

<https://zhuanlan.zhihu.com/p/39645975>


### client {#client}

Windows 下就有三款客户端：官方客户端、KeeWeb、KeePassXC，

安卓方面有 KeePassDroid 和 Keepass2Android，

苹果方面 keepass touch 和 Mini KeePass 都是不错的选择

linux 平台也可以使用：官方客户端、KeeWeb、KeePassXC，

就连 Windows phone 也有 WinKee。


### 自动输入 {#自动输入}

<https://zhuanlan.zhihu.com/p/36057692>
在工具-选项-高级-自动输入中，勾选以下几项，将会大大提高自动登录的可匹配度

标记可以在帐号记录中右键然后点击“编辑/查看记录”-“属性”-“标记”中添加，所有的标记用英文的逗号隔开


### 1、安全的密码自动填入功能 Auto-Type: {#1-安全的密码自动填入功能-auto-type}

此功能允许用户定义一个快捷键（默认的是 Ctrl+Alt+A），当按此快捷键时，Keepass 会在选定的任何窗口中自动填入相应的密码记录。

在密码记录的备注栏，以‘Auto-Type:’开头的一行代表了自动登录的语法结构。KeePass 使用预先定义的语法结构来实现自动登录，要实现这个功能只要注意两点：

a)密码记录的“备注”中写上代码：Auto-Type: {USERNAME}{TAB}{PASSWORD}{ENTER}

b)密码记录的“标题”最好能正确填写：Auto-Type-Window: ABC

Keepass 需要从密码记录的“备注”中读取代码：

来正确的选择相应窗口的密码记录。命令中的“ABC”表示待填密码的窗口上标题栏中显示的名称（Title）。如，北美中文博客网站的 Title 为“北美中文博客”，和讯博客网站的 Title 为“和讯个人门户”。这些 Title 都会在浏览器的标题栏上显示出来。

**如果密码记录的“备注”中没有给出代码“Auto-Type-Window: ABC”，那么 Keepass 会默认已写入如下代码： Auto-Type-Window: \*{TITLE}** 其中"\*"是通配符，"{TITLE}"是你在密码记录的“标题”栏中填入的内容。

因此，对于北美中文网站而言，只要在密码记录的“标题”栏中填入“北美中文博客”（即网站的 Title 的一部分内容），Keepass 就能识别出来，并自动填入记录中的用户名和密码了。

也可以根据具体情况来修改以达到不同环境下的自动登录。 例如：Auto-Type: {USERNAME}{TAB}{PASSWORD}{TAB}{TAB}{TAB}{ENTER}

\*技巧：这个例子中多了两个 TAB 键，用于登录某些论坛。在设置时，读者可以先把光标置于密码栏，然后按 TAB 键，直到光标跳到确定按钮，这时按了几次 TAB 键，自动登录语法就设几个{TAB}。


### 2、自动登录目标窗口设置 Auto-Type-Window: {#2-自动登录目标窗口设置-auto-type-window}

备注栏中以‘Auto-Type-Window: ’开头的一行代表了自动登录的目标窗口。 例如：Auto-Type-Window: Total Commander\*，就是自动登录 TC 论坛的窗口设置：Total Commander\*是 TC 论坛网页的标题，‘\*’是通配符。

上面的例子合起来粘贴到备注栏就是这样：Auto-Type: {USERNAME}{TAB}{PASSWORD}{TAB}{ENTER}，Auto-Type-Window: Total Commander\*，登录时，把光标定位到用户名框内，按快捷键，就 OK 了。（当然，有些论坛的登录需要验证码，先要手工输入验证码，然后按登录快捷键）。


### 自动输入和双通道自动输入混淆 {#自动输入和双通道自动输入混淆}

自动输入全局热键默认为【Ctrl + Shift + A】。

使用方法非常简单：点击输入框→按下自动输入全局热键；

或点击输入框→切换到 keepass 主界面→右键单击记录→【执行自动输入】

自动输入的键入规则，默认规则为{USERNAME}{TAB}{PASSWORD}{ENTER}。解释：输入用户名，Tab 键（换行），输入密码，回车键。但这套规则明显不适合中文用户，因为使用自动输入时输入法必须是英文.

推荐使用以下规则：+{DELAY 100}{CLEARFIELD}{USERNAME}{TAB}{PASSWORD}{ENTER}。解释：Shift 键（Windows10 输入法切换），等待 100 毫秒，清空输入框，输入用户名，Tab 键（换行），输入密码，回车键。

**使用此规则自动输入时请确保输入法为中文**


## kindle {#kindle}


### 个人文档设置 {#个人文档设置}

Kindle 个人文档服务可以让您轻松地随身携带个人文档，不再需要打印。您和您认可的发件人可以将文档发送到您的〖发送至 Kindle〗电子邮箱，该文档即可自动传送到您的 Kindle。（注：Kindle 个人文档服务支持 Kindle Android, Kindle iPhone, Kindle iPad 阅读软件。）


### 〖发送至 Kindle〗电子邮箱 {#发送至-kindle-电子邮箱}

```markdown
| name                          | email                      |
|-------------------------------|----------------------------|
| 近海 888                      | wenhua_s_huawei@kindle.cn  |
| 远山近海的 Fire               | wenhua_s_fire@kindle.cn    |
| 近海 888's 2nd Android Device | wenhua_s_xiaomi@kindle.cn  |
| 近海 888's 3rd Android Device | wenhua_s_oneplus@kindle.cn |
| 近海 888's Android Device     | wenhua_s_C73dmu@kindle.cn  |
```


### kindle for pc {#kindle-for-pc}

1.19 安装 pc 可用（关闭自动更新），之上版本安装后无法连接。


## Makror {#makror}

一款带 todo、优先级和标记的 markdown app
(orgzly)


## Motrix {#motrix}

open source
支持下载 HTTP、FTP、BT、磁力链等资源。

-   download baiduyun
    -   [broswer plugin](e:/Refine/Daoyi/CRX/BaiduExporter/)


## Markdown {#markdown}


### 链接 {#链接}

```cfg
[]()  表示超链接，中括号表示链接文字，小括号表示链接地址
![]() 表示图片。其中中括号表示图片未加载时的提示文字，小括号表示图片地址。

# （行内式链接）
[百度][https://www.baidu.com/]

# （参考式链接）
[CSDN][CSDN 网址]
[CSDN 网址]:https://www.csdn.net/

# （自动链接）
<https://github.com/>
```


### 代码块 {#代码块}

````markdown
`单行代码` ，可行内使用
-----
```
多行代码
多行代码
```
````


### 表格 {#表格}

使用一根竖线来分隔各个单元格，使用冒号来决定单元格的对齐方向。

````markdown
| 序号 | 姓名 |
|:-----|:-----|
|:-----|:-----|
|:-----|:-----|
| 1    | 小明 |
| 2    | 小红 |
````


### 水平分割线 {#水平分割线}

使用 --- 或 **\*** 或 <span class="underline">_</span> 来表示分割线，（注意：行内不能有其他东西）


### 脚注 {#脚注}

Typora[^1]

[^1]A markdown editor


### other {#other}

gitbook 就可以教你把一个个 Markdown 文件组织起来，弄成一本电子书。


## markdown-typora {#markdown-typora}

<https://mp.weixin.qq.com/s/9D7Ct7MTBbXvlHEBachtow>


#### plugins {#plugins}

<https://github.com/Thobian/typora-plugins-win-img>


#### qiniu {#qiniu}

````js
//“密钥管理”页面地址：https://portal.qiniu.com/user/key
$.image.init({
    target:'qiniu',
    qiniu: {
        UploadDomain: 'https://xxx.com', // 上传地址，需要根据你存储空间所在位置选择对应“客户端上传”地址 详细说明：https://developer.qiniu.com/kodo/manual/1671/region-endpoint
        AccessDomain: 'http://xxx.com/', // 上传后默认只会返回相对访问路径，需要设置好存储空间的访问地址。进入“文件管理”下面可以看到个“外链域名”就是你的地址了，复制过来替换掉 xxx 就可以了。
        AccessKey : 'xxxx', // AK 通过“密钥管理”页面可以获取到
        SecretKey: 'xxxx', // SK 通过“密钥管理”页面可以获取到
        Folder: 'typora', // 可以把上传的图片都放到这个指定的文件夹下

        policyText: {
            scope: "xxx", // 对象存储->空间名称，访问控制记得设置成公开
            deadline: 225093916800, // 写死了：9102-12-12 日，动态的好像偶尔会签名要不过
        },
    }
});
````


## OneNote {#onenote}


### Gem for onenote {#gem-for-onenote}

语法支持：标题、引用、列表、图片、链接、分隔线、代码块、待办清单、文本样式（粗体、斜体、行内代码）等


### One Markdown 独立客户端链接 OneNote {#one-markdown-独立客户端链接-onenote}

表格、流程图、目录、代码高亮、数学公式、LaTeX 等语法


### NoteHighlight {#notehighlight}

OneNote 代码高亮插件，免费开源项目，支持 2010 版本，2013 为 Beta 版，2016 为网友改进版。

[2016 版 – GitHub](https://github.com/elvirbrk/NoteHighlight2016/releases)

-   该插件需要 .NET3.5 环境支持


### share notes or pages {#share-notes-or-pages}

1.  onenote2016 文件-共享  邮件 or 链接 share 笔记
2.  onenote2016 开始-通过电子邮件发送页面
3.  onenote2016 文件-导出（.onenote; .pdf etc.）
4.  onenote for windows10 右上角 共享邮件 or 右下角发送副本（\*page\*）


## pandoc {#pandoc}


### basic {#basic}

````sh
# 读取文件
pandoc -f 输入格式 -t 输出格式 -o 输出文件名 输入文件
# 读取网页
pandoc -f html -t 输出格式 -o 输出文件名 --request-header User-Agent:"Mozilla/5.0" \
  https://www.fsf.org

pandoc --list-input-formats
pandoc --list-output-formats
````


### docx {#docx}

````cfg
--toc # 生成目录
--toc-depth=NUMBER # 生成的目录深度
--wrap=auto|none|preserve # 文字换行方式
--reference-doc=FILE # 指定模板

默认的 word 模板可以通过命令来查看
pandoc --print-default-data-file reference.docx > custom-reference.docx

Mac 的用户需要注意，使用 Pages 对模板文件进行修改会导致模板失效，需要使用 Office 进行编辑，并使用兼容模式进行保存。
https://blog.csdn.net/fenghuizhidao/article/details/107202497
````


### metadata {#metadata}

metadata 是导出格式中的一些信息，例如作者、日期、简介等等，在 EPUB、PDF、Word 等格式中有一定作用。
可以在命令行中指定 metadata

-M KEY[=VAL], --metadata=KEY[:VAL] # 将 KEY 的内容设置为 VAL
--metadata-file=FILE # 读取 FILE 中的内容作为 metadata


## Rapidee {#rapidee}

修改 windows 注册表


## Rime {#rime}

<https://www.jianshu.com/p/296bba666604>


### 基本 {#基本}


#### 简述 {#简述}

Rime 的各种配置，均是由.yaml 文件所定义。yaml 是一种标记语言。.yaml 文件实际上是文本文档。可使用记事本、或 Emeditor 等进行编辑。

对 Rime 进行自定义，是通过对.custom.yaml 文件修改达成。不同的.custom.yaml 文件，控制不同的功能实现。

.custom.yaml 实际上是相当于对.yaml 文件打补丁，在重新部署后，会将.custom.yaml 中的内容写入.yaml 文件中，完成自定

-   weasel.yaml 是常规设置，主要控制托盘图标、候选词横竖排列、界面配色等等功能。那么，我们需要定制界面配色，只需在 weasel.custom.yaml 中修改，重新部署后就可实现
-   default.yaml 是默认设置，主要控制快捷键、按键上屏等等。

****以上是全局设置，亦即不论使用何种输入方案，均起作用。****

-   double_pinyin_flypy.custom.yaml 这种则是输入法方案设置。主要实现特殊标点符号、词库等功能。是针对特定输入方案的配置。

-【中州韻】 ibus-rime → Linux
-【小狼毫】 Weasel → Windows
-【鼠鬚管】 Squirrel → Mac OS X

Rime 從用戶文件夾加載配置如：[用戶資料夾](#用戶資料夾)


#### 共享資料夾 {#共享資料夾}

Rime 中所有文本文檔，均要求以 UTF-8 編碼，並建議使用 UNIX 換行符（LF）。

Rime 輸入法在查找一項資源的時候，會優先訪問 用戶文件夾 中的文件。 用戶文件不存在時，再到共享文件夾中尋找。

共享資料夾 包含預設輸入方案的源文件。 這些文件屬於 Rime 所發行軟件的一部份，在訪問權限控制較嚴格的系統上對用戶是只讀的，因此謝絕軟件版本更新以外的任何修改


#### 用戶資料夾 {#用戶資料夾}

Rime 從「用戶文件夾」讀取用家自訂的配置.
-【中州韻】 ~/.config/ibus/rime/ （0.9.1 以下版本爲 ~/.ibus/rime/）
-【小狼毫】 %APPDATA%\Rime
-【鼠鬚管】 ~/Library/Rime/

<!--list-separator-->

-  用戶資料夾 則包含爲用戶準備的內容，如：

    -   〔全局設定〕 default.yaml
    -   〔發行版設定〕 weasel.yaml
    -   〔預設輸入方案副本〕 &lt;方案標識&gt;.schema.yaml
    -   ※〔安裝信息〕 installation.yaml
    -   ※〔用戶狀態信息〕 user.yaml

<!--list-separator-->

-  編譯輸入方案所產出的二進制文件：

    -   〔Rime 棱鏡〕 &lt;方案標識&gt;.prism.bin
    -   〔Rime 固態詞典〕 &lt;詞典名&gt;.table.bin
    -   〔Rime 反查詞典〕 &lt;詞典名&gt;.reverse.bin

<!--list-separator-->

-  記錄用戶寫作習慣的文件：

    -   ※〔用戶詞典〕 &lt;詞典名&gt;.userdb/ 或 &lt;詞典名&gt;.userdb.kct
    -   ※〔用戶詞典快照〕 &lt;詞典名&gt;.userdb.txt、&lt;詞典名&gt;.userdb.kct.snapshot 見於同步文件夾

<!--list-separator-->

-  以及用戶自己設定的：

    -   ※〔用戶對全局設定的定製信息〕 default.custom.yaml
    -   ※〔用戶對預設輸入方案的定製信息〕 &lt;方案標識&gt;.custom.yaml
    -   ※〔用戶自製輸入方案〕及配套的詞典源文件

<!--list-separator-->

-  日誌：

    -   【中州韻】 /tmp/rime.ibus.\*
    -   【小狼毫】 %TEMP%\rime.weasel.\*
    -   【鼠鬚管】 $TMPDIR/rime.squirrel.\*

    各發行版的早期版本 用戶資料夾/rime.log

    註：以上標有 ※ 號的文件，包含用戶資料，您在清理文件時要注意備份！


#### 詳解輸入方案 {#詳解輸入方案}

````yaml
# 以下代碼片段節選自 luna_pinyin.schema.yaml

schema:
  schema_id: luna_pinyin
  name: 朙月拼音
  version: "0.9"
  author:
    - 佛振 <chen.sst@gmail.com>
  description: |
    Rime 預設的拼音輸入方案。
````

以上 schema/schema_id、schema/version 字段用於在程序中識別輸入方案， 而 schema/name、schema/author、schema/description 則主要是展示給用戶的信息。


#### 輸入法引擎與功能組件 {#輸入法引擎與功能組件}

````cfg
# luna_pinyin.schema.yaml
# ...

engine:                    # 輸入引擎設定，即掛接組件的「處方」
  processors:              # 一、這批組件處理各類按鍵消息
    - ascii_composer       # ※ 處理西文模式及中西文切換
    - recognizer           # ※ 與 matcher 搭配，處理符合特定規則的輸入碼，如網址、反查等
    - key_binder           # ※ 在特定條件下將按鍵綁定到其他按鍵，如重定義逗號、句號爲候選翻頁鍵
    - speller              # ※ 拼寫處理器，接受字符按鍵，編輯輸入碼
    - punctuator           # ※ 句讀處理器，將單個字符按鍵直接映射爲文字符號
    - selector             # ※ 選字處理器，處理數字選字鍵、上、下候選定位、換頁鍵
    - navigator            # ※ 處理輸入欄內的光標移動鍵
    - express_editor       # ※ 編輯器，處理空格、回車上屏、回退鍵等
    segmentors:              # 二、這批組件識別不同內容類型，將輸入碼分段
    - ascii_segmentor      # ※ 標識西文段落
    - matcher              # ※ 標識符合特定規則的段落，如網址、反查等
    - abc_segmentor        # ※ 標識常規的文字段落
    - punct_segmentor      # ※ 標識句讀段落
    - fallback_segmentor   # ※ 標識其他未標識段落
  translators:             # 三、這批組件翻譯特定類型的編碼段爲一組候選文字
    - echo_translator      # ※ 沒有其他候選字時，回顯輸入碼
    - punct_translator     # ※ 轉換標點符號
    - script_translator    # ※ 腳本翻譯器，用於拼音等基於音節表的輸入方案
    - reverse_lookup_translator  # ※ 反查翻譯器，用另一種編碼方案查碼
  filters:                 # 四、這批組件過濾翻譯的結果
    - simplifier           # ※ 繁簡轉換
    - uniquifier           # ※ 過濾重複的候選字，有可能來自繁簡轉換
````

除示例代碼中引用的組件外，尚有

````nil
- fluid_editor      # ※ 句式編輯器，用於以空格斷詞、回車上屏的【注音】、【語句流】等輸入方案，替換 express_editor，也可以寫作 fluency_editor
- chord_composer    # ※ 和絃作曲家或曰並擊處理器，用於【宮保拼音】等多鍵並擊的輸入方案
- table_translator  # ※ 碼表翻譯器，用於倉頡、五筆等基於碼表的輸入方案，替換 script_translator

````


### 部署 {#部署}

所有自定修改，都必须重新部署。在开始菜单可以找到【小狼毫】重新部署。

-   在开始菜单可以找到【小狼毫】重新部署。
-   右键托盘图标重新部署。

〔★〕重新佈署的方法是：
-【小狼毫】從開始菜單選擇「重新部署」；或當開啓托盤圖標時，在托盤圖標上右鍵選擇「重新佈署」；
-【鼠鬚管】在系統語言文字選單中選擇「重新佈署」；
-【中州韻】點擊輸入法狀態欄（或 IBus 菜單）上的(Deploy) 按鈕；

-   早於 ibus-rime 0.9.2 的版本：刪除用戶資料夾的 default.yaml 之後、執行 ibus-daemon -drx 重載 IBus

****wubi_pinyin.custom.yaml 文件在部署的时候,配置会写进 wubi_pinyin.yaml 中.****


### 同步 {#同步}

<https://www.jianshu.com/p/296bba666604>

Rime 没有云同步功能，但有本地同步功能，我们可以借助坚果云、onedrive 等第三方云实现个人词典和配置方案在不同电脑间的同步和备份。

1.  先打开用户资料夹，打开 installation.yaml 文件，在最下方添加如下代码：

<!--listend-->

````cfg
sync_dir: 'D:\Nutstore\RimeSync'
````

1.  开始菜单找到【小狼毫】用户资料同步，(也可以点击托盘图标，选择用户资料同步).

note：Rime 的同步功能，在个人词典是双向同步，在个人配置是单项同步。


### 配置 {#配置}


#### 横排选词 {#横排选词}

-   横排选词
    -   在【小狼毫】用户文件夹，修改 weasel.custom.yaml 文件，在 patch:后加入 “style/horizontal”: true
-   选词数修改
    -   在【小狼毫】用户文件夹，修改 default.custom.yaml 文件，在 patch:后加入”menu/page_size”: 9
-   修改 F4 快捷键
    -   在【小狼毫】用户文件夹，修改 default.custom.yaml 文件，在 patch:后加入”switcher/hotkeys”: -“Control+grave”
-   修改 Shift 切换键
    -   在【小狼毫】用户文件夹，修改 default.custom.yaml 文件，在 patch:后加入 “ascii_composer/switch_key”:
    -   Shift_L: commit_code
    -   Shift_R: commit_code


#### 设置 Rime 默认英文状态 {#设置-rime-默认英文状态}

默认情况下，Rime 使用“朙月拼音”，对应的配置文件为 luna_pinyin.schema.yaml。如果想将它设置为默认输入英文，则将该文件中 switches-&gt;ascii_mode-&gt;reset 的值修改为 1 即可.

****部署(deploy)**** 一下 Rime，使配置生效。

<https://www.jianshu.com/p/7eb4a2ac0b69>


### 定製指南 {#定製指南}

創建一個文件名的主體部份（「.」之前）與要定製的文件相同、次級擴展名（位於「.yaml」之前）寫作 .custom 的定製檔，形如：

````yaml
patch:
  "一級設定項/二級設定項/三級設定項": 新的設定值
  "另一個設定項": 新的設定值
  "再一個設定項": 新的設定值
  "含列表的設定項/@0": 列表第一個元素新的設定值
  "含列表的設定項/@last": 列表最後一個元素新的設定值
  "含列表的設定項/@before 0": 在列表第一個元素之前插入新的設定值（不建議在補靪中使用）
  "含列表的設定項/@after last": 在列表最後一個元素之後插入新的設定值（不建議在補靪中使用）
  "含列表的設定項/@next": 在列表最後一個元素之後插入新的設定值（不建議在補靪中使用）

````

patch 定義了一組「補靪」，以源文件中的設定爲底本，寫入新的設定項、或以新的設定值取代舊有的值。


### emoji {#emoji}

<https://github.com/rime/rime-emoji>
下載 opencc 檔案夾內容，將完整檔案夾放入 Rime 用戶檔案夾內

<https://github.com/rime/home/issues/186>


## Screen {#screen}


### Deskreen {#deskreen}


## Scrcpy {#scrcpy}

````sh
#支持鼠标控制、键盘输入、电脑剪切板复制粘贴、拖放文件传输到手机、以及拖放 APK 文件进行安装
# 0)手机打开开发者工具；
  #在搭载 Android 4.2 及更高版本的设备上，“开发者选项”屏幕默认情况下处于隐藏状态。
  #如需将其显示出来，请依次转到设置 > 关于手机，然后点按版本号七次。
  #返回上一屏幕，在底部可以找到开发者选项。
  #https://developer.android.com/studio/command-line/adb
````


#### adb {#adb}

````bat
rem 1)adb
>  .\adb.exe devices
  List of devices attached
  db64f3d7        unauthorized
> .\adb.exe usb
  restarting in USB mode
> .\adb tcpip 5555
  #拔掉你的数据线。
> .\adb connect IP :5555	#IP 地址 (设置 →关于手机→状态中查看)
````


#### scrcpy {#scrcpy}

````bat
rem 2) .\Scrcpy

cat > STEP << EOF
IP 					地址 (设置 →关于手机→状态)
adb.exe devices
adb tcpip 5555		其中 5555 为端口号
          拔掉数据线
adb connect IP:5555
scrcpy
scrcpy -b 3M -m 800	码率限制 3 Mbps，画面分辨率限制 800，数值可以随意调整。

如需切换回 USB 模式，执行：adb usb
EOF

````


#### cmd {#cmd}

````cfg
# 关闭手机屏幕	scrcpy -S
# 限制画面分辨率	scrcpy -m 1024 (比如限制为 1024)
# 修改视频码率	scrcpy -b 4M (默认 8Mbps，改成 4Mbps)
# 裁剪画面	scrcpy -c 1224:1440:0:0
# 表示分辨率 1224x1440 并且偏移坐标为 (0,0)
# 多设备切换	scrcpy -s 设备 ID (使用 adb devices 命令查看设备 ID)
# 窗口置顶	scrcpy -T
# 显示触摸点击	scrcpy -t
# 在演示或录制教程时，可在画面上对应显示出点击动作
# 全屏显示	scrcpy -f
# 文件传输默认路径	scrcpy --push-target /你的/目录
# 将文件拖放到 scrcpy 可以传输文件，此命令指定默认保存目录
# 只读模式(仅显示不控制)	scrcpy -n
# 屏幕录像	scrcpy -r 视频文件名.mp4 或 .mkv
# 屏幕录像 (禁用电脑显示)	scrcpy -Nr 文件名.mkv
# 设置窗口标题	scrcpy --window-title '异次元好棒！'
  # 同步传输声音	可借助 USBaudio 这个开源项目实现，但仅支持 Linux 系统
````


#### hotkey {#hotkey}

````cfg
  # 4) HotKey
Ctrl+b 		返回，或者可以按鼠标右键
Ctrl+h 		桌面，或者可以按鼠标中键
Ctrl+s 		多任务
Ctrl+p 		手机电源
Ctrl+g 		显示最佳窗口，或者可以双击手机画面外黑色区域
Ctrl+上下键 调节音量
Ctrl+左右键 旋转屏幕
Ctrl+o 		关闭设备屏幕，但 pc 端仍保持连接
Ctrl+c 		将设备剪贴板复制到计算机
Ctrl+v 		将计算机剪贴板粘贴到设备
Ctrl+shift+v 将计算机剪贴板同步到设备剪贴板
Ctrl+f 		切换全屏模式
````


#### scrcpy-gui {#scrcpy-gui}

<https://www.iplaysoft.com/scrcpy-gui.html>


## Rainmeter {#rainmeter}

Rainmeter allows you to display customizable skins on your desktop, from hardware usage meters to fully functional audio visualizers.


## RSShub {#rsshub}

````cfg
  # 1）用 Feed43 订阅任意网站 RSS
http://feed43.com/


# 2）RSS 全文订阅在线网站
http://fetchrss.com
http://fivefilters.org
http://fullcontentrss.com/
https://www.freefullrss.com/ #freefullrss 是完全免费的，输入你的 RSS 订阅地址。

# 3)自建 PSS
Heroku 平台，免费的
````


## VSCode {#vscode}


### plugins {#plugins}


#### Chinese {#chinese}


#### Jupyter {#jupyter}


#### LaTexWorkshop {#latexworkshop}


#### Markdown all in one {#markdown-all-in-one}


#### Markdown Preview Git {#markdown-preview-git}


#### Org-mode {#org-mode}


#### Python {#python}


#### Vim {#vim}


#### VS Code Org Mode {#vs-code-org-mode}

no agenda-view


#### VS-ORG {#vs-org}

有 agenda-view


### Remote-WSL {#remote-wsl}

````json
setting.json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe",   //cmd.exe
    "terminal.external.windowsExec": "D:\\Program Files\\JetBrains\\Anaconda3\\condabin\\conda"
}
````


## Vimdesktop {#vimdesktop}

tc
microexcel


## VimDesktop_browser {#vimdesktop-browser}

````cfg
# Browser:
Chrome:	 Vimium
FireFox: Tridactyl
     Vimperator/Pentadactylp

# Windows
# 1 )Hunt and Peck
  With any window focused, press Alt + ;
  Alternatively, via the command-line or AutoHotKey by specifying /hint:  hap.exe /hint

# 2 )GlobalVim
  GlobalVim the editor in window for exampe word, excel, notepad etc. by GeeKey(Capslock) + Vim(v).

# 3 )VimDesktop
VimDesktop = Vim Mode At Desktop

````


## WebDAV {#webdav}


### NetDsik {#netdsik}

-   Dropbox（美国，墙外）

<https://www.dropbox.com/>
2G
<https://dav.dropdav.com/>

-   Google drive（美国，墙外）

<https://drive.google.com>
5G
<https://dav-pocket.appspot.com/>

-   Teracloud（日本，墙内）

<https://teracloud.jp/>
15G
<https://nanao.teracloud.jp/dav/>

-   坚果云（中国，墙内）

<https://www.jianguoyun.com/>
流量限制
<https://dav.jianguoyun.com/dav/>

-   yandex（俄罗斯，墙内）

<https://disk.yandex.com/>
10G
<https://webdav.yandex.ru>


### appliation support WebDAV {#appliation-support-webdav}

[盘点22个支持坚果云WebDav的软件，数据同步不用愁！](https://zhuanlan.zhihu.com/p/128501633)

-   keepass
-   易码
-   纯纯写作
-   MWeb
-   NoteBility
-   Tampermonkey
-   静读天下
-   Floccus


## Windows {#windows}


### cmd {#cmd}

````bat
D:/(d:) #directly cd dir
cd Program File #cd dir

move C:\pagefile.sys E:\pagefile.sys

dir  /a #show hide file or dir
del  C:pagefile.sys
````


### AppData {#appdata}

-   locallow：共享数据存放文件，一般都可以清理,一些无用的共享文件。
-   Local：   本地保存文件，其中本地临时文件，AppData\Local\Temp\\下面的文件可以删除（注意是 Temp）。
-   Roaming： 保存应用程序运行后的数据信息，如果删除应用程序运行配置数据会丢失。


### AutoStart {#autostart}

Win+r

<startup> # 打开启动文件夹 将该应用的快捷方式从文件位置复制并粘贴到“启动”文件夹中

C:\Users\SWH\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup


### path {#path}

````bat
set path=tmp
echo %PATH%  #tmp  #当前 dos 中环境变量，变了之后，系统会刷新，重新找开一个 dos 即是刷新过的%path%
````


### openssh {#openssh}

setupssh-8.4p1-2.exe

C:\Program Files\OpenSSH


### PowerShell {#powershell}


### ClearCdisk {#clearcdisk}

````bat
https://zhuanlan.zhihu.com/p/87565681
rem 1) pagefile.sys
  move it from c to other disk,above link.

rem 2) swap.

rem 3) hiberfils.sys
CMD
  Powercf -h off  #delete hiberfils.sys , turn hibernation function
  Powercfg -h on  #restore hibernation
````


### hotkey {#hotkey}

````cfg
CTRL+SHIFT+ESC： 打开进程管理器；
WIN+左箭头： 当前窗口缩放为屏幕的一半，靠屏幕左侧显示；
WIN+右箭头： 当前窗口缩放为屏幕的一半，靠屏幕右侧显示；
WIN+上箭头： 最大化当前窗口；
WIN+下箭头： 还原和最小化当前窗口；
在桌面上，右键任何一个程序，鼠标定位到快捷键一栏，为该应用设置启动快捷键，然后你就可以通过这个这个快捷键来启动该程序啦；
WIN+R， 输入“msconfig”，弹出系统设置界面，可设置禁止、允许进程开机自启动；
WIN+R ，输入“psr”后回车：打开步骤记录器；
WIN+R， 输入“mip”，启动数学公式手写板；
WIN+Home： 最小化所有窗口，除了当前激活窗口；
WIN+M： 最小化所有窗口；
WIN+SHIFT+M： 还原最小化窗口到桌面上；
WIN+P： 选择一个演示文稿显示模式；
WIN+Pause： 显示系统属性对话框；
WIN+F： 打开 windows 帮助中心；
WIN+T： 切换任务栏上的程序；
WIN+ALT+数字： 让位于任务栏指定位置（按下的数字作为序号）的程序，显示跳转清单；

WIN+D： 显示桌面，再按一次还原桌面；
WIN+R： 打开运行，输入命令可以执行相应操作，输入路径可以打开对应路径，输入程序名称可以打开对应程序（前提是你打开的是 windows 下面的程序）;输入 cmd 打开 DOS 窗口，输入 notepad 打开记事本，输入 calc 打开计算器等。
WIN+E： 打开资源管理器；
CTRL+ALT+Delete： 程序不响应时用这一招结束不响应的程序，xp 下用得比较多；
WIN+L： 锁屏；
WIN+Tab： 切换程序；
ALT+SHIFT+TAB： 切换程序；
CTRL+W： 关闭资源管理器；
CTRL+Home： 跳转到文件最开头，直接按 Home 跳转到行头；
CTRL+End： 跳转到文件尾部，直接按 End 跳转到行尾；
ALT+双击： 查看文件属性；
WIN+数字键： 启动任务栏上的程序；
在桌面或者任何文件夹下，SHIFT+鼠标右键，可以在当前路径下打开 DOS 命令窗口；
在桌面或者任何文件夹下，CTRL+鼠标左键，拖动文件、文件夹都可以立马生成文件对应的副本；
新建只有扩展名的文件的方法：”.suffix.”，比如创建.gitignore，正常情况下 windows 是不允许创建的，但在扩展名后面加点，即.gitignore.就可以正常创建了；
````


### chocolatey {#chocolatey}

````cfg
#1 Install chocolatey
Set-ExecutionPolicy AllSigned
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

#2 Install OpenSSH
choco install openssh

#https://blog.csdn.net/tuzixini/article/details/82013230
````


### start {#start}

shell：startup # open start dir

put lnk in start dir


### MYSYS2 {#mysys2}


#### zsh {#zsh}

````cfg
pacman -Sy zsh
mkpasswd -c | sed -e 's/bash/zsh/' | tee -a /etc/passwd

(setq shell-file-name (executable-find "zsh.exe"))
(setenv "PATH" "C:\\programs\\msys2\\mingw64\\bin;C:\\programs\\msys2\\usr\\local\\bin;C:\\programs\\msys2\\usr\\bin;C:\\Windows\\System32;C:\\Windows")
````


## WSL {#wsl}


### 安装 {#安装}

````p
设置(win+i)->更新与安全->开发者选项->开发人员模式
在搜索栏(win+q),输入启用或关闭 windows 功能-->适用于 Linux 的 windows 子系统
在 Microsoft Store 中搜索 WSL，选择系统下载安装

卸载删除 wsl
wslconfig /u <DistributionName>
wslconfig /unregister Ubuntu
````


### 配置源 {#配置源}

sudo vim /etc/apt/sources.list


#### aliyun {#aliyun}

````cfg
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

````


#### tsinghua {#tsinghua}

````cfg
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
````


#### update {#update}

````cfg
jsudo apt-get update  # 更新软件源中的所有软件列表
sudo apt-get upgade  # 更新软件
sudo apt-get dist-upgrade  #sudo apt-get dist-upgrad
````


### run gui-app {#run-gui-app}

````cfg
# open Mobaxterm X server

 /etc/profile
export DISPLAY=:0
export NO_AT_BRIDGE=1

````


### NOTE {#note}


#### 中文乱码 {#中文乱码}

````sh
/etc/environment(文件末尾添加)
export LC_ALL="zh_CN.UTF-8"

sudo locale-gen zh_CN.UTF-8

# 空格乱码，安装中文字体
sudo apt-get install fonts-droid-fallback ttf-wqy-zenhei ttf-wqy-microhei fonts-arphic-ukai fonts-arphic-uming
````


## Scoop {#scoop}


### 安装 {#安装}

使用需要翻墙,v2rayN


#### install {#install}

````sh
# input in powershell
$PSVersionTable.PSVersion.Major   #查看 Powershell 版本, require 3+
$PSVersionTable.CLRVersion.Major  #查看.NET Framework 版本, require 4.5+

# install
set-executionpolicy remotesigned -s currentuser  # 先设置 PowerShell 允许执行未签名脚本
  # or # set-executionpolicy remotesigned -scope currentuser
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')   # 下载 Scoop 安装脚本进行安装
  # or # Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
  # or # iwr -useb get.scoop.sh | iex

# iex (new-object net.webclient).downloadstring('https://raw.githubusercontent.com/lukesampson/scoop/master/bin/install.ps1')

# 用户安装的程序和 scoop 本身位于 C:\Users<user>\scoop。全局安装的程序（–global）位于 C:\ProgramData\scoop

# 将 Scoop 安装到自定义目录(命令行方式):
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 将 Scoop 配置为将全局程序安装到自定义目录 SCOOP_GLOBAL(命令行方式)
$env:SCOOP_GLOBAL='D:\GlobalScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')

# cmd
scoop cache rm <app> 用来删除所下载的安装文件以便节省硬盘空间。
scoop cleanup <app>  可以用来删掉软件的旧版本，注意全局设置。
scoop hold <apps>    禁止指定软件停止更新
scoop unhold <apps>  来允许指定软件继续更新
# 有一款叫 scoop-backup 的软件可以把当前所安装的软件都导出成一个.ps1 文件或者.bat 文件。 双击该文件可以恢复整个 Scoop 软件列表。

````


#### 完整步骤 {#完整步骤}

````sh
使用需要翻墙,v2rayN
# 设置环境变量
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
$env:SCOOP_GLOBAL='D:\Scoop\GlobalScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')
  # root 权限

# 安装 scoop
set-executionpolicy remotesigned -s currentuser  # 先设置 PowerShell 允许执行未签名脚本
  # or # Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  # or # set-executionpolicy remotesigned -scope currentuser
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')   # 下载 Scoop 安装脚本进行安装
  # or # iex (new-object net.webclient).downloadstring('https://raw.githubusercontent.com/lukesampson/scoop/master/bin/install.ps1')
  # or # Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
  # or # iwr -useb get.scoop.sh | iex

# 设置环境变量之后，建议将默认目录下的所有文件复制到新目录下

# 开始安装软件
scoop install aria2
# scoop install <软件名>
# global 目录下安装：scoop install -g <软件名>

# 找不到软件？添加软件库
scoop bucket add <bucketname>
````


#### bucket {#bucket}


#### aria2 {#aria2}

````bat
rem  打开 16 线程（aria2 编译版本默认最高线程为 16，需要更高的请自行编译）
scoop config aria2-max-connection-per-server 16

scoop config aria2-split 16
scoop config aria2-min-split-size 1M
````


### 常用命令 {#常用命令}

````cfg
scoop help #查看帮助
scoop help <某个命令> # 具体查看某个命令的帮助

scoop install <app>   # 安装 APP
scoop uinstall <app>  # 卸载 APP

scoop list  # 列出已安装的 APP
scoop search # 搜索 APP
scoop status # 检查哪些软件有更新

scoop update # 更新 Scoop 自身
scoop update <app1> <app2> # 更新某些 app
scoop update *  # 更新所有 app （前提是需要在 apps 目录下操作）

scoop bucket known #通过此命令列出已知所有 bucket（软件源）
scoop bucket add bucketName #添加某个 bucket

scoop cache rm <app> # 移除某个 app 的缓存

# 显示某个 app 的信息
scoop info <app>
# 在浏览器中打开某 app 的主页
scoop home <app>
# 比如
scoop home git
````


### 安装卸载软件 {#安装卸载软件}

````cfg
# 安装之前，通过 search 搜索 APP, 确定软件名称
scoop search  xxx

# 安装 APP
scoop install <app>

# 安装特定版本的 APP；语法 AppName@[version]，示例
scoop install git@2.23.0.windows.1

# 卸载 APP
scoop uninstall <app> #卸载 APP
````


### 更新软件 {#更新软件}

````cfg
scoop update # 更新 Scoop 自身

scoop update appName1 appName2 # 更新某些 app

# 更新所有 app （可能需要在 apps 目录下操作）
scoop update *

# 禁止某程序更新
scoop hold <app>
# 允许某程序更新
scoop unhold <app>
````


### 清除缓存与旧版本 {#清除缓存与旧版本}

````cfg
# 查看所有以下载的缓存信息
scoop cache show

# 清除指定程序的下载缓存
scoop cache rm <app>

# 清除所有缓存
scoop cache rm *

# 删除某软件的旧版本
scoop cleanup <app>

# 删除全局安装的某软件的旧版本
scoop cleanup <app> -g

# 删除过期的下载缓存
scoop cleanup <app> -k
````


### 别名 {#别名}

````cfg
 注意：请在 Powershell 中运行下面的命令
# 可用操作
scoop alias add|list|rm [<args>]

## 添加别名，格式：
scoop alias add <name> <command> <description>

# 示例：（注意：必须在 Powershell 中运行）
scoop alias add st 'scoop status' '检查更新'
# 检查已添加的别名
scoop alias list -v

Name Command      Summary
---- -------      -------
st   scoop status 检查更新

# 测试已添加的别名 st
scoop st

# 另一个示例：
scoop alias add rm 'scoop uninstall $args[0]' '卸载某 app'
````


### 版本之间切换 {#版本之间切换}

````cfg
scoop reset [app]@[version]

scoop reset idea-ultimate-eap@201.6668.13
scoop reset idea-ultimate-eap@201.6073.9
# 切换到最新版本
scoop reset idea-ultimate-eap
````


### 软件源 Bucket {#软件源-bucket}

````cfg

Scoop 默认的 Bucket 为 main ；官方维护的另一个 Bucket 为 extras，我们需要手动添加。

# bucket 的用法
scoop bucket add|list|known|rm [<args>]
scoop bucket add extras

# 添加第三方 bucket
scoop bucket add dorado https://github.com/h404bi/dorado
scoop install dorado/<app_name>
# 下面是 dorado 中特有的软件，测试其是否添加成功
scoop search trash

# 因为并不是所有的软件都有，所以可以通过添加“软件库”来找到自己想要的软件，例如下列：
1、main - Default bucket for the most common (mostly CLI) apps
2、extras - Apps that don’t fit the main bucket’s criteria
3、games - Open source/freeware games and game-related tools
4、nerd-fonts - Nerd Fonts
5、nirsoft - A subset of the 250 Nirsoft apps
6、java - Installers for Oracle Java, OpenJDK, Zulu, ojdkbuild, AdoptOpenJDK, 7、Amazon Corretto, BellSoft Liberica & SapMachine
8、jetbrains - Installers for all JetBrains utilities and IDEs
9、nonportable - Non-portable apps (may require UAC)
10、php - Installers for most versions of PHP
11、versions - Alternative versions of apps found in other buckets

extras：Scoop 官方维护的一个仓库，涵盖了大部分因为种种原因不能被收录进主仓库 的常用软件（在我看来是必须要添加的）。地址 ：lukesampson/scoop-extras
nirsoft：是一个 NirSoft 开发的小工具的安装合集。NirSoft 制作了大量的小工具，包括系统工具、网络工具、密码恢复等等，孜孜不倦、持续更新。
  - Bucket 地址 ：kodybrown/scoop-nirsoft
  - NirSoft 官网地址：NirSoft
dorado（添加了一些国内的 app，比如 qqplayer）h404bi/dorado
ash258：Ash258/scoop-Ash258
java：添加后可以通过它安装各种 jdk 、 jre
nerd-fonts ：包含各种字体

# 先添加 bucket
scoop bucket add extras
scoop bucket add nirsoft
scoop bucket add dorado https://github.com/h404bi/dorado
scoop bucket add Ash258 'https://github.com/Ash258/Scoop-Ash258.git'
scoop bucket add nerd-fonts
# 对于开发人员，可添加下面的两个
scoop bucket add java
scoop bucket add versions
````


### Question {#question}


#### 网络问题导致 app 安装失败 {#网络问题导致-app-安装失败}

在 scoop 的 cache 目录下的 application.txt 文件中找到下载路径与文 件名称.

可以尝试在浏览器或其他下载程序中下载该程序，下载完成,再更改文件名(application.txt 中的 out=后的信息)并将其放入 scoop 的 cache 目录，最后再次运行 scoop install application 即可安装


#### 利用 aria2 进行断点续传 {#利用-aria2-进行断点续传}

在 scoop 的 cache 目录下的 vscode-portable.txt 文件中找到下载路径与文 件名称.

aria2c.exe --input-file='D:\Scoop\Applications\cache\vscode-portable.txt

当提示下载完成后,scoop update vscode-portable


## tmux {#tmux}


### tmux {#tmux}

````cfg
Ctrl-B d， detach
Ctrl+b %：划分左右两个窗格。
Ctrl+b '"'：划分上下两个窗格。
Ctrl+b <arrow key>：光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b ;：光标切换到上一个窗格。
Ctrl+b o：光标切换到下一个窗格。
Ctrl+b {：当前窗格左移。
Ctrl+b }：当前窗格右移。
Ctrl+b Ctrl+o：当前窗格上移。
Ctrl+b Alt+o：当前窗格下移。
Ctrl+b x：关闭当前窗格。
Ctrl+b !：将当前窗格拆分为一个独立窗口。
Ctrl+b z：当前窗格全屏显示，再使用一次会变回原来大小。
Ctrl+b Ctrl+<arrow key>：按箭头方向调整窗格大小。
````


## total commander {#total-commander}


### 隐藏菜单 {#隐藏菜单}

[Configuration]

Mainmenu=NONE.MNU


### 启动最大化 {#启动最大化}

menu--&gt;configuration--&gt;save position


### note {#note}

1.  tc64 无法与 vimdesktop 配合
2.  cpastab++ + nkey 启动的 tc32 无法与 vimdesktop 配合
3.  注册版不能使用 plugins


## zsh {#zsh}

````sh
# # 查看系统当前使用的 shell
echo $SHELL
# 查看系统自带哪些 shell
cat /etc/shells

sudo apt update
sudo apt install zsh
# sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sudo apt install zsh
zsh --version

whereis zsh
# /usr/bin/zsh
sudo usermod -s /usr/bin/zsh $(whoami)
NOTE: wsl-terminal must set ./etc/wsl-terminal.conf; shell=/bin/bash -> shell=/bin/zsh

# 安装「Powerline」和「Powerline 字体」
sudo apt install powerline fonts-powerline

# theme
sudo apt install zsh-theme-powerlevel9k
echo "source /usr/share/powerlevel9k/powerlevel9k.zsh-theme" >> ~/.zshrc

# 语法高亮
sudo apt install zsh-syntax-highlighting
echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc

# 目录颜色修改
wget https://raw.githubusercontent.com/seebi/dircolors-solarized/master/dircolors.ansi-dark
mv dircolors.ansi-dark .dir_colors

# .bashrc / .zshrc
if [ -f ~/.dir_colors ]; then
  eval `dircolors ~/.dir_colors`
fi
````


## ohmyzsh {#ohmyzsh}

ZSH 有一个致力于与 Git 版本控制系统一起工作的完整框架——「Oh My ZSH」
要启用「Oh My ZSH」插件也需要编辑 ~/.zshrc 配置文件，在 plugin 变量的大括号（）中添加要启用的插件名称即可


#### github {#github}

````sh
sudo apt-get install zsh
sudo apt install git
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
# 注意：安装「Oh My ZSH」会自动更改 ~/.zshrc 配置文件
````


#### gitee {#gitee}

````sh
sudo apt-get install zsh
wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh
chmod +x install.sh

vim install.sh
> REPO=${REPO:-mirrors/oh-my-zsh}
# > REPO=${REPO:-daotoyi/ohmyzsh}
> REMOTE=${REMOTE:-https://gitee.com/${REPO}.git}

./install.sh
````


#### gitee {#gitee}

````sh
sudo apt-get install zsh
wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh
chmod +x install.sh

vim install.sh
> REPO=${REPO:-mirrors/oh-my-zsh}
# > REPO=${REPO:-daotoyi/ohmyzsh}
> REMOTE=${REMOTE:-https://gitee.com/${REPO}.git}

./install.sh
````


#### .zsh {#dot-zsh}

````sh
ZSH_THEME=""
   # 如果 ZSH_THEME=""则不启用任何主题.
   # 如果 ZSH_THEME="random",那么每次打开一个新的终端窗口时，电脑会随机选择一个主题使用，echo $RANDOM_THEME 可输出当前主题名称.
   ZSH_THEME="random" && ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" ),从喜欢的主题列表中选择随机主题
plugins=(git extract z) # 直接使用的插件,ohmyzsh inside
   # extract ,功能强大的解压插件，所有类型的文件解压一个命令 x 全搞定
   # 强大的目录自动跳转命令，会记忆你曾经进入过的目录，用模糊匹配快速进入你想要的目录: z *
   #https://www.jianshu.com/p/ba782b57ae96

plugins=(zsh-syntax-highlighting zsh-autosuggestions incr)

  -- zsh-syntax-highlighting
  sudo apt install zsh-syntax-highlighting
  echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
  #git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

  -- zsh-autosuggestions
  sudo apt install zsh-autosuggestion
  echo "source /usr/share/zsh-autosuggestion/zsh-autosuggestion.zsh" >> ~/.zshrc
  #git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

  -- incr
  cd ~/.oh-my-zsh/plugins/
  mkdir incr && cd incr
  wget http://mimosa-pudica.net/src/incr-0.2.zsh
  echo "ssource ~/.oh-my-zsh/plugins/incr/incr*.zsh" >> ~/.zshrc

source ~/.bash_profile   # 如果.bash_profile 中有配置内容的话
````


#### uninstall_oh_my_zsh {#uninstall-oh-my-zsh}

terminal: uninstall_oh_my_zsh


#### update {#update}

````cfg
upgrade_oh_my_zsh # mannual
export UPDATE_ZSH_DAYS=13  # 设置更新日期
DISABLE_AUTO_UPDATE="true" # 禁用自动更新
````


#### theme {#theme}

````cfg
'fletcherm'
'xiong-chiamiov-plus'
'jonathan'
'linuxonly'
'jnrowe'
arrow
````


## txd {#txd}

````cfg
connect.cfg
[[http://www.360doc.com/content/20/1028/10/10993297_942765341.shtml][关于通达信增加工具菜单栏，及外挂]]

MainWebTitle=Options
WebPageNum=1
WebPageStr01=板块轮动
WebPageStr01=http://www.treeid/py_bkturn
````


## Mobile App {#mobile-app}


### termux - terminal {#termux-terminal}


### magit {#magit}


### orgzly {#orgzly}


### foldersync - sync file {#foldersync-sync-file}


### syncthing - sync file {#syncthing-sync-file}


### keepass2android(/离线版)(for android) {#keepass2android--离线版----for-android}


### MiniKeePass(for iPhone / iPad) {#minikeepass--for-iphone-ipad}


### feeedme - RSS {#feeedme-rss}

较新版本支持 Inoreader 定义网址 www.innoreader.com


### Rolly - RSS {#rolly-rss}