+++
lastmod = "2022-12-11 10:56:00"
categories = ["Python"]
draft = false
toc = true
+++

## Emacs {#emacs}


### install {#install}


#### defvar {#defvar}

```lisp
(require 'package)

(add-to-list 'package-archives
       '("melpa" . "http://melpa.org/packages/") t)

(package-initialize)
(when (not package-archive-contents)
  (package-refresh-contents))

(defvar myPackages
  '(better-defaults
    material-theme))

(mapc #'(lambda (package)
    (unless (package-installed-p package)
      (package-install package)))
      myPackages)
```


### basic {#basic}

```cfg
basic(){
# 1) Tab 标签页
C-x t 2 ;; 新建 Tab
      1 ;; 关闭其它 Tab
      0 ;; 关闭当前 Tab
      b ;; 在新 Tab 中打开 Buffer

# 2) #.emacs 生效
  不重启 Emacs 让 .emacs 配置文件生效有四个函数可以做到：eval-last-sexp,eval-region,eval-buffer 和 load-file
M-x  eval-last-sexp 		使.emacs 中光标前的那一条语句立刻生效。
M-x  eval-region   			使.emacs 中选中的 region 中的语句立刻生效。
M-x  eval-buffer   			使当前的 buffer 中的设置语句立刻生效。
M-x  load-file ~/.emacs 	载入.emacs 文件，从而使其中的设置生。

# 3) 运行外部命令
M-! cmd

 在 Evil 里 :!start python %
 使用 Emacs 的运行外部命令的方法 M-! start python test.py
 }
```


### basicOperate {#basicoperate}

```sh
basicOperate(){
　　C-d (delete-char)，删除光标处的字符。
　　Backspace :(delete-backward-char)，删除光标前字符。
　　M-\ (delete-horizontal-space)，删除光标处的所有空格和 Tab 字符。
　　M-SPC (just-one-space)，删除光标处的所有空格和 Tab 字符，但留下一个。
　　C-x C-o (delete-blank-lines)，删除光标周围的空白行，保留当前行。
　　M-^ (delete-indentation)，将两行合为一行，删除之间的空白和缩进。参见下面两图。

　　C-k (kill-line)，从光标处起删除该行。
　　C-S-Backspace (kill-whole-line)，删除整行。
　　C-w (kill-region)，删除区域。
　　M-w (kill-ring-save)，复制到 kill 环，而不删除。
　　M-d (kill-word)，删除光标起一个单词。
　　M-Backspace (backward-kill-word)，删除光标前单词。
　　C-x Backspace (backward-kill-sentence)，往前删一句。
　　M-k (kill-sentence)，删除光标起一句。
　　M-z char (zap-to-char)，${删至字符 char 为止}。

# Yanking [https://www.cnblogs.com/robertzml/archive/2010/02/19/1669204.html]
  C-y 在调出内容后还把使用该命令的点加入了标记环，我们可以很方便的使用${C-x C-x 找到是哪个位置插入的文本}。
  M-y (yank-pop)，这个命令只能在刚用完 C-y 后使用。它的作用是用 kill 环中再前一个内容替换掉刚用 C-y 粘贴出来的内容。
    简单点说，假如 kill 环中有 1 号、2号、3号记录，使用 C-y 后 3 号记录调出，紧接着使用 M-y，删掉 3 号记录，换成 2 号记录，
    还有 M-y 是可以连着多次使用的，我们再按一下 1 号记录就出来了。
  C-h v kill-ring 可以查看我们之前删了些什么东西。

# CUA 绑定
  CUA（Common User Access），Windows，Linux，Mac 都是 CUA 系统。
  CUA 绑定就是说常规的 C-c (copy)，C-v (Paste)，C-x (Cut)还是按系统定义来使用。
  通过 M-x cua-mode 命令可以将 Emacs 的粘贴复制设为上述方式。

# window
　　C-x 4 b bufname (switch-to-buffer-other-window) 在另一个窗口打开缓冲。
　　C-x 4 C-o bufname (display-buffer) 在另一个窗口打开缓冲，但不选中那个窗口。
　　C-x 4 f filename (find-file-other-window) 在另一个窗口打开文件。
　　C-x 4 d directory (dired-other-window) 在另一个窗口打开文件夹。
　　C-x 4 m (mail-other-window) 在另一个窗口写邮件。
　　C-x 4 r filename (find-file-read-only-other-window) 在另一个窗口以只读方式打开文件。
}
```


### coding {#coding}

-**- coding:utf-8 -**-加在文件头，读取时会是以 utf-8 编码格式读入

如果文中出现“未经加工的文字”（'\\034'等不能识别的字符），会写入和读取以 raw-text 格式。


### calendar {#calendar}

```lisp
;;----------日历设置--------------------

;;设置日历的一些颜色
(setq calendar-load-hook
'(lambda ()
(set-face-foreground 'diary-face "skyblue")
(set-face-background 'holiday-face "slate blue")
(set-face-foreground 'holiday-face "white")))

;;设置我所在地方的经纬度，calendar 里有个功能是日月食的预测，和你的经纬度相联系的。
;; 让 emacs 能计算日出日落的时间，在 calendar 上用 S 即可看到
(setq calendar-latitude +39.54)
(setq calendar-longitude +116.28)
(setq calendar-location-name "北京")

;; 设置阴历显示，在 calendar 上用 pC 显示阴历
(setq chinese-calendar-celestial-stem
  ["甲" "乙" "丙" "丁" "戊" "己" "庚" "辛" "壬" "癸"])
(setq chinese-calendar-terrestrial-branch
  ["子" "丑" "寅" "卯" "辰" "巳" "戊" "未" "申" "酉" "戌" "亥"])

;; 设置 calendar 的显示
(setq calendar-remove-frame-by-deleting t)
(setq calendar-week-start-day 1) ; 设置星期一为每周的第一天
(setq mark-diary-entries-in-calendar t) ; 标记 calendar 上有 diary 的日期
(setq mark-holidays-in-calendar nil) ; 为了突出有 diary 的日期，calendar 上不标记节日
(setq view-calendar-holidays-initially nil) ; 打开 calendar 的时候不显示一堆节日

;; 去掉不关心的节日，设定自己在意的节日，在 calendar 上用 h 显示节日
(setq christian-holidays nil)
(setq hebrew-holidays nil)
(setq islamic-holidays nil)
(setq solar-holidays nil)
(setq general-holidays '((holiday-fixed 1 1 "元旦")
                         (holiday-fixed 2 14 "情人节")
                         (holiday-fixed 3 14 "白色情人节")
                         (holiday-fixed 4 1 "愚人节")
                         (holiday-fixed 5 1 "劳动节")
                         (holiday-float 5 0 2 "母亲节")
                         (holiday-fixed 6 1 "儿童节")
                         (holiday-float 6 0 3 "父亲节")
                         (holiday-fixed 7 1 "建党节")
                         (holiday-fixed 8 1 "建军节")
                         (holiday-fixed 9 10 "教师节")
                         (holiday-fixed 10 1 "国庆节")
                         (holiday-fixed 12 25 "圣诞节")))

;;Calendar 模式支持各种方式来更改当前日期
;;（这里的“前”是指还没有到来的那一天，“后”是指已经过去的日子）
;; q 退出 calendar 模式
;; C-f 让当前日期向前一天
;; C-b 让当前日期向后一天
;; C-n 让当前日期向前一周
;; C-p 让当前日期向后一周
;; M-} 让当前日期向前一个月
;; M-{ 让当前日期向后一个月
;; C-x ] 让当前日期向前一年
;; C-x [ 让当前日期向后一年
;; C-a 移动到当前周的第一天
;; C-e 移动到当前周的最后一天
;; M-a 移动到当前月的第一天
;; M-e 多动到当前月的最后一天
;; M-< 移动到当前年的第一天
;; M-> 移动到当前年的最后一天

;;Calendar 模式支持移动多种移动到特珠日期的方式
;; g d 移动到一个特别的日期
;; o 使某个特殊的月分作为中间的月分
;; . 移动到当天的日期
;; p d 显示某一天在一年中的位置，也显示本年度还有多少天。
;; C-c C-l 刷新 Calendar 窗口

;; Calendar 支持生成 LATEX 代码。
;; t m 按月生成日历
;; t M 按月生成一个美化的日历
;; t d 按当天日期生成一个当天日历
;; t w 1 在一页上生成这个周的日历
;; t w 2 在两页上生成这个周的日历
;; t w 3 生成一个 ISO-SYTLE 风格的当前周日历
;; t w 4 生成一个从周一开始的当前周日历
;; t y 生成当前年的日历

;;EMACS Calendar 支持配置节日：
;; h 显示当前的节日
;; x 定义当天为某个节日
;; u 取消当天已被定义的节日
;; e 显示所有这前后共三个月的节日。
;; M-x holiday 在另外的窗口的显示这前后三个月的节日。


;; 另外，还有一些特殊的，有意思的命令：
;; S 显示当天的日出日落时间(是大写的 S)
;; p C 显示农历可以使用
;; g C 使用农历移动日期可以使用

;;-----------日历设置结束----------------
```


### config {#config}

```lisp

M-x describe-font # font
customize-vairbale 将 select-enable-primary 的值设置为 t 即可  ;;共用系统剪贴板

(delete-selection-mode 1)		#选中后，输入会代替此选中部分
(global-auto-revert-mode 1)		#自动加载外部修改过的文件
(setq auto-save-default nil)	#关闭自动保存文件
(setq ring-bell-function 'ignore)	;;' #
(fset 'yes-or-no-p 'y-or-n-p)


;; # 不要补全 "'"
(sp-local-pair 'emacs-lisp-mode "'" nil :actions nil)
(sp-local-pair 'lisp-interaction-mode "'" nil :actions nil)
;; 也可以把上面两句合起来
(sp-local-pair '(emacs-lisp-mode lisp-interaction-mode) "'" nil :actions nil)


;; show-paren-mode #可以使鼠标在括号上是高亮其所匹配的另一半括号
;; # 以下； 光标 在括号内时就高亮包含内容的两个括号
(define-advice show-paren-function (:around (fn) fix-show-paren-function)
  "Highlight enclosing parens."
  (cond ((looking-at-p "\\s(") (funcall fn))
        (t (save-excursion
             (ignore-errors (backward-up-list))
             (funcall fn)))))

;; # 隐藏\r(^M) 换行符
(defun hidden-dos-eol ()
  "Do not show ^M in files containing mixed UNIX and DOS line endings."
  (interactive)
  (unless buffer-display-table
    (setq buffer-display-table (make-display-table)))
  (aset buffer-display-table ?\^M []))
;; # 隐藏\r(^M) 换行符
(defun remove-dos-eol ()
  "Replace DOS eolns CR LF with Unix eolns CR"
  (interactive)
  (goto-char (point-min))
  (while (search-forward "\r" nil t) (replace-match "")))

;; set language environment	#解决中文显示乱码
(set-language-environment 'UTF-8)		;'
(set-locale-environment "UTF-8")

;; "Insert the date in current position."	# 插入时间
(defun sucha-insert-time-string ()
(interactive)
(insert (format-time-string "[%Y-%m-%d, %a]")))
(define-key text-mode-map "\C-c\i" 'sucha-insert-time-string)	;'
}
```


### dired {#dired}

```cfg
Dired(){

+ 创建目录
g 刷新目录
C 拷贝
D 删除
R 重命名
d 标记删除
u 取消标记
x 执行所有的标记

#删除目录的时候 Emacs 会询问是否递归删除或拷贝， 这也有些麻烦我们可以用下面的配置将其设定为默认递归删除目录
(setq dired-recursive-deletes 'always)
(setq dired-recursive-copies 'always)

#重用唯一的一个缓冲区作为 Dired Mode 显示专用缓冲区(每一次你进入一个回车进入一个新的目录中是，一个新的缓冲区就会被建立)
(put 'dired-find-alternate-file 'disabled nil)
;; 主动加载 Dired Mode
;; (require 'dired)
;; (defined-key dired-mode-map (kbd "RET") 'dired-find-alternate-file)
;; 延迟加载
(with-eval-after-load 'dired
    (define-key dired-mode-map (kbd "RET") 'dired-find-alternate-file))

(require 'dired-x)	;'		#启用 dired-x 可以让每一次进入 Dired 模式时，使用新的快捷键 C-x C-j 就可以进 入当前文件夹的所在的路径。
(setq dired-dwin-target 1) 	#当一个窗口（frame）中存在两个分屏 （window）时，将另一个分屏自动设置成拷贝地址的目标。
```


### encoding {#encoding}

```cfg
# 1、打开文件出现乱码时，可以尝试修改字符的编码：
M-x revert-buffer-with-coding-system RET（回车）
# 或者
C-x return r
# 然后输入对应编码，如：utf-8 或者 chinese-gbk。

# 2、在保存的时候还可以指定文件的保存编码：
M-x set-buffer-file-coding-system
C-x return f

C-x C-m f utf-8-unix RET   ;;即可把当前文件转换为 utf-8 编码。
C-x C-m c RET C-x C-w RET ;;另存为指定编码的(会提示当前文件编码)

# 3、查看 Emacs 编码格式
M-x describe-coding-system
```


### encodeSet {#encodeset}

```lisp
;;;; 设置编辑环境
;; 设置为中文简体语言环境
(set-language-environment 'Chinese-GB)
;; 设置 emacs 使用 utf-8
(setq locale-coding-system 'utf-8)
;; 设置键盘输入时的字符编码
(set-keyboard-coding-system 'utf-8)
(set-selection-coding-system 'utf-8)
;; 文件默认保存为 utf-8
(set-buffer-file-coding-system 'utf-8)
(set-default buffer-file-coding-system 'utf8)
(set-default-coding-systems 'utf-8)
;; 解决粘贴中文出现乱码的问题
(set-clipboard-coding-system 'utf-8)
;; 终端中文乱码
(set-terminal-coding-system 'utf-8)
(modify-coding-system-alist 'process "*" 'utf-8)
(setq default-process-coding-system '(utf-8 . utf-8))
;; 解决文件目录的中文名乱码
(setq-default pathname-coding-system 'utf-8)
(set-file-name-coding-system 'utf-8)
;; 解决 Shell Mode(cmd) 下中文乱码问题

(defun change-shell-mode-coding ()
  (progn
    (set-terminal-coding-system 'gbk)
    (set-keyboard-coding-system 'gbk)
    (set-selection-coding-system 'gbk)
    (set-buffer-file-coding-system 'gbk)
    (set-file-name-coding-system 'gbk)
    (modify-coding-system-alist 'process "*" 'gbk)
    (set-buffer-process-coding-system 'gbk 'gbk)

    (set-file-name-coding-system 'gbk)))
```


### font（解决中文卡顿） {#font-解决中文卡顿}


#### dejavu-fonts {#dejavu-fonts}

<https://dejavu-fonts.github.io/Download.html>


#### 编码设置 {#编码设置}

```lisp
(set-language-environment 'UTF-8)
(set-locale-environment "UTF-8")
(set-default-coding-systems 'utf-8)
```


#### 中英文等宽设置 {#中英文等宽设置}

```lisp
(defun set-font (english chinese english-size chinese-size)
   (set-face-attribute 'default nil :font
                       (format   "%s:pixelsize=%d"  english english-size))
   (dolist (charset '(kana han symbol cjk-misc bopomofo))
     (set-fontset-font (frame-parameter nil 'font) charset
                       (font-spec :family chinese :size chinese-size))))

(set-font   "Dejavu Sans Mono" "WenQuanYi Zen Hei Mono" 14 14)
```


### loadfile {#loadfile}

```cfg
loadfile(){

cmd:
emacs -nw -Q #终端模式来运行 emacs: nw=nowindow Q=no welcomwindow
emacs dir\bin\runemacs.exe --debug-init	#方便调试（debug）配置文件

C:\\Users\\SWH/.ssh/known_host

3) load-file , load , require , autoload 之间的区别。
# load-file 用于打开某一个指定的文件，用于当你不想让 Emacs 来去决定加 载某个配置文件时（ .el 或者 .elc 文件）。
# load 搜索 load-path 中的路径并打开第一个所找到的匹配文件名的文件。此方法用于 你预先不知道文件路径的时候。
# require 加载还未被加载的插件。首先它会查看变量 features 中是否存在所要加载的 符号如果不存在则使用上面提到的 load 将其载入。
# autoload 用于仅在函数调用时加载文件，使用此方法可以大大节省编辑器的启动时间。

# 单文件的扩展都提供 require 的加载方式，只要把文件放到 load-path 下再 require 对应的功能就可以了，例如：(require 'template)		;'
# 其中 load-path 是 Emacs 需要加载文件的时候寻找的路径。这实际上是一个 list，里面依次列出了 Emacs 将要查找的路径，就类似于 Shell 里面的 PATH。
(add-to-list 'load-path		;'
         "~/emacs/extension"
         t)
# 最后一个参数 t 用于指定把你添加的路径加到表的末尾，一般都建议都添加到末尾
}
```


### path {#path}

```lisp
exec-path
process-environment

;; Emacs 有一套自身的环境变量，可以通过 getenv 获取。
;; Emacs 的环境变量不等同于 Shell 的环境变量.

;; 使用 shell 的 PATH 变量代替 Emacs 的 PATH 变量
(exec-path-from-shell-initialize)

;; 也可以将指定 shell 变量拷贝到 Emacs 里，比如 go 的 GOPATH 和 GOROOT
(exec-path-from-shell-copy-env "GOPATH")
(exec-path-from-shell-copy-env "GOROOT")

```


### platform {#platform}

```lisp
platform(){
(defconst *is-mac* (eq system-type 'darwin))			;'
(defconst *is-linux* (eq system-type 'gnu/linux))		;'
(defconst *is-windows* (or (eq system-type 'ms-dos) (eq system-type 'windows-nt)))

(when (eq system-type 'windows-nt)
  (setq locale-coding-system 'gbk     			;;gb18030
        w32-unicode-filenames 'nil
        file-name-coding-system 'gbk)		 	;;gb18030
  (set-next-selection-coding-system 'utf-8)		;;'
  (set-selection-coding-system 'utf-8)			;;'
  (set-clipboard-coding-system 'utf-16-le)) 	   	;; must be utf-16-le;'
}
```


### someSet {#someset}

```lisp
;; # 快速定位到(自定义目录)
;;定义变量 		(defconst my-projects-path "~/My-Projects" "My projects dir")
;;定义函数 		(defun goto-my-projects-dir () (interactive) (dired my-projects-path))
;;定义快捷键 	(define-key-list global-map '("C-x G p" goto-my-projects-dir)))) 		;'
(global-set-key (kbd "C-x G p") 'goto-my-projects-dir)	;'

;; # Shift+Space 设置标记（set-mark)
(global-set-key [?\S- ] 'set-mark-command)		;'

;; all backups goto ~/.backups instead in the current directory
(setq backup-directory-alist (quote (("." . "e:/Refine/Org/backups"))))

;; 行号背景 (set-face-background 'linum “#000000”)
;; 行号前景 (set-face-foreground 'linum “#CD661D”)
;; 当前行背景 (set-face-background 'hl-line “#BEBEBE”)
;; 当前行前景 (set-face-foreground 'hl-line “#000000”)
}
```


### setq {#setq}

```lisp
setq(){
;;-SET-ENVIRONMENT-------------------------------------------------
(setq jinz-default-dir (concat default-directory "/../jinzCFG"))
(setq jinz-default-path (concat default-directory "/.."))
(setq source-directory (concat jinz-default-path "/24.3"))
(setq-default frame-title-format (concat "%b - e@" (system-name)))
(setq user-init-file jinz-default-path)
(setq user-emacs-directory jinz-default-dir)
(setenv "HOME" jinz-default-dir)
(setenv "PATH" jinz-default-path)
;; set the default file path
(add-to-list 'load-path jinz-default-dir) ;'

(setenv "JAVA_HOME" "/usr/lib/jvm/jdk1.6.0_35")
(setenv "PATH" (concat (getenv "PATH") ":" (getenv "JAVA_HOME") "/bin"))
  export JAVA_HOME=/usr/lib/jvm/jdk1.6.0_35
  export PATH=$PATH:$JAVA_HOME/bin

Windows		#HOME  C:\Users\epich\AppData\Roaming
      #user-emacs-directory	~/.emacs.d
"PATH"
(setenv "PATH" (concat ".:/usr/texbin:/opt/local/bin" (getenv "PATH")))
(setq exec-path (append exec-path '(".:/usr/texbin:/opt/local/bin")))

;; #任务栏时间显示

;; display time
(setq display-time-day-and-date t)                             ;打开日期显示
(setq display-time-interval 1)
(display-time-mode t)
(display-time)
(setq display-time-format "%H:%M %Y/%m/%d %A")                 ;设定时间显示格式
(setq display-time-24hr-format t)                              ;打开 24 小时显示模式
(setq time-stamp-format "%3a %3b %2d %02H:%02M:%02S %:y (%z)") ;设置时间戳的显示格式

}
```


### sorceProxy {#sorceproxy}

```lisp
(setq url-proxy-services
      '(("no_proxy" . "^\\(localhost\\|10.*\\)")
        ("http" . "127.0.0.1:8888") ; http 代理 proxy_host 换成代理的域名或 ip，port 换成代理的端口
        ("https" . "127.0.0.1:8888") ;https 代理
        ))


;;(add-to-list '("melpa" . "http://melpa.milkbox.net/packages/"))										;; can't visit it
;;(add-to-list 'package-archives '("melpa" . "http://melpa.milkbox.net/packages/"))						;; can't visit it
;;(add-to-list 'package-archives '("melpa-stable" . "http://melpa-stable.milkbox.net/packages/"))		;; can't visit it
;;(add-to-list 'package-archives '("marmalade" . "http://marmalade-repo.org/packages/") 				;; can't visit it


;;(add-to-list 'package-archives
;;			'("gnu"   . "http://elpa.emacs-china.org/gnu/")
;;			'("melpa" . "http://elpa.emacs-china.org/melpa/")
;;			'("org-cn"   . "http://elpa.emacs-china.org/org/")
;;			'("elpa" . "http://tromey.com/elpa/")

;;			'("melpa" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")
;;			'("gnu" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")
;;			'("org" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/org/")

;;			'("melpa" . "http://mirrors.cloud.tencent.com/elpa/melpa/")
;;			'("gnu" . "http://mirrors.cloud.tencent.com/elpa/gnu/")
;;			'("org" . "http://mirrors.cloud.tencent.com/elpa/org/")

;;			'("melpa-cn" . "http://elpa.zilongshanren.com/melpa/")
;;			'("org-cn"   . "http://elpa.zilongshanren.com/org/")
;;			'("gnu-cn"   . "http://elpa.zilongshanren.com/gnu/")
;;			)		;;'

;; #Emacs 配置文件中（任何用到 package 特性的代码之前）添加如下内容
(setq package-archives '(("gnu" . "http://mirrors.ustc.edu.cn/elpa/gnu/")
                         ("melpa" . "http://mirrors.ustc.edu.cn/elpa/melpa/")
                         ("melpa-stable" . "http://mirrors.ustc.edu.cn/elpa/melpa-stable/")
                         ("org" . "http://mirrors.ustc.edu.cn/elpa/org/")))
;;'

;; #spacemacs 添加下面的代码到 .spacemacs 的 dotspacemacs/user-init 中
(setq configuration-layer--elpa-archives
      '(("melpa-cn" . "http://mirrors.ustc.edu.cn/elpa/melpa/")
        ("org-cn"   . "http://mirrors.ustc.edu.cn/elpa/org/")
        ("gnu-cn"   . "http://mirrors.ustc.edu.cn/elpa/gnu/")))
;;'
;; ${develop 分支应使用 configuration-layer-elpa-archives 代替上面代码中的 configuration-layer--elpa-archives （ -- 换成 - ）
;; 由于 Emacs 的 BUG，URL 末尾的 / 不可略去，否则无法正常工作}

  (setq configuration-layer--elpa-archives
      '(("melpa-cn" . "http://elpa.emacs-china.org/melpa/")
        ("org-cn"   . "http://elpa.emacs-china.org/org/")
        ("gnu-cn"   . "http://elpa.emacs-china.org/gnu/")))
```


### theme {#theme}

```lisp
(use-package molokai-theme
  :ensure t
  :init
  (setq molokai-theme-kit t)
  (load-theme 'molokai t)	;'
  )
}

;; tags(){

;; # 工具函数, 当保存文件时会自动的重新生成 TAGS:
;; # 可以将 my-auto-udpate-tags-when-save 函数加入 after-save-hook 中, 或者绑定到快捷键上.
(defun my-auto-update-tags-when-save (prefix)
  (interactive "P")
  (cond
   ((not my-tags-updated-time)
    (setq my-tags-updated-time (current-time)))

   ((and (not prefix)
         (< (- (float-time (current-time)) (float-time my-tags-updated-time)) 300))
    ;; < 300 seconds
    (message "no need to update the tags")
    )
   (t
    (setq my-tags-updated-time (current-time))
    (my-update-tags)
    (message "updated tags after %d seconds." (- (float-time (current-time)) (float-time my-tags-updated-time))))))

;; #	ctags 自身也有一个配置文件, 可以在该文件中定义规则来更好的生成 TAGS,
;; # 一个配置文件的示例如下:
;; --exclude=*.svn*
;; --exclude=*.git*
;; --exclude=*tmp*
;; --exclude=.#*
;; --tag-relative=yes
;; --recurse=yes
;; --langdef=js
;; --regex-js=/[ \t.]([A-Z][A-Z0-9._$]+)[ \t]*[=:][ \t]*([0-9"'\[\{]|null)/\1/n,constant/	#;"
;; --langdef=css
;; --langmap=css:.css
;; --regex-css=/^[ \t]*\.([A-Za-z0-9_-]+)/.\1/c,class,classes/
```


## Lsp {#lsp}


### VSCode {#vscode}

```lisp
;; script 找 vscode 的 executable
(def-package! lsp-python-ms
  :demand nil
  :hook (python-mode . lsp)
  :config
  ;; for executable of language server, if it's not symlinked on your PATH
  (setq lsp-python-ms-executable
        (string-trim (shell-command-to-string
         "fd -a ^Microsoft.Python.LanguageServer$ $HOME/.vscode/extensions | tail -1")))
  ;; for dev build of language server
  (setq lsp-python-ms-dir
        (file-name-directory lsp-python-ms-executable)))

```


### newsest nupkg url {#newsest-nupkg-url}

```lisp
(defun lsp-python-ms-latest-nupkg-url (&optional channel)
  (let ((channel (or channel "stable")))
    (unless (member channel '("stable" "beta" "daily"))
      (error (format "Unknown channel: %s" cnannel)))
    (with-temp-buffer
      (url-insert-file-contents
       (concat
        "https://pvsc.blob.core.windows.net/python-language-server-"
        channel
        "?restype=container&comp=list&prefix=Python-Language-Server-"
        (cond (*macos* "osx")
              (*linux* "linux")
              (*winnt* "win")
              (t (error (format "Unknown system: %s" system-type))))
        "-x64"))
      (pcase (xml-parse-region (point) (point-max))
        (`((EnumerationResults
            ((ContainerName . ,_))
            (Prefix nil ,_)
            (Blobs nil . ,blobs)
            (NextMarker nil)))
         (cdar
          (sort
           (mapcar (lambda (blob)
                     (pcase blob
                       (`(Blob
                          nil
                          (Name nil ,_)
                          (Url nil ,url)
                          (Properties nil (Last-Modified nil ,last-modified) . ,_))
                        (cons (encode-time (parse-time-string last-modified)) url))))
                   blobs)
           (lambda (t1 t2)
             (time-less-p (car t2) (car t1))))))))))
```


## Mail {#mail}


### 1.~/.emacs 添加 {#1-dot-dot-emacs-添加}

```lisp
;;发送 email
(setq send-mail-function (quote smtpmail-send-it))
(setq smtpmail-smtp-server "smtp.qq.com")
(setq smtpmail-smtp-service 25)
(setq user-full-name “小白”) ;;设置自己用户名
(setq user-mail-address "123456@qq.com”) ;;设置自己的邮箱
```


### 2.~/.authinfo 添加 {#2-dot-dot-authinfo-添加}

> 格式：machine 发件服务器 login 自己的邮箱 port 25 password 自己的邮箱密码
> 以 QQ 邮箱为例：
> machine smtp.qq.com login 123456@qq.com port 25 password 123456


### 3.创建邮件签名文件 {#3-dot-创建邮件签名文件}


### 4.收发邮件命令 {#4-dot-收发邮件命令}

```cfg
# <1>发送邮件
   M-x mail
# <2>发送邮件
   C-c C-s
# <3>发送并退出
   C-c C-c
# <4>抄送邮件
   C-c C-f C-c (注意不管是发送或抄送发送多人时，邮箱与邮箱账号之间必须加空格!)
# <5>插入文本
   C-x i
# <6>给邮件加上签名
   C-c C-w
# <7>Emacs 接收邮件
   # 在.emacs 配置
   (setq rmail-file-name “~/Mail/inbox.rmail")
   # //邮件读取
      M-x rmail
```


### &lt;8&gt;接收邮件快捷键命令 {#8-接收邮件快捷键命令}

```cfg
快捷键	命令	         功能
SPACE	scroll-up	卷屏，查看此消息的下一个画面
DEL	scroll-down	卷屏，查看此消息的上一个画面
.	rmail-beginning-of-message	移动到此消息的开头
n	rmail-next-undeleted-message	移动到下一条消息
p	rmail-previous-undeleted-message	移动到上一条消息
<	rmail-first-message	移动到第一条消息
>	rmail-last-message	移动到最后一条消息
j	rmail-show-message	如果这个命令的前面有一个数字 n,跳到第 n 条消息
g	refresh	刷新,获取新邮件

d	rmail-delete-forward	给邮件加上待删除标记，然后移动到下一个
C-d	rmail-delete-backward	给邮件加上待删除标记，然后移动到上一个
ESC n	rmail-next-message	移动到下一条消息；不管它是否已经加上待删除标记
ESC p	rmail-previous-message	移动到上一条消息；不管它是否已经加上待删除标记
u	rmail-undelete-previous-message	去掉邮件消息上的待删除标记
x	rmail-expunge	删除已经加有待删除标记的全部消息
s	rmail-expunge-and-save	删除加有待删除标记的消息并保存 RMAIL 文件
```


## Macro {#macro}


### macro {#macro}

```lisp
;; 3） backquote
;; backquote 是指反引号(`)  #`
(sp-local-pair 'emacs-lisp-mode "`" nil :actions nil)  #;'   关闭 Emacs 输入 backquote 时会插入两个反引号功能

;; # backquote 的作用与 quote 相似, 同样不对后面的表达式求值,
;; # 但是当 backquote 在宏中 与逗号(,)一起使用时, 用逗号修饰的变量将进行求值.
(defmacro my-print-2 (number)
  `(message "This is a number: %d" ,number))			;`
(pp (macroexpand '(my-print-2 (+ 2 3))))				;'
(my-print-2 (+ 2 3))
;; # 当输出 message 且 number 不带逗号时, my-print-2 的执行将提示错误. 因为宏不对参 数进行求值, 所以以上宏展开相当于:
(message "This is a number:" number)
;; # 如果加入逗号, 则在宏展开时会对变量 number 进行求值, 展开结果为:
(message "This is a number: %d" (+ 2 3))

;; 使用 macroexpand 和 macroexpand-all 获取宏展开的结果
}
```


### packages_installed_p {#packages-installed-p}

```lisp

;;; Add Packages ---  Another Method --->> Option

(defvar my/packages '(		;'
  ;; --- Use-package ---
    use-package
    emacs
   ;; --- Themes ---
      monokai-theme
    smart-mode-line
      ; solarized-theme
  ;; ---Search && Editor ---
    ivy
    counsel
    swiper
    smartparens
    smooth-scrolling
    hungry-delete
    recent
    smex
    ; helm
    ace-jump-mode
  ;; --- Auto-completion ---
    company
  ;; --- Syntax ---
    flycheck
  ;; --- Major Mode ---
    evil
    ; org-mode
    ; js2-mode
    ; markdown-mode
    exec-path-from-shell
  ;; --- Miojor Mode ---
    which-key
    crux
  ;; --- Python ---
    ; elpy
  ;; --- Web ---
    ; web-mode
    ; emmet-mode
  ;; --- Other ---
    vterm
    magit
   )
  "Default packages")

(defun my/packages-installed-p ()
    (loop for pkg in my/packages
          when (not (package-installed-p pkg)) do (return nil)
          finally (return t)))

(unless (my/packages-installed-p)
    (message "%s" "Refreshing package database...")
    (package-refresh-contents)
    (dolist (pkg my/packages)
      (when (not (package-installed-p pkg))
        (package-install pkg))))


```


### use-package {#use-package}

```lisp
;; 最简洁的格式
 (use-package restart-emacs)

;; 常用的格式
 (use-package smooth-scrolling
    :ensure t ;是否一定要确保已安装
    :defer nil ;是否要延迟加载
    :init (setq smooth-scrolling-margin 2) 	;初始化参数  ，init 后的代码在包的 require 之前执行
    :config (smooth-scrolling-mode t) 		;基本配置参数，config 后的代码在包的 require 之后执行
    :bind (("M-s O" . moccur)				;快捷键的绑定
         ("M-o" . isearch-moccur))
    :hook) 									;hook 模式的绑定

(eval-and-compile
    (setq use-package-always-ensure t) 		;不用每个包都手动添加:ensure t 关键字
    (setq use-package-always-defer t) 		;默认都是延迟加载，不用每个包都手动添加:defer t
    (setq use-package-always-demand nil)
    (setq use-package-expand-minimally t)
    (setq use-package-verbose t))

;; # 使用(use-package package-name) 可以避免:当 package-name 不在 load-path 中时,(require 'package-name)会抛出错误
;; # init 与 config 之后只能接单个表达式语句, 如果需要执行多个语句, 可以用 progn

;; 使用 autoload 则可以在真正需要这个包时再 require, 提高启动速度, 避免无谓的 require.
(use-package package-name
  :commands
  (global-company-mode)
  :defer t
  )
;; # 使用 commands 可以让 package 延迟加载, 如以上代码会首先判断 package 的符号是否 存在,
;; # 如果存在则在 package-name 的路径下加载. defer 也可以让 package-name 进行延迟加载.

```


### quelpa {#quelpa}

```lisp
;; ~/.emacs.d/init.el
;; quelpa - For those packages which are not in MELPA
(use-package quelpa
  :config ; 在 (require) 之后需要执行的表达式
  (use-package quelpa-use-package) ; 把 quelpa 嵌入 use-package 的宏扩展
  (quelpa-use-package-activate-advice)) ; 启用这个 advice

;; 直接 HTTP get 一个 elisp
(use-package dired+
  :quelpa (dired+ :fetcher url :url "https://www.emacswiki.org/emacs/download/dired+.el"))

;; git clone 一个 GitHub repo
(use-package elixir-mode
  :quelpa (elixir-mode :fetcher github :repo "elixir-editors/emacs-elixir"))

;; 只使用 repo 中的某些文件
(use-package mix
  :quelpa (mix.el :fetcher github :repo "ayrat555/mix.el" :files ("mix.el" "LICENSE"))
  :hook ((elixir-mode . mix-minor-mode)))
```


## Packages {#packages}


### ag {#ag}

```sh
ag > pt > ack > grep
ag(){
# Mac OS X 通过 Homebrew 安装
brew install the_silver_searcher

# Ubuntu 下安装
apt-get install silversearcher-ag

# Windows 下通过 msys2 安装（确保在 path 中）
pacman -S mingw-w64-i686-ag # 32 位电脑
pacman -S mingw-w64-x86_64-ag # 64 位电脑

# 安装好 ag 后我就可以安装 helm-ag 插件
(global-set-key (kbd "C-c p s") 'helm-do-ag-project-root)		;'
#可以在缓冲区对搜索到的结果进行直接的修改，这样就可以做到快速 的搜索与替换。

```


### crux {#crux}

```lisp

;; #该扩展提供了包含该场景在内的一系列优化快捷命令。

;;     优化版的回到行首
;;     快速打开 Emacs 配置文件
;;     快速连接两行等

(use-package crux
  :bind (("C-a" . crux-move-beginning-of-line)
         ("C-c ^" . crux-top-join-line)
         ("C-x ," . crux-find-user-init-file)
         ("C-c k" . crux-smart-kill-line)))
```


### drag-stuff {#drag-stuff}

```lisp
;; #上下移动行/块
(use-package drag-stuff
  :bind (("<M-up>". drag-stuff-up)
         ("<M-down>" . drag-stuff-down)))

```


### exec-path-from-shell {#exec-path-from-shell}

```lisp
;; golang 的开发环境中:\\
;; 配置中加入以下几行，（一定要在　package-initialize　之后加入）
　(exec-path-from-shell-copy-env "GOPATH")
　(exec-path-from-shell-copy-env "GOROOT")
　(when (memq window-system '(mac ns x))
　 (exec-path-from-shell-initialize))
```


### hipple {#hipple}

```lisp
;; #Hippie 补全
(setq hippie-expand-try-function-list '(try-expand-debbrev
                                        try-expand-debbrev-all-buffers
                                        try-expand-debbrev-from-kill
                                        try-complete-file-name-partially
                                        try-complete-file-name
                                        try-expand-all-abbrevs
                                        try-expand-list
                                        try-expand-line
                                        try-complete-lisp-symbol-partially
                                        try-complete-lisp-symbol))

(global-set-key (kbd "s-/") 'hippie-expand)		;'

```


### hungry-delete {#hungry-delete}

```lisp
(use-package hungry-delete
    :defer 2
    :bind (("C-c DEL" . hungry-delete-backward)		        ;; delete
           ("C-c d" . hungry-delete-forward)))
```


#### web-mode {#web-mode}

```lisp

;; # 将所有的 *.html 文件都使 用 web-mode 来打开,启用 web-mode 而非默认的 HTML Mode
(setq auto-mode-alist
      (append
       '(("\\.js\\'" . js2-mode))
       '(("\\.html\\'" . web-mode)) ;'
       auto-mode-alist))

;; # web-mode 支持在 HTML 文件中存在多语言，可以对不同的语言的缩减做出设置,下面的代码用于设置初始 的代码缩进，
(defun my-web-mode-indent-setup ()
  (setq web-mode-markup-indent-offset 2) ; web-mode, html tag in html file
  (setq web-mode-css-indent-offset 2)    ; web-mode, css in html file
  (setq web-mode-code-indent-offset 2)   ; web-mode, js code in html file
  )
(add-hook 'web-mode-hook 'my-web-mode-indent-setup)

;; # 下面的函数可以用于在两个空格和四个空格之间进行切换
(defun my-toggle-web-indent ()
  (interactive)
  ;; web development
  (if (or (eq major-mode 'js-mode) (eq major-mode 'js2-mode))
      (progn
        (setq js-indent-level (if (= js-indent-level 2) 4 2))
        (setq js2-basic-offset (if (= js2-basic-offset 2) 4 2))))

  (if (eq major-mode 'web-mode)
      (progn (setq web-mode-markup-indent-offset (if (= web-mode-markup-indent-offset 2) 4 2))
             (setq web-mode-css-indent-offset (if (= web-mode-css-indent-offset 2) 4 2))
             (setq web-mode-code-indent-offset (if (= web-mode-code-indent-offset 2) 4 2))))
  (if (eq major-mode 'css-mode)
      (setq css-indent-offset (if (= css-indent-offset 2) 4 2)))

  (setq indent-tabs-mode nil))

(global-set-key (kbd "C-c t i") 'my-toggle-web-indent)			;'

```


#### expand-region {#expand-region}

```lisp

(global-set-key (kbd "C-=") 'er/expand-region);'
;; # 类似 Sublime Text 中的多光标编辑
;; # 可以使用 Customized-group 来更改其高亮的背景色，将 highlight 改为 region
```


#### showLineRight {#showlineright}

```lisp
(defun linum-relative-right-set-margin ()
  "Make width of right margin the same as left margin"
  (let* ((win (get-buffer-window))
     (width (car (window-margins win))))
    (set-window-margins win width width)))

(defadvice linum-update-current (after linum-left-right-update activate)
  "Advice to run right margin update"
  (linum-relative-right-set-margin)
  (linum-relative-right-update (line-number-at-pos)))

(defadvice linum-delete-overlays (after linum-relative-right-delete activate)
  "Set margins width to 0"
  (set-window-margins (get-buffer-window) 0 0))

(defun linum-relative-right-update (line)
  "Put relative numbers to the right margin"
  (dolist (ov (overlays-in (window-start) (window-end)))
    (let ((str (overlay-get ov 'linum-str)))
      (if str
          (let ((nstr (number-to-string
                       (abs (- (string-to-number str) line)))))
            ;; copy string properties
            (set-text-properties 0 (length nstr) (text-properties-at 0 str) nstr)
            (overlay-put ov 'after-string
                         (propertize " " 'display `((margin right-margin) ,nstr))))))))
```


### ivy {#ivy}

```cfg

# https://emacs-china.org/t/ivy/12091

# ivy-minibuffer-map 提供了 6 个比较基础的移动方式绑定：

C-n 下一个选项
C-p 上一行选项
M-<第一个选项
M->最后一个选项
C-v 向下翻页，页数由 ivy-height 确定
M-v 向上翻页，同样页数由 ivy-height 确定

ivy 也提供了 2 个与历史操作有关的按键。

M-p 上一条历史记录
M-n 下一条历史记录
除此之外，C-a (move-beginning-of-line)、C-e (move-end-of-line) 等操作方 式一样在 minibuffer 下同样受用
```


#### iedit {#iedit}

```lisp
(global-set-key (kbd "M-s e") 'iedit-mode) ;'
```


#### mutilple-cursor {#mutilple-cursor}

<https://github.com/magnars/multiple-cursors.el>


#### semx {#semx}

```lisp
(require 'smex)
  (global-set-key [(meta x)] (lambda ()
                            (interactive)
                            (or (boundp 'smex-cache)
                                (smex-initialize))
                            (global-set-key [(meta x)] 'smex)
                            (smex)))

  (global-set-key [(shift meta x)] (lambda ()
                                (interactive)
                                (or (boundp 'smex-cache)
                                    (smex-initialize))
                                (global-set-key [(shift meta x)] 'smex-major-mode-commands)
                                (smex-major-mode-commands)))
```


#### yasnippet {#yasnippet}

```lisp
;; # 是一个代码块补全的插件
;; # 下面的配置文件将其在所有 的编程语言的模式中激活。
(yas-reload-all)
(add-hook 'prog-mode-hook #'yas-minor-mode)

yas-new-snippet (C-c & C-n)
```


### shell {#shell}


#### evil {#evil}

```lisp

evil(){
(setq evil-default-state 'emacs)	;'
# ;这个是打开文件后默认进入 emacs 模式,在 emacs 和 vim 模式里面切换：C-z

(evil-mode 1)	#激活
(setcdr evil-insert-state-map nil)
# 下面的代码可以将 insert state map 中的快捷键清空，使其可以回退（Fallback）到 Emacs State 中，
# 这样我们之前的 Emacs State 里面定义的 C-w 等快捷键就不会被 evil insert minor mode state 所覆盖，
(define-key evil-insert-state-map [escape] 'evil-normal-state)	;'

(define-key evil-emacs-state-map (kbd "C-o") 'evil-execute-in-normal-state)	;'
; C-o 按键调用 vim 功能（临时进入 normal 模式，然后自动回来）比如，你要到第一行，可以使用 emacs 的 M-<，也可以使用 evil 的 C-o gg
; "Fuck you!" 如何删除""里面的内容呢？-->C-o di ; 比如 C-o 3dd C-o dib C-o yy C-o p C-o f *

; 下面 4 行是设置使用 C-d 作为 ESC 按键
(define-key evil-insert-state-map (kbd "C-d") 'evil-change-to-previous-state)
(define-key evil-normal-state-map (kbd "C-d") 'evil-force-normal-state)
(define-key evil-replace-state-map (kbd "C-d") 'evil-normal-state)
(define-key evil-visual-state-map (kbd "C-d") 'evil-exit-visual-state)

; 以下设置时使用 t 作为多剪贴板的起始按键，比如 tay(不是 "ay 哦) tap(就是"ap 啦)~
(define-key evil-normal-state-map "t" 'evil-use-register)	; '

}

```


#### evil-leader {#evil-leader}

```lisp

evil-leader (){
# 根据 cofi/evil-leader 的说明，你应该在激活 evil-mode 之前就激活 global-evil-leader-mode，
# 否则 evil-leader 在几个初始缓冲区(scratch, Message,…)上将不生效。
(global-evil-leader-mode)

(evil-leader/set-key
  "ff" 'find-file
  "bb" 'switch-to-buffer
  "0"  'select-window-0
  "1"  'select-window-1
  "2"  'select-window-2
  "3"  'select-window-3
  "w/" 'split-window-right
  "w-" 'split-window-below
  ":"  'counsel-M-x
  "wM" 'delete-other-windows
  )
}

```


#### Window-numbering {#window-numbering}

```lisp

Window-numbering(){

(window-numbering-mode 1)

}

```


#### Evil-Surround {#evil-surround}

```lisp

Evil-Surround(){

#  Vim 上非常常用的插件改写的，使用它可以快速的将选中区域进行 匹配的操作，例如选中区域两边同时进行添加或修改括号，引号等操作。
# 简单的使用方法就是在选中所选区域后，使用 S( 来将选中区域包括在括号之中。如果想 将括号改变成 =”= 可以在选中后使用 =cs(“=
(require 'evil-surround)
(global-evil-surround-mode)		;'

}

ivy_counsel_swiper(){
(use-package ivy
  :defer 1
  :demand
  :hook (after-init . ivy-mode)
  :config
  (ivy-mode 1)
  (setq ivy-use-virtual-buffers t
        ivy-initial-inputs-alist nil
        ivy-count-format "%d/%d "
        enable-recursive-minibuffers t
        ivy-re-builders-alist '((t . ivy--regex-ignore-order))) ;'
  (ivy-posframe-mode 1)		;; set it will bug in startup
  ))

(use-package counsel
  :after (ivy)
  :bind (("M-x" . counsel-M-x)
         ("C-x C-f" . counsel-find-file)
         ("C-c f" . counsel-recentf)
         ("C-c g" . counsel-git)))

(use-package swiper
  :after ivy
  :bind (("C-s" . swiper)
         ("C-r" . swiper-isearch-backward))
  :config (setq swiper-action-recenter t
                swiper-include-line-number-in-search t))

}

company(){
(use-package company
  :config
  (setq company-dabbrev-code-everywhere t
        company-dabbrev-code-modes t
        company-dabbrev-code-other-buffers 'all
        company-dabbrev-downcase nil
        company-dabbrev-ignore-case t
        company-dabbrev-other-buffers 'all
        company-require-match nil
        company-minimum-prefix-length 2
        company-show-numbers t
        company-tooltip-limit 20
        company-idle-delay 0
        company-echo-delay 0
        company-tooltip-offset-display 'scrollbar
        company-begin-commands '(self-insert-command))
  (push '(company-semantic :with company-yasnippet) company-backends) 	;'
  :hook ((after-init . global-company-mode)))

}

Flycheck(){

#默认 Emacs 自带了 Flymake，但 Flycheck 是一个更优的方案。
建议全局启用：
(use-package flycheck
  :hook (after-init . global-flycheck-mode))

在编程语言的模式下启用：
(use-package flycheck
  :hook (prog-mode . flycheck-mode))

}
 which_key(){
(use-package which-key
  :defer nil
  :config (which-key-mode))
}

ivy_posframe(){

#Note:;set it will bug in startup
显示在左下角的 MiniBuffer 移动视线范围大，移动到中央位置，更合适一些。
(use-package ivy-posframe
  :init
  (setq ivy-posframe-display-functions-alist
    '((swiper . ivy-posframe-display-at-frame-center)		;'
      (complete-symbol . ivy-posframe-display-at-point)
      (counsel-M-x . ivy-posframe-display-at-frame-center)
      (counsel-find-file . ivy-posframe-display-at-frame-center)
      (ivy-switch-buffer . ivy-posframe-display-at-frame-center)
      (t . ivy-posframe-display-at-frame-center)))
}

ace_window(){
(use-package ace-window
    :bind (("M-o" . 'ace-window)))		;'
}

```


#### shell-mode {#shell-mode}

```lisp

;; 在执行 ls – color=auto 命令的时候输出的色彩信息能够被 Emacs 正确解析。

 (autoload 'ansi-color-for-comint-mode-on "ansi-color" nil t)
 (add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on t)

```


#### exec-path-from-shell {#exec-path-from-shell}

```lisp


;; # 启用 exec-path-from-shell , 在 emacs 启动时可能会提示 PATH 变量重复定义, 解决方案如下:
(use-package exec-path-from-shell
  :ensure t
  :if (and (eq system-type 'darwin) (display-graphic-p))		;'
  :config
  (progn
    (when (string-match-p "/zsh$" (getenv "SHELL"))
      (setq exec-path-from-shell-arguments '("-l")))			;'
    (exec-path-from-shell-initialize)
    )
  )
;; # if 子句可以确定启用 Package 的条件, 在 config 子句中向 exec-path-from-shell-arguments 即可消除这个警告
;; # ensure 子句来确保 Package 被安装. 如果要使用 stable 版, 则添加以下子句
:pin melpa-stable

```


#### shell mode hotkey {#shell-mode-hotkey}

```cfg

M-x shell：运行一个子 Shell，该子 Shell 对应于 emacs 中的一个名为*Shell*的缓冲区，此后我们就可以交互式的运行 Shell 命令了。
C-c C-c 相当于 Bash 下的 C-c
C-c C-z 相当于 Bash 下的 C-z
C-c C-d 相当于 Bash 下的 C-d
M-p 执行前一条命令
C-n 执行下一条命令
C-c C-o 删除最后一条命令产生的输出
C-c C-r 屏幕滚动到最后一条命令输出的开头
C-c C-e 屏幕滚动到最后一套命令输出的结尾
C-c C-p 查看前一条命令的输出
C-c C-n 查看后一条命令的输出
M-x term：运行一个子 Shell，该子 Shell 对应于 emacs 中的一个名为*Terminal*的缓冲区。使用该命令获得的子 Shell 是一个完整的 Shell 的模拟，与我们直接在 Shell 中操作没有什么差别。
M-x eshell：运行 emacs shell，该 Shell 为 emacs 自己实现的一个 shell，而前面运行的 shell 都为系统中的 shell 程序(例如：/bin/csh 等）。我们可以通过设置变量 shell-file-name 来设置 emacs 所使用的默认 shell

```


#### shell mode skill {#shell-mode-skill}

```lisp

M-! cmd RET(M-x shell-command)
运行命令并把执行结果显示在名为*Shell Command Output*缓冲区中;加前缀 C-u 表示将其输出放到编辑区中光标所在的位置处
M-| cmd RET(M-x shell-command-region)
运行 Shell 命令，并使用编辑窗口中选定的区域作为该 Shell 命令的输入，然后可以选择是否用该 Shell 命令的输出来替换编辑窗口中选中的区域。

```


#### eshell {#eshell}

\#+begin_src lisp

eshell(){

在.emacs 下，配置如下内容：
(setq ansi-color-for-comint-mode t)
然后执行 ansi-term 命令，按 Enter 执行默认程序 /bin/bash 即可。但是 emacs 的好多命令都不能用了。
}

<!--list-separator-->

-  plink

    ```lisp

    M-x eshell
      plink host@ip

    ```


#### shell outlin-mode {#shell-outlin-mode}

```lisp

 (setq outline-regexp ".*[bB]ash.*[#\$]")
设置标题以后，在 Shell mode 里面
- 输入 M-x outline-minor-mode 就可以享受 outline-mode 带来的便利
- 输入 M-x hide-body 或者 M-x hide-all 命令折叠起 Shell buffer 里的所有命令
- 移动光标到 ls *.el 所在的行,使用 M-x show-entry 或者 M-x show-subtree 命令展开 ls *.el 命令

 outline-regexp 变量是一个全局变量，所以对 outline-regexp 的值势必改变其他模式中的 outline-minor-mode 的行为方式.
->方法：使用一个函数为每一个 buffer 设置分别的 outline-regexp，并且把 outline-regexp 变量修改为特定 buffer 范围内的局部变量。

(defun set-outline-minor-mode-regexp ()
    ""
    (let ((find-regexp
           (lambda
             (lst mode)
             ""
             (let
                 ((innerList
                   (car lst)))
               (if innerList
                   (if
                       (string=
                        (car innerList)
                        mode)
                       (car
                        (cdr innerList))
                     (progn
                       (pop lst)
                       (funcall find-regexp lst mode))))))))
      (outline-minor-mode 1)
      (make-local-variable 'outline-regexp)
      (setq outline-regexp (funcall find-regexp outline-minor-mode-list major-mode))))

这个函数首先定义了一个匿名函数，存储在 find-regexp 变量中，这个函数通过递归的方式遍历一个嵌套列表，直至找到与给定模式对应的值；然后启动 outline-minor-mode，修改 outline-regexp 为局部变量，然后调用上述的匿名函数设置正确的 outline-regexp。

  (add-hook 'shell-mode-hook      'set-outline-minor-mode-regexp t )
  (add-hook 'sh-mode-hook         'set-outline-minor-mode-regexp t )
  (add-hook 'emacs-lisp-mode-hook 'set-outline-minor-mode-regexp t )
  (add-hook 'perl-mode-hook       'set-outline-minor-mode-regexp t )

需要一个全局变量 outline-minor-mode-list 来存储 set-outline-minor-mode-regexp 函数所需的所有数据。

 (setq outline-minor-mode-list
      (list '(emacs-lisp-mode "(defun")
      '(shell-mode ".*[bB]ash.*[#\$] ")
      '(sh-mode "function .*{")
      '(perl-mode "sub ")

 ))

```


#### linux {#linux}

```lisp

(setq shell-file-name "/bin/bash")
export EMACSSHELL=/usr/bin/zsh

使用一个支持 ANSI color 的 Shell 进程，那么最好在你的 Emacs 配置文件里面加入下面两行，以便在执行 ls – color=auto 命令的时候输出的色彩信息能够被 Emacs 正确解析。
(autoload 'ansi-color-for-comint-mode-on "ansi-color" nil t)
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on t)

-----
https://blog.csdn.net/superwen_go/article/details/8234342

```


### shell enhance {#shell-enhance}


#### mutil open {#mutil-open}

```lisp

;; 1)先用 rename-buffer 把打开的那个*eshell* buffer 重命名为其他命令,再调用 M-x eshell

;; 2)使用 C-u 数字 n M-x eshell 会创建一个编号为 n 的的 eshell 窗口
```


#### rename-buffer {#rename-buffer}

```lisp

(global-set-key (kbd "C-c z") 'shell)
(global-set-key (kbd "<f10>") 'rename-buffer)

```


#### goback windows {#goback-windows}

```lisp

 (when (fboundp 'winner-mode)
  (winner-mode)
  (windmove-default-keybindings))
;; # 然后就可以使用 Ctrl-c ← （对，就是向左的箭头键）组合键，退回你的上一个窗口设置。

```


#### go shell &amp;&amp; auto-rename-buffer(with remote host) {#go-shell-and-and-auto-rename-buffer--with-remote-host}

```lisp

(global-set-key (kbd "C-c z") 'shell)
(global-set-key (kbd "C-c z") (quote shell))

  (defun rename-buffer-in-ssh-login (cmd)
    "Rename buffer to the destination hostname in ssh login"
    (if (string-match "ssh [-_a-z0-9A-Z]+@[-_a-z0-9A-Z.]+[ ]*[^-_a-z0-9-A-Z]*$" cmd)
        (let (( host (nth 2 (split-string cmd "[ @\n]" t) )))
        (rename-buffer (concat "*" host)) ;
         (add-to-list 'shell-buffer-name-list (concat "*" host));
                 (message "%s" shell-buffer-name-list)
        )
      )
  )
(add-hook 'comint-input-filter-functions 'rename-buffer-in-ssh-login)
  # 要让这个函数工作，我们需要把它加入到一个 hook 变量 comint-input-filter-functions 当中。

```


#### exit &amp;&amp; after work {#exit-and-and-after-work}

```lisp

  (defun kill-shell-buffer(process event)
    "The one actually kill shell buffer when exit. "
    (kill-buffer (process-buffer process))
  )

;; #  kill-shell-buffer 函数关联到正确的进程上去
  (defun kill-shell-buffer-after-exit()
    "kill shell buffer when exit."
    (set-process-sentinel (get-buffer-process (current-buffer))
                  #'kill-shell-buffer)
  )
(add-hook 'shell-mode-hook 'kill-shell-buffer-after-exit t)

```


#### outline in Shell Mode {#outline-in-shell-mode}

```lisp

Outline-mode 是 GNU Emacs 的一个非常好用的写作模式。使用 outline-mode 可以轻松方便的操作结构化文档.
org-mede based on it.

(setq outline-regexp ".*[bB]ash.*[#\$]")     # 将 Shell 提示符的内容定义为“标题”

M-x outline-minor-mode 就可以进入 outline-mode
- 输入 M-x hide-body 或者 M-x hide-all 命令折叠起 Shell buffer 里的所有命令
- 移动光标到 ls *.el 所在的行
- 使用 M-x show-entry 或者 M-x show-subtree 命令展开 ls *.el 命令

;; NOTE: outline-regexp 变量是一个全局变量，所以对 outline-regexp 的值势必改变其他模式中的 outline-minor-mode 的行为方式
```


#### Enhanced outline in Shell Mode {#enhanced-outline-in-shell-mode}

```lisp

(defun set-outline-minor-mode-regexp ()
    ""
    (let ((find-regexp
           (lambda
             (lst mode)
             ""
             (let
                 ((innerList
                   (car lst)))
               (if innerList
                   (if
                       (string=
                        (car innerList)
                        mode)
                       (car
                        (cdr innerList))
                     (progn
                       (pop lst)
                       (funcall find-regexp lst mode))))))))
      (outline-minor-mode 1)
      (make-local-variable 'outline-regexp)
      (setq outline-regexp (funcall find-regexp outline-minor-mode-list major-mode))))

;; # 要让这个函数能够工作，我们就需要把他加入到各个主模式的 hook 之中
  (add-hook 'shell-mode-hook      'set-outline-minor-mode-regexp t )
  (add-hook 'sh-mode-hook         'set-outline-minor-mode-regexp t )
  (add-hook 'emacs-lisp-mode-hook 'set-outline-minor-mode-regexp t )
  (add-hook 'perl-mode-hook       'set-outline-minor-mode-regexp t )

;; # 需要一个全局变量 outline-minor-mode-list 来存储 set-outline-minor-mode-regexp 函数所需的所有数据。
(setq outline-minor-mode-list
      (list '(emacs-lisp-mode "(defun")
      '(shell-mode ".*[bB]ash.*[#\$] ")
      '(sh-mode "function .*{")
      '(perl-mode "sub ")

      ))

```


#### hook {#hook}

```lisp

;; hook 就是一个存储函数列表的 Lisp 变量，该列表里的每一个函数被称作这个 hook 的一个 hook 函数。

(add-hook 'shell-mode-hook 'outline-minor-mode t)

;; 关于 hook 有几个细节需要注意:

- 绝大多数普通 hook 变量的名称都是在主模式的名称后面加上 -hook 后缀来构成的
- 但是，并不是所有 hook 变量都是这样命名的
- 绝大多数普通 hook 函数被调用的时候是不会向它传递任何参数的，同时也不会理会函数的返回结果的
- 但是，并不是所有 hook 函数都是这样调用的
- 已经装入的 hook 函数将无法通过再次执行 add-hook 来进行覆盖或修改。实际的结果将会装入该 hook 函数的多个版本。
---- 解决的办法之一是清除 hook 变量，然后再次装入：
 (setq 'shell-mode-hook nil)
 (add-hook 'shell-mode-hook 'outline-minor-mode t)

```


### window {#window}


#### 4 windows {#4-windows}

```lisp

(defun split-window-4()
"Splite window into 4 sub-window"
(interactive)
(if (= 1 (length (window-list)))
    (progn (split-window-vertically)
     (split-window-horizontally)
     (other-window 2)
     (split-window-horizontally)
     )
  )
)

(global-set-key (kbd "C-x 4 4"))
```


#### 3 windows rotate {#3-windows-rotate}

```lisp

(defun change-split-type-3 ()
  "Change 3 window style from horizontal to vertical and vice-versa"
  (interactive)

  (select-window (get-largest-window))
  (if (= 3 (length (window-list)))
      (let ((winList (window-list)))
            (let ((1stBuf (window-buffer (car winList)))
                  (2ndBuf (window-buffer (car (cdr winList))))
                  (3rdBuf (window-buffer (car (cdr (cdr winList)))))

                  (split-3
                   (lambda(1stBuf 2ndBuf 3rdBuf split-1 split-2)
                     "change 3 window from horizontal to vertical and vice-versa"
                     (message "%s %s %s" 1stBuf 2ndBuf 3rdBuf)

                     (delete-other-windows)
                     (funcall split-1)
                     (set-window-buffer nil 2ndBuf)
                     (funcall split-2)
                     (set-window-buffer (next-window) 3rdBuf)
                     (other-window 2)
                     (set-window-buffer nil 1stBuf)))

                  (split-type-1 nil)
                  (split-type-2 nil)
                  )
              (if (= (window-width) (frame-width))
                  (setq split-type-1 'split-window-horizontally
                        split-type-2 'split-window-vertically)
                (setq split-type-1 'split-window-vertically
           split-type-2 'split-window-horizontally))
              (funcall split-3 1stBuf 2ndBuf 3rdBuf split-type-1 split-type-2)

 ))))

(global-set-key (kbd "C-x 4 c") (quote change-split-type-3))

```


#### buffer rotate {#buffer-rotate}

```lisp

(defun roll-v-3 (&optional arg)
    "Rolling 3 window buffers (anti-)clockwise"
    (interactive "P")
    (select-window (get-largest-window))
    (if (= 3 (length (window-list)))
        (let ((winList (window-list)))
          (let ((1stWin (car winList))
                (2ndWin (car (cdr winList)))
                (3rdWin (car (last winList))))
            (let ((1stBuf (window-buffer 1stWin))
                  (2ndBuf (window-buffer 2ndWin))
                  (3rdBuf (window-buffer 3rdWin)))
              (if arg (progn
 ; anti-clockwise
                        (set-window-buffer 1stWin 3rdBuf)
                        (set-window-buffer 2ndWin 1stBuf)
                        (set-window-buffer 3rdWin 2ndBuf))
                (progn                                      ; clockwise
                  (set-window-buffer 1stWin 2ndBuf)
                  (set-window-buffer 2ndWin 3rdBuf)
                  (set-window-buffer 3rdWin 1stBuf))
                ))))))

(global-set-key (kbd "C-x 4 r")  (quote roll-v-3))

```


## Org {#org}


### Org-auto-mode {#org-auto-mode}

```lisp

(setq auto-mode-alist
      (append
       '(("\\.js\\'" . js2-mode))
       '(("\\.el\\'" . emacs-lisp-mode))
       '(("\\.org\\'" . org-mode))
       auto-mode-list))

```


### Org-agenda {#org-agenda}

```lisp

org_agenda(){

;; 1 自定义 agenda 模板
(setq org-agenda-custom-commands
        '(												# ; 'importance&urgency
          ("w" . "任务安排")
          ("wa" "重要且紧急的任务" tags-todo "+PRIORITY=\"A\"")
          ("wb" "重要且不紧急的任务" tags-todo "-weekly-monthly-daily+PRIORITY=\"B\"")
          ("wc" "不重要且紧急的任务" tags-todo "+PRIORITY=\"C\"")
          ("W" "Weekly Review"
           ((stuck "") ;; review stuck projects as designated by org-stuck-projects
            (tags-todo "project")
            (tags-todo "daily")
            (tags-todo "weekly")
            (tags-todo "school")
            (tags-todo "code")
            (tags-todo "theory")
            ))
          ))
;; # ("w" . "任务安排") 表示了设置快捷键"w"展示任务安排
;; # ("wa" "重要且紧急的任务" tags-todo "+PRIORITY="A"") 表示设置快捷键 "wa"展示重要且紧急的任务，筛选条件是 优先级等于"A"
;; # ("wb" "重要且不紧急的任务" tags-todo "-weekly-monthly-daily+PRIORITY="B"") 筛选条件是：排除每周、每月、每日标签、且优先级等于 B
;; # ((stuck "") 表示显示尚未进行管理的任务
;; # 下面的"project", "daily"表示展现该类标签下的任务

;; 2 关键词标注
(setq org-todo-keywords
    '((sequence "BUG(b!)" "|" "FIXED(f!)")				;'
      (sequence "TODO(t!)" "SOMEDAY(s)" "|" "DONE(d!)" "CANCELED(c @/!)")
     ))
;; # 可以在 () 中定义附加选项,包括:
;; # 	字符:该状态的快捷键
;; # 	! : 切换到该状态时会自动添加时间戳
;; # 	@ : 切换到该状态时要求输入文字说明
;; # 	如果同时设定@和!,使用@/!
;; # 也可以通过 S-左方向键 和 S-右方向键进行调整，S表示 super 键，即 shift 键
;; 上文中展示了 A B C 三个优先级，你可以通过 S-UP/DOWN 来进行调整
;; # C-c C-s 插入 Schedule 时间， C-c C-t 插入 Deadline 时间, 或者直接 C-c .插入一般时间。

;; # C-c a 进入 org-agenda
;; # a 进入每日、每周任务
;; 默认展示的是一周内每天的任务
;; # 按 d 进入当天任务，按 w 返回每周任务
;; # 按 R (注意大写)查看当天每个任务的完成时间情况
;; # 按 r 刷新状态

;; # w 进入自定义的模板
;; # a 选择优先级为 a 的任务列出
;; # C-c a, wb 选择优先级为 b 的任务列出
;; # C-c a, W (大写)列出所有模板中的代办任务
}

```


### org-beamer {#org-beamer}

<https://www.latexstudio.net/archives/2825.html>


#### documentclass {#documentclass}


#### title {#title}


#### theme {#theme}

```sh

默认的主题如下：

Antibes Bergen Berkeley Berlin
Boadilla Copenhagen Darmstadt Dresden
Frankfurt Goettingen Hannover Ilmenau
Juanlespins Madrid Malmoe Marburg
Montpellier Paloalto Pittsburgh Rochester
Singapore

eg.http://www.ctan.org/tex-archive/macros/latex/contrib/beamer/doc/
```


#### theme-color/inner/outter {#theme-color-inner-outter}

```sh

颜色主题有三种，分别是 colortheme，inner color theme，outter color theme。
- colortheme 控制着全部的颜色，
- inner color theme 控制着帧内一些元素的颜色，主要是 block，
- outter color theme 控制着 headline，footline，sidebar 等元素的颜色。

使用的方法都是一致的。即 \usecolortheme{default}。

Beamer 中的颜色主题：

1. color theme: albatross crane beetle dove fly seagull wolverine beaver
2. inner color: lily orchid rose
3. outter color: whale seahorse dolphin
```


#### usepackage {#usepackage}


#### outline {#outline}


### org-clock {#org-clock}

```lisp

;; 在 todo.org 中，移到一个条目上，按
;; Ctrl-c Ctrl-x Ctrl-i 即可对该条目开始计时，
;; Ctrl-c Ctrl-x Ctrl-o 停止当前计时。
;; 如果在 Agenda 中，移到条目按 I(大写)即可对该条目开始计时，O(大写)即可停止计时。

;; 加前缀(Ctrl-u)再按 Ctrl-c Ctrl-x Ctrl-i，可快速查看最近计时项目，进行快速计时。

;; todo.org 的头部加入了#+PROPERTY: CLOCK_INTO_DRAWER t，这样，时间记录会放到一个名为 LOGBOOK 的抽屉(drawer)中，平时看项目时并不展开，所以记录再多也不影响日常操作。

```


### org-pomodoro {#org-pomodoro}

```lisp

Org_pomodoro (){

# Org-pomodoro 是一个番茄时间工作法的插件
(set-language-environment "UTF-8")
# 当 org-mode 不能生效时，我们需要将与 Org 相关的配置放置于 with-eval-after-load 中，
(with-eval-after-load 'org'
  ;; Org 模式相关设定
  )

---
# pacemacs 自带，将光标移动到接下来要办的事情上，通过
M-x org-pomodoro 启动, 之后你会看到你的 spaceline 上多了一个计时器，好了接下来 25
M-x spaceline-toggle-org-pomodoro-off 关闭番茄计时
# 如果你不想选择番茄计时，而是随意的开始和终止，那么你可以在相应的任务下运行:
C-c C-x C-i 启动时钟（不会在 spaceline 上显示）
C-c C-x C-o 关闭时钟

${调整提示音音量}
(setq org-pomodoro-audio-player "mplayer")
(setq org-pomodoro-finished-sound-args "-volume 0.7")
(setq org-pomodoro-long-break-sound-args "-volume 0.7")
(setq org-pomodoro-short-break-sound-args "-volume 0.7")
(setq org-pomodoro-ticking-sound-args "-volume 0.3")
}

```


### org-remember {#org-remember}

```lisp

org-remember 支持模板，可以通过快捷键选择事件的类型，生成特定格式的记录，并插入到指定容器的指定位置。其格式是： （名称，快捷键，内容模板，文件，父节点）

我的事件定义如下：


事件（快捷键）	容器	模板
New(n)	inbox.org	收件箱，收集未整理的信息
Task(t)	task.org	待办事项，所有未完成的事情
Calendar(c)	task.org	日程安排，具有明确时间的待办实现，可以是周期性任务
Idea(i)	task.org	想法，愿望
Note(r)	note.org	笔记，最终会被移到真正的笔记本
Project(p)	project.org	项目任务
对应的模板配置：
(org-remember-insinuate)
(setq org-directory "~/Documents/Dropbox/0.GTD/")
(setq org-remember-templates '(("New"      ?n "* %? %t \n %i\n %a"   "~/Documents/Dropbox/0.GTD/inbox.org" )
             ("Task"     ?t "** TODO %?\n %i\n %a" "~/Documents/Dropbox/0.GTD/task.org" "Tasks")
             ("Calendar" ?c "** TODO %?\n %i\n %a" "~/Documents/Dropbox/0.GTD/task.org" "Tasks")
             ("Idea"     ?i "** %?\n %i\n %a"      "~/Documents/Dropbox/0.GTD/task.org" "Ideas")
             ("Note"     ?r "* %?\n %i\n %a"       "~/Documents/Dropbox/0.GTD/note.org" )
             ("Project"  ?p "** %?\n %i\n %a"      "~/Documents/Dropbox/0.GTD/project.org" %g) ))
(setq org-default-notes-file (concat org-directory "/inbox.org"))
使用模板参数能带来很多便捷。比如上面的 Project 模板，在收集的时候能够根据选择的项目名称，自动将任务插入到对应项目的条目下面。

常用的模板元素：


元素	说明
%?	输入文字
\n	插入换行符
%i	插入选择区域
%a	当前光标所在标题的链接
%t	插入日期
%T	插入日期和时间
%g	从目标容器的标签中选择
%G	从全局标签中选择
%t	输入日期时间

```


### org-mobile sync {#org-mobile-sync}

good!!!

<https://stackoverflow.com/questions/8432108/how-to-automatically-do-org-mobile-push-org-mobile-pull-in-emacs>


#### startuo &amp;&amp; exit {#startuo-and-and-exit}

```lisp
it automatically pulls the changes on emacs startup, and pushes the changes before emacs exits

(add-hook 'after-init-hook 'org-mobile-pull)
(add-hook 'kill-emacs-hook 'org-mobile-push)
```


#### idle time sync {#idle-time-sync}

```lisp
;; moble sync
(defvar org-mobile-sync-timer nil)
(defvar org-mobile-sync-idle-secs (* 60 10))
(defun org-mobile-sync ()
  (interactive)
  (org-mobile-pull)
  (org-mobile-push))
(defun org-mobile-sync-enable ()
  "enable mobile org idle sync"
  (interactive)
  (setq org-mobile-sync-timer
        (run-with-idle-timer org-mobile-sync-idle-secs t
                             'org-mobile-sync)));
(defun org-mobile-sync-disable ()
  "disable mobile org idle sync"
  (interactive)
  (cancel-timer org-mobile-sync-timer))
(org-mobile-sync-enable)

```


### org-basic {#org-basic}

```lisp

;;lisp 子目录加到 Emacs 的加载路径里
(setq load-path (cons "~/path/to/orgdir/lisp" load-path))
(setq load-path (cons "~/path/to/orgdir/contrib/lisp" load-path))


;; The following lines are always needed. Choose your own keys.
(add-to-list 'auto-mode-alist '("\\.org\\'" . org-mode))
(add-hook 'org-mode-hook 'turn-on-font-lock) ; not needed when global-font-lock-mode is on
(global-set-key "\C-cl" 'org-store-link)
(global-set-key "\C-ca" 'org-agenda)
(global-set-key "\C-cb" 'org-iswitchb)		;'
```

```cfg
${Links}
http://www.astro.uva.nl/~dominik            on the web
file:/home/dominik/images/jupiter.jpg       file, absolute path
/home/dominik/images/jupiter.jpg            same as above
file:papers/last.pdf                        file, relative path
file:projects.org                           another Org file
docview:papers/last.pdf::NNN                open file in doc-view mode at page NNN
id:B7423F4D-2E8A-471B-8810-C40F074717E9     Link to heading by ID
news:comp.emacs                             Usenet link
mailto:adent@galaxy.net                     Mail link
vm:folder                                   VM folder link
vm:folder#id                                VM message link
wl:folder#id                                WANDERLUST message link
mhe:folder#id                               MH-E message link
rmail:folder#id                             RMAIL message link
gnus:group#id                               Gnus article link
bbdb:R.*Stallman                            BBDB link (with regexp)
irc:/irc.com/#emacs/bob                     IRC link
info:org:External%20links                   Info node link (with encoded space)

file:~/code/main.c::255                     进入到 255 行
file:~/xx.org::My Target                    找到目标"<<My Target>>"
file:~/xx.org/::#my-custom-id               查找自定义 id 的项
```


### org-capture {#org-capture}


#### templates {#templates}

```plaintext

#* %^{提示语句}  '#'为注释符号
# 把提示语句提示给用户,并插入用户的输入.
# 你可以定义默认值和可选列表,语法为:{提示语句|默认值|可选值 1|可选值 2...}.
# 可用用方向键来获取输入的历史
#* %a
# 注释,一般来说会根据 org-store-link 定义的值来创建这条链接
#* %A
# 类似于%a, 但是会提示输入链接的描述部分
#* %i
# 若 remember 被调用时用了 C-u 前缀,则会插入 region 的内容.
# 文本的缩进不变.
#* %t
# 插入时间戳,但是只插入日期
#* %T
# 插入时间戳,包括日期和时间
#* %u, %U
# 类似于%t 和%T,但是不会让你有选择时间戳的机会
#* %^t
# 类似%t, 但是会提示输入时间.%^T, %^u, %^U 也类似.你也可用自定义一个提示信息,语法为%^{提示信息}t
#* %n
# 插入用户名(从变量 user-full-name 中获得)
#* %c
# 插入当前 kill ring 最开头部分的内容.
#* %x
# 插入 X 系统粘贴板的内容
#* %^C
# 提供交互功能让用户选择插入那个 kill 或 clip 的内容.
#* %^L
# 类似于%^C, 但是以链接的方式插入.
#* %k
# 插入当前计时任务的标题
#* %K
# 链接到当钱计时任务
#* %^g
# 提示输入 tag,能够自动补完目标文件中定义的 tag
#* %^G
# 提示输入 tag,能够自动补完所有 agenda 文件中的所有 tag
#* %^{prop}p
# 提示用户输入属性 prop 的值
#* %:指定类型的关键字
# 指定信息为特定的链接类型.可选的关键字在后面有列出.
#* %[file]
# 插入 file 的内容
#* %(elisp 表达式)
# 计算 elisp 表达式,并插入计算结果
#* %!
# 补完 template 后,理解保存记录
# (通常情况下需要按 C-c C-c 来触发保存动作,但是这里跳过这一步了)
#* %&
# 保存记录之后,立即跳转到保存的地址
#* %?
# 在完成模板替换之后,鼠标放置在这个位置

```


### org-header {#org-header}


#### 文档元数据 {#文档元数据}

```lisp
#+TITLE:       the title to be shown (default is the buffer name)
#+AUTHOR:      the author (default taken from user-full-name)
#+DATE:        a date, an Org timestamp1, or a format string for format-time-string
#+EMAIL:       his/her email address (default from user-mail-address)
#+DESCRIPTION: the page description, e.g. for the XHTML meta tag
#+KEYWORDS:    the page keywords, e.g. for the XHTML meta tag
#+LANGUAGE:    language for HTML, e.g. ‘en’ (org-export-default-language)
#+TEXT:        Some descriptive text to be inserted at the beginning.
#+TEXT:        Several lines may be given.
#+OPTIONS:     H:2 num:t toc:t \n:nil @:t ::t |:t ^:t f:t TeX:t ...
#+BIND:        lisp-var lisp-val, e.g.: org-export-latex-low-levels itemize
              You need to confirm using these, or configure org-export-allow-BIND
#+LINK_UP:     the ``up'' link of an exported page
#+LINK_HOME:   the ``home'' link of an exported page
#+LATEX_HEADER: extra line(s) for the LaTeX header, like \usepackage{xyz}
#+EXPORT_SELECT_TAGS:   Tags that select a tree for export
#+EXPORT_EXCLUDE_TAGS:  Tags that exclude a tree from export
#+XSLT:        the XSLT stylesheet used by DocBook exporter to generate FO file

#+TAGS: { code(c) theory(t) school(s) easy(e) project(p) }
#+PROPERTY: CLOCK_INTO_DRAWER t     ;; 将所有时间信息放在一个抽屉(:LOGBOOK)中
```


#### 其中#+OPTIONS 是复合的选项： {#其中-plus-options-是复合的选项}

```lisp

H:         set the number of headline levels for export
num:       turn on/off section-numbers
toc:       turn on/off table of contents, or set level limit (integer)
\n:        turn on/off line-break-preservation (DOES NOT WORK)
@:         turn on/off quoted HTML tags
::         turn on/off fixed-width sections
|:         turn on/off tables
^:         turn on/off TeX-like syntax for sub- and superscripts.  If
           you write "^:{}", a_{b} will be interpreted, but
           the simple a_b will be left as it is.
-:         turn on/off conversion of special strings.
f:         turn on/off footnotes like this[1].
todo:      turn on/off inclusion of TODO keywords into exported text
tasks:     turn on/off inclusion of tasks (TODO items), can be nil to remove
           all tasks, todo to remove DONE tasks, or list of kwds to keep
pri:       turn on/off priority cookies
tags:      turn on/off inclusion of tags, may also be not-in-toc
<:         turn on/off inclusion of any time/date stamps like DEADLINES
*:         turn on/off emphasized text (bold, italic, underlined)
TeX:       turn on/off simple TeX macros in plain text
LaTeX:     configure export of LaTeX fragments.  Default auto
skip:      turn on/off skipping the text before the first heading
author:    turn on/off inclusion of author name/email into exported file
email:     turn on/off inclusion of author email into exported file
creator:   turn on/off inclusion of creator info into exported file
timestamp: turn on/off inclusion creation time into exported file
d:         turn on/off inclusion of drawers

```


### org-latex {#org-latex}

```lisp
org_latex(){

(setq org-latex-pdf-process
 '("xelatex -interaction nonstopmode %f"		;'
  "xelatex -interaction nonstopmode %f"))

org-tex

C-c C-c (M-x TeX-command-master) 并选择使用 XeLaTeX 编译
```


### org-link {#org-link}

C-c l 可以在光标所在处创建一个跳转目标点，在需要跳转至该目标的位置输入命令 C-c C-l 可以建立到目标的链接当输入 C-c C-l 命令，光标若处在已经存在的一个链接上的时候，可以编辑改链接。命令 C-c %可以记录当前光标所在位置，当光标移到其他地方后，可以用 C-c &amp;跳转回来。这里的位置记录类似一个 kill-ring，重复输入 C-c %可以记录多个位置，重复输入 C-c &amp;可以连续跳转到之前记录的对应位置上。

插入脚注：C-c C-x f

对于文件链接，可以用::后面增加定位符的方式链接到文件的特定位置。定位符可以是行号或搜索选项。如：

```nil
file:~/code/main.c::255                     进入到 255 行
file:~/xx.org::My Target                    找到目标‘<<My Target>>’
file:~/xx.org/::#my-custom-id               查找自定义 id 的项
```

对于表格和图片，可以在前面增加标题和标签的说明，以方便交叉引用。比如在表格的前面添加：

则在需要的地方可以通过\ref{table1}来引用表格。

\#+end_src


### org-templates {#org-templates}

```lisp

--->init.el
(package-initialize)

(require 'org-install)
(require 'ob-tangle)
(org-babel-load-file (expand-file-name "org-file-name.org" user-emacs-directory))


;; #设置了待办事项的 优先级还有触发键
(setq org-capture-templates
      '(("t" "Todo" entry (file+headline "~/.emacs.d/gtd.org" "工作安排")
         "* TODO [#B] %?\n  %i\n"
         :empty-lines 1)))		;'
;; #我们也可以为其绑定一个快捷键
(global-set-key (kbd "C-c r") 'org-capture)		;'
;; # C-c a 中可以根据提示使用 s 来进行关键字所搜。使用 t 则可以进行代办事项的搜索
(setq org-capture-templates
      '(("t" "Todo" entry (file+headline "~/org/gtd.org" "Tasks")
         "* TODO %?\n  %i\n  %a")
        ("j" "Journal" entry (file+datetree "~/org/journal.org")
         "* %?\nEntered on %U\n  %i\n  %a")))				;'

-----
${1 org-capture 配置}
M-x org-capture		; #(define-key global-map "\C-cc" 'org-capture)
;; 绑定键位
  (define-key global-map "\C-cc" 'org-capture)	; '

;; 这边就是为路径赋值
(defvar org-agenda-dir "" "gtd org files location")
  (setq-default org-agenda-dir "/Path/To/Your/GTD/File/")
  (setq org-agenda-file-note (expand-file-name "notes.org" org-agenda-dir))
  (setq org-agenda-file-task (expand-file-name "task.org" org-agenda-dir))
  (setq org-agenda-file-calendar (expand-file-name "calendar.org" org-agenda-dir))
  (setq org-agenda-file-finished (expand-file-name "finished.org" org-agenda-dir))
  (setq org-agenda-file-canceled (expand-file-name "canceled.org" org-agenda-dir))

;; 添加每次打开时可添加的任务类型
  (setq org-capture-templates
        '(														;'
          ("t" "Todo" entry (file+headline org-agenda-file-task "Work")
           "* TODO [#B] %?\n  %i\n"
           :empty-lines 1)
          ("l" "Tolearn" entry (file+headline org-agenda-file-task "Learning")
           "* TODO [#B] %?\n  %i\n"
           :empty-lines 1)
          ("h" "Toplay" entry (file+headline org-agenda-file-task "Hobbies")
           "* TODO [#C] %?\n  %i\n"
           :empty-lines 1)
          ("o" "Todo_others" entry (file+headline org-agenda-file-task "Others")
           "* TODO [#C] %?\n  %i\n"
           :empty-lines 1)
          ("n" "notes" entry (file+headline org-agenda-file-note "Quick notes")
           "* %?\n  %i\n %U"
           :empty-lines 1)
          ("i" "ideas" entry (file+headline org-agenda-file-note "Quick ideas")
           "* %?\n  %i\n %U"
           :empty-lines 1)
          )
        )
;; 步骤：
;; # C-c c 打开 org-capture
;; # t 新建 TODO 任务
;; # 填写你的任务名称
;; # C-c C-d 增加 Deadline
;; # C-c C-c 确认添加，之后这条任务就出现在了 task.org 之中

${2 转接 org-refile}
;; 绑定键位
  (define-key global-map "\C-cr" 'org-refile)		;'
;; 添加 finished 和 canceled 两个文件路径，并且只转移到一级标题
  (setq org-refile-targets  '((org-agenda-file-finished :maxlevel . 1)		;'
                             (org-agenda-file-canceled :maxlevel . 1)
                             ))
}

```


### org-tags {#org-tags}

对于信息的管理，有分类(category)和标签(tag)两种方式
通常分类是固定的，很少变化，而 tag 随时可以增加。 分类通常表现为树状结构，比较清晰，但是树状结构过于简单，不能表达复杂的信息。


#### 标记 tags {#标记-tags}

```lisp

如果希望文档中的所有标题都具有某些标签，只需要定义文档元数据：
#+FILETAGS: :Peter:Boss:Secret:

更方便的做法是在正文部分用 C-c C-q 或
           直接在标题上用 C-c C-c 创建标签

```


#### 预定义 tags {#预定义-tags}

```lisp

;; 1. 在当前文件头部定义这种方式预定义的标签只能在当前文件中使用。使用#+TAGS 元数据进行标记，如：
#+TAGS: { 桌面(d) 服务器(s) }  编辑器(e) 浏览器(f) 多媒体(m) 压缩(z)

**对标签定义进行修改后，要在标签定义的位置按 C-c C-c 刷新才能生效。**

;; 2. 如果要在所有的.org 文件中生效，需要在 Emacs 配置文件 .emacs 中进行定义：
(setq org-tag-alist '((:startgroup . nil)
                      ("@work . ?w) ("@home" . ?h)
                      ("@tennisclub" . ?t)
                      (:endgroup . nil)
                      ("laptop" . ?l) ("pc" . ?p)))


;; 默认情况下，org 会动态维护一个 Tag 列表，即当前输入的标签若不在列表中，则自动加入列表以供下次补齐使用。
;; 为了使这几种情况（默认列表、文件预设 tags，全局预设 tags）同时生效，需要在文件中增加一个空的 TAGS 定义：

#+TAGS:

```


#### tags 查询 {#tags-查询}

```lisp

快捷键	说明
C-c \	可以用来查找某个 tag 下的所有项目
C-c / m	搜索并按树状结构显示
C-c a m	从所有 agenda file 里建立符合某 tag 的全局性列表

+   和      a+b   同时有这两个标签
-   排除    a-b   有 a 但没有 b
|   或      a|b   有 a 或者有 b
&   和      a&b   同时有 a 和 b，可以用“+”替代

```


#### tags search {#tags-search}

```lisp
org_tags(){

这是要标记的文字     :标记 1:标记 2

KEYS	COMMENT
C-c \	按 tag 搜索标题
C-c / m	搜索并按树状结构显示
C-c a m	按标签搜索多个文件（需要将文件加入全局 agenda)
可以使用逻辑表达式限制条件，更准确灵活的搜索

+     和      a+b     同时有这两个标签
-     排除    a-b     有 a 但没有 b
|     或      a|b     有 a 或者有 b
&     和      a&b     同时有 a 和 b，可以用“+”替代
}

```


### org-timestamps {#org-timestamps}


#### timestamps {#timestamps}

```plaintext

C-c . 插入 timestamps， 但仅插入日期
<2017-09-20 三>
C-c ! 可以插入日期，但不被 Agenda View 识别。
[2017-09-20 三]
C-u C-c . 插入日期和时间
<2017-09-20 三 00:34>
C-u C-c ! 插入日期和时间，但不被 Agenda View 识别。

插入时间时，可以直接输入 15-4-5 12:15 形式的内容来指定时间。

```


#### 周期性任务 {#周期性任务}

```lisp

如前面 habits 设置周期性代办事项 中所示， .+2d/4d 意味着

周期至少为 2 天，至多为 4 天
当任务标记为结束时，重新从 今天 开始记
描述时间周期的符号有三种

+   这个要求必须每次的任务都完成，如果落下，需要补上。比如说交房租
.+  之前未完成的可以忽略，当标记为结束时，从 今天 开始
++  同 .+, 但当标记为结束时，从下个周期开始。比如前面那个例子下个任务会从２天后开始

```


### define view {#define-view}

```lisp
https://www.cnblogs.com/quantumman/p/10808374.html

日程视图的定义需要通过设置变量 org-agenda-custom-commands 来完成。该变量是一个列表，其中的每一项对应一个视图设置。这个视图设置的基本格式为：

 (key desc type match settings files)
各部分的含义如下：

key：当用户执行 org-agenda 命令时，会弹出*Agenda Commands*缓冲区，其中包含了系统默认和用户自定义的日程视图。每个日程视图均对应一个快捷字母。当用户按下这个字母时，则可以进入到相应的视图中查看。这里的 key 则代表快捷字母。

desc：日程视图的说明。

type：日程视图的类型，即用于定义将哪些类型的任务条目收录到该视图中。通常用到的类型有：
agenda：基于日或周的日程。
todo：包含有特定状态关键词的任务条目。
alltodo：所有处于未结束状态的任务条目，即，状态关键词为 org-todo-keywords 设置中竖线之前的。
tags：包含指定标签的条目。
match：用于指定与之前 type 对应的匹配条件。例如，当 type 为 todo 时，match 若为"DONE"，则匹配状态关键词为 DONE 的任务条目。如果没有匹配条件需要定义，则这一项为空字符串。
settings：用于指定匹配时应满足的一系列选项设置。settings 的格式类似用于定义局部变量的 let 形式，即， ((option1 value1) (option2 value2) ...)

常用的选项有：
org-agenda-skip-function：用于设定忽略条件的函数对象。
org-agenda-overriding-header：用于设定日程视图的台头提示信息。
org-agenda-files：这个变量的值是一个字符串列表，用于指定从哪些 Org 文件中提取信息。默认情况是从所有的 Org 文件中提取信息。

files：用于指定当执行了 org-store-agenda-views 命令后需要将日程视图自动导出的文件。可以是 HTML 格式，也可以是纯文本格式。这个功能非常方便：当用户将所有的视图都定义好后，可以定期地直接将其全部导出。既可以放在 HTTP 服务器上统一浏览，也可以在审阅后存档，形成历史记录。

随着日积月累，当用户定义的日程视图比较多时，管理起来就会较为混乱，同时可供绑定的字母快捷键也开始不够用。为此，可以将功能、类别相似的视图归为一组。这个组视图在 org-agenda-custom-commands 中的定义方式为：

 (Group-key . desc)
其中的 Group-key 为一个字母，指定了组的快捷键。

当组定义好了之后，随后便可以定义组内的各个日程视图。每个日程视图的定义与前面所述相同，

 (Group-KeyView-Key desc type match settings files)
只是其 key 为两个字母，第一个字母为 Group-key，第二个字母 View-key 为日程视图自己的快捷捷。当用户执行 org-agenda 时，按下 Group-key 先进入组视图，再按下 View-key 则进入到指定的日程视图中。

```


### statistic view {#statistic-view}

```lisp
https://www.cnblogs.com/quantumman/p/10808374.html
a
* TODO A big task to be handled.                                         :TG:
   :PROPERTIES:
   :COLUMNS:  %75ITEM(Task) %8PRIORITY(Priority) %9TODO(Status) %8EFFORT(Effort){:} %16SCHEDULED %16DEADLINE
   :END:
 ** TODO [#A] Task 1
 ** TODO [#C] Task 2
 ** TODO [#B] Task 3
-----
C-c C-x C-c 得到的列视图模式只是暂时地显示于 Emacs 的缓冲区而无法永久保存。
C-c C-x i  执行 org-insert-columns-dblock 命令。随后 Emacs 提示需要为什么范围的任务节点生成列视图。对此，有如下模式可供选择：
  local：对光标所在节点及子树生成视图。
  global：对整个文件中的标题节点生成视图。
  file:FILENAME：对指定文件生成视图。
  LABEL：对光标所在节点及子树中 ID 属性值为 LABEL 的节点生成视图。
C-c C-c 或 C-c C-x C-u 执行 org-dblock-update  如果节点内容有所变动，更新上述 dynamic block
-----
按快捷键 C-c C-x C-i 执行 org-clock-in 命令，即可对该任务进行计时。
按 C-c C-x C-o 执行 org-clock-out 命令，结束对该任务的计时。
按 C-c C-x C-r 执行 org-clock-report 命令，可对光标当前所在处的任务子树或者整个 Org 文件生成时间统计报告。

```


### latex-usepackage {#latex-usepackage}


#### amssymb 全部数字符号 {#amssymb-全部数字符号}

宏包套件 AMSFonts 中的一个宏包，它定义了 amsfonts 宏包里 msam 和 mabm 字库中全部数学符号的命令。当调用该宏包时，amsfonts 宏包也同时被加载了。


#### amsmath 定理排版 {#amsmath-定理排版}

主要的目的是用来排版数学符号和公式，其中专门有 amsthm 宏包，提供对定理的排版。


#### textcomp 数理和符号货币 {#textcomp-数理和符号货币}

这是 LaTeX 的标准宏包之一，它提供了许多 TS1 编码的可直接在文本中使用的常见数理单位和货币符号。例如命令 \textperthousand 可得到“‰”


#### amscls {#amscls}

提供了美国数学会要求的论文和书籍的格式。


#### biblatex cite 引用 {#biblatex-cite-引用}


#### capt-of  格式化图表标题 {#capt-of-格式化图表标题}

格式化图表标题和子标题


#### fontspac 宏包是最好用的字体设置宏包 {#fontspac-宏包是最好用的字体设置宏包}


#### fancyvrb 与 fvrb-ex {#fancyvrb-与-fvrb-ex}

fancyvrb 宏包提供了方便的命令来设计不同式样的抄录环境。如使用不同的字体，颜色，加入行号，边框等。还可根据不同的条件对抄录的文本使用不同的式样。 fvrb-ex 宏包则利用 fanvyvrb 所提供的命令给出了一个 example 环境，允许在列出包含 TeX 命令的文本的同时将该文本排版。


#### geometry {#geometry}

利用 geometry 可以很方便的设置页面的大小。由于可以自动居中排放页面，自动计算并平衡页面各部分如页眉、页脚、左右边空等的大小，因此只需给出很少的信息就能得到满意的页面。


#### graphicx {#graphicx}

<!--list-separator-->

-  单张图片

<!--list-separator-->

-  两张图片并排


#### grffile – Extended file name support for graphics (legacy package) {#grffile-extended-file-name-support-for-graphics--legacy-package}


#### hyperref {#hyperref}

扩展了 LaTeX 的所有的交叉引用的命令（包括目录，参考文献等）的功能，使其生成各种驱动如 dvips, pdftex 等可识别的 \special 命令，从而得到超文本链接。此外，该宏包还提供了新的命令来支持在文档中加入对外部文档和 Internet 网址的链接。


#### hyphenat 断词 {#hyphenat-断词}

\usepackage[none]{hyphenat}

可以在文档中取消 TeX 自动断词的功能，也可以在某一单词后再恢复这一功能。


#### longtable {#longtable}

如果表格太长，超过了一页时，就可以试试 longtable 宏包所定义的 longtable 环境。


#### listings  源代码高亮 {#listings-源代码高亮}

排版 C, C++, Pascal 等源代码，提供语法加亮显示的功能。


#### overpic {#overpic}

允许直接将 LaTeX 对象放置到 一幅图形上，而不是通过对图形上已有的标记进行替换来实现。overpic 宏包中定义了一个 overpic 环境，它有效地将 picture 环境和 \includegraphics 命令结合起来。 使得 picture 环境的维数和插入的 EPS 图形的维数相同。 这样就可以很容易地把 LaTeX 的命令放到图形上的任何指定位置。同时，还可以在图形上加上标尺以方便定位。参见其所附的两个示例：一（使用绝对位置），二（使用相对位置）。


#### rotfloat 旋转 {#rotfloat-旋转}

将 rotating 宏包和 float 宏包结合起来，通过对 float 宏包所定义的命令加以扩展，可以很方便的定义新的被旋转 90°或 270°的浮动对象。


#### TikZ 强大的绘图宏包 {#tikz-强大的绘图宏包}


#### ulem  强调文本 {#ulem-强调文本}

利用下划线，而不是斜体来 表示强调，而且加下划线的文本部分中可以断行，加上连字符 等等。可以命令\normalem 和\ULforem 来开关这种功能。

另外该宏包还提供了几个更花哨的命令，如：\uline{加下划线}而\uwave{加波浪线}则是在文本下面加上波浪线。 \sout{中间加横线}


#### wrapfig  挂版小图形 {#wrapfig-挂版小图形}

wrapfig 宏包提供了一个 wrapfigure 环境来排版窄小的图形，使得该图形位于文本的一边，并使文本在其边上折行。


#### xcolor {#xcolor}


#### verbatim 抄录和代码打印 {#verbatim-抄录和代码打印}

重新实现了 LaTeX 的 verbatim 和 verbatim\* 环境，并提供了新的环境 comment 和 verbatiminput 来在文挡中加入评论和直接抄录文件。


### newcommand 使用语法如下： {#newcommand-使用语法如下}


### Other {#other}


#### 列目录时，隐藏所有的小节 {#列目录时-隐藏所有的小节}


#### 自动压缩，以显示全部内容 {#自动压缩-以显示全部内容}


#### 在每一节（或小节）前增加目录 {#在每一节-或小节-前增加目录}


#### frametitle 的两种写法 {#frametitle-的两种写法}


## Emms {#emms}


### eg.1 {#eg-dot-1}

```lisp
(add-to-list 'load-path "~/.emacs.d/emms/lisp")
(require 'emms-setup)
(require 'emms-player-vlc)
(emms-standard)
(emms-default-players)
(setq emms-player-vlc-command-name
      "/Applications/VLC.app/Contents/MacOS/VLC")
```


### eg.2 {#eg-dot-2}

```lisp
(setq exec-path (append exec-path '("/usr/local/bin")))
(add-to-list 'load-path "~/.emacs.d/site-lisp/emms/lisp")
(require 'emms-setup)
(require 'emms-player-mplayer)
(emms-standard)
(emms-default-players)
(define-emms-simple-player mplayer '(file url)
     (regexp-opt '(".ogg" ".mp3" ".wav" ".mpg" ".mpeg" ".wmv" ".wma"
        ".mov" ".avi" ".divx" ".ogm" ".asf" ".mkv" "http://" "mms://"
        ".rm" ".rmvb" ".mp4" ".flac" ".vob" ".m4a" ".flv" ".ogv" ".pls"))
     "mplayer" "-slave" "-quiet" "-really-quiet" "-fullscreen")
```


### eg.3 {#eg-dot-3}

```lisp
(require 'general)
(require 'pretty-hydra)
(use-package emms
  :general
  (z-spc-leader-def "e" 'z-music-hydra/body)
  (ranger-mode-map "C-c m" 'emms-play-dired)
  :config
  (require 'emms-setup)
  (emms-standard)
  (emms-history-load)
  (emms-mode-line-disable)
  :pretty-hydra
  (z-music-hydra
   (:color red :quit-key "q")
   ("Playlists"
    (("e" emms)
     ("g" emms-play-directory "open dir")
     ("v" emms-playlist-mode-go "go to current")
     ("m" emms-metaplaylist-mode-go "metaplaylist"))
    "Controls"
    (("n" emms-next "next")
     ("p" emms-previous "previous")
     ("s" emms-shuffle "shuffle"))
    ""
    (("i" emms-mode-line-toggle "song info")
     ;; ("w" emms-pause "pause")
     (define-key emms-playlist-mode-map (kbd "SPC") 'emms-pause)
     ("x" emms-stop "stop"))
    ))
  :custom
  (emms-seek-seconds 5)
  (emms-player-list '(emms-player-mpv))
  (emms-source-file-default-directory "/e:/Recreation/Music/")
  (emms-playlist-buffer-name "*Emms*")
  (emms-source-file-directory-tree-function 'emms-source-file-directory-tree-find)
  (emms-browser-covers 'emms-browser-cache-thumbnail)
  )
```


## Bongo {#bongo}

```lisp
(use-package bongo
  :commands bongo-playlist
 :general
  (:states 'normal
     :keymaps 'bongo-playlist-mode-map
     "<return>" 'bongo-dwim
     "i" 'bongo-insert-file
     "p" 'bongo-play-previous
     "n" 'bongo-play-next
     "w" 'bongo-pause/resume
     "d" 'bongo-dired-line
     "a" 'bongo-append-enqueue
     "s" 'bongo-seek
     "r" 'bongo-rename-line
     "v" 'volume)
  :custom
  (bongo-enabled-backends '(mplayer.exe))
  (bongo-default-directory "e:/Recreation/Music/")
  (bongo-insert-album-covers t)
  (bongo-album-cover-size 100)
  (bongo-mode-line-indicator-mode nil))
```


## Spacemacs {#spacemacs}


### layers {#layers}

```cfg
layers(){
dotspacemacs-configuration-layers 			;;内置的 layer
dotspacemacs-excluded-packages 				;;删除安装的 package
dotspacemacs-additional-package				;;变量,将需要安装的 package 加入
dotspacemacs-themes 						;;变量,将主题加入列表即可. 在列表中靠前的主题会优先使用

# customize-group
  (setq custom-file (expand-file-name "custom.el" dotspacemacs-directory))
  (load custom-file 'no-error 'no-message)
  # 使用 customize-group 对配置进行了修改,
  # 可以以下代码将生成的 custom.el 配置文件纳入 ~/.spacemacs.d 目录中进行统一管理:


1) 每一个 layer 都可以配置一些变量,
# 可以通过 SPC h SPC 然后输入 layer 名称, 点击对应的选项即可打开该 layer 的 README.org 文件.
# 然后按下 SPC f j 进入 dired 模式, 选择 config.el 文件打开, 该文件中即定义了该 layer 的变量.
# 要配置使用这些变量, 可以在启用 layer 时使用如下的代码:
(better-defaults :variables
                 better-defaults-move-to-end-of-code-first t)
}
```


### location {#location}

```lisp
location(){

;; 1) 本地 package
;; 自定义 package 安装地址
(defconst zilongshanren-packages
  '(youdao-dictionary							；'
    (occur-mode :location built-in)
    )
  )
;; 初始化 occur mode
(defun zilongshanren/init-occur-mode ()
  (evilified-state-evilify-map occur-mode-map
    :mode occur-mmode)
  )

;; 2) github
;; 自定义 package 安装地址
(defconst zilongshanren-packages
  '(youdao-dictionary							;'
    (occur-mode :location built-in)
    (gulpjs :location (recipe :fetcher github :repo "zilongshanren/emacs-gulpjs"))
    )
  )

(defun zilongshanren/init-gulpjs ()
  (use-package gulpjs
    :init)
  )
}

```


### BasicOperate {#basicoperate}

```cfg

BasicOperate(){

# 1)Change the Theme in current buffer
    <leader>Ts

  对齐
SPC j = 自动对齐，相当于 beautify
快速翻页 (在 spacemacs 0.1xx 中没测试过)
SPC n , 或 . 或 < 或 > 进入 scrolling transient state 然后重复按 , 或 . 或 < 或 > 即可，
                        按其他键会退出 scrolling transient state , 向上翻一页 . 向下翻一页 < 向上翻半页 > 向下翻半页}
#  macro
qa 开始记录一个叫 a 的宏
q 停止记录
@a 运行宏，接下来如果要重复运行的话，可以用 . 来运行上一个命令}

# 2)CMD
配置文件管理
SPC f e d 快速打开配置文件 .spacemacs
SPC f e R 同步配置文件
SPC q R 重启 emacs

# 3)帮助文档
SPC h d   查看 describe 相关的文档
SPC h d f 查看指定函数的帮助文档
SPC h d b 查看指定快捷键绑定了什么命令
SPC h d v 查看指定变量的帮助文档

# 4)注释  #命令以 c 开头
SPC c l 注释行
SPC c p 注释一段

# 5)emacs 标准键
C-c C-k 关闭文件
[e 将选中行向上移
]e 将选中行向下移

# 6)文件管理
SPC f f 打开文件（夹），相当于 $ open xxx 或 $ cd /path/to/project
SPC / 用合适的搜索工具搜索内容，相当于 $ grep/ack/ag/pt xxx 或 ST / Atom 中的 Ctrl + Shift + f
SPC s c 清除搜索高亮
SPC f R 重命名当前文件
SPC f y 显示当前文件路径并复制

# 7)Buffer
SPC b d 关闭当前 buffer (spacemacs 0.1xx 以后)
SPC SPC 搜索当前文件

# 8)窗口管理
SPC f t 或 SPC p t 用 NeoTree 打开/关闭侧边栏，相当于 ST / Atom 中的 Ctrl(cmd) + k + b
SPC f t 打开当前文件所在的目录
SPC p t 打开当前文件所在的根目录
SPC N 快速切换窗口。在 Spacemacs 中的每个窗口，都可以在窗口左下角看到窗口的编号，通过 SPC N 可以快速的根据编号切换窗口
    SPC 0 光标跳转到侧边栏（NeoTree）中 SPC n(数字) 光标跳转到第 n 个 buffer 中

SPC w s 或 SPC w h 或 SPC w - 水平分割窗口
SPC w v 或 SPC w / 垂直分割窗口
SPC w d 关闭当前窗口 (spacemacs 0.1xx 以后)
SPC w U/J/H/K 将当前窗口移至最左/上/下/右
SPC w w 切换窗口
SPC w = 让窗口长宽协调

Ctl+w j 移动光标到下边的窗口
Ctl+w k 移动光标到上边的窗口
Ctl+w h 移动光标到左边的窗口
Ctl+w l 移动光标到右边的窗口


# 9)项目管理
SPC p f 打开/查找文件
SPC p ' 打开命令行  #'
SPC p $t 在根目录打开命令行
SPC p h 最近编辑文件
SPC p t 打开文件树
SPC p b 当前 project 中查找打开的 buffer
SPC p l 切换到其他的 project 并创建一个新的 layout
SPC p p/l 切换项目
SPC p D 在 dired 中打开项目根目录
SPC p f 在项目中搜索文件名，相当于 ST / Atom 中的 Ctrl + p
SPC p R 在项目中替换字符串，根据提示输入「匹配」和「替换」的字符串，然后输入替换的方式：
    - E 修改刚才输入的「替换」字符串
    - RET 表示不做处理
    - y 表示只替换一处
    - Y 表示替换全部
    - n 或 delete 表示跳过当前匹配项，匹配下一项
    - ^ 表示跳过当前匹配项，匹配上一项
    - , 表示替换当前项，但不移动光标，可和 n 或 ^ 配合使用


# 10)Shell 集成 (必须先配置 Shell layer)
SPC "'" (单引号) 打开/关闭 Shell
C-k 	前一条 shell 命令，相当于在 shell 中按上箭头
C-j 	后一条 shell 命令，相当于在 shell 中按下箭头

# 11)GIT
    Git	            Magit
git init	        SPC g i
git status	        SPC g s
git add	SPC         g s 弹出层选中文件然后按 s
git add currentFile	SPC g S
git commit	        SPC g c c
git push	        SPC g P 按提示操作
git checkout xxx	SPC g C
git checkout -- xxx	SPC g s 弹出层选中文件然后按 u
git log	SPC g l
在 commit 时，我们输入完 commit message 之后，需要按 C-c C-c 来完成 commit 操作，也可以按 C-c C-k 来取消 commit

# 12)VIM
v50G 从当前开始选择到第 50 行
v6k 从当前开始向下选择 6 行
vat 选择 html tag
v/foo 选择到下一个 foo 之前
v?foo 选择到上一个 foo 之后
viw 选中当前词
~ 转换大小写
A 在行末插入
J 将下一行接到本行末尾
. 重复刚才的命令
ea 在当前单词末尾插入
E 停在下一个空白符前
ctrl-r 重做
mx 设定一个叫 x 的记号
'x 或者 \x` 回到 x 记号位置或者回到 x 记号所在行 #'
:marks 列出所有记号
guu 整行变小写
gUU 整行变大写
'' 跳到前一个位置
>aB 缩进一个块
ds> 删除两端的 <>
}

```


### SpaceOperate {#spaceoperate}


#### set-space {#set-space}

```lisp

dotspacemacs-default-font '("Inconsolata_NF"
                            :size 20
                            :weight normal
                            :width normal
                            :powerline-scale 1.1) ;'
```


#### file {#file}

```cfg
files(){
SPC f f		#从当前目录开始查找文件. 在作者的配置中同时启用了 ivy-layer 和 helm-layer, 默认使用的是 helm 来查找文件.
SPC f L		#使用 helm-locate 来在当前系统中查找文件.
SPC f l		#查找文件并使用 literal 的方式来打开文件, 使用 literal 方式打开的文件不会附加编码信息, 例如 utf-8 编码中可能存在的 BOM 头信息, 使用 literal 模式即可以看到 BOM 头.
SPC f h		#查找文件并使用二进制的方式来打开文件, 可以使用 C-c C-c 回到之前的模式.
SPC f o		#使用外部程序打开文件.
SPC f E		#使用 sudo 来编辑文件, 当某些文件是只读的时候可以采用这种方式来编辑文件.
SPC f D		#删除当前的文件和 buffer.
SPC f j		#以当前文件的目录打开 dired buffer.
SPC f r		#使用 ivy 打开最近文件列表.
SPC f R		#重命名当前文件.
SPC f v		#添加 local variables, 可以通过这个功能给项目做一些特殊的设置. 例如按下 SPC f v, 然后选择 add-dir-local-variable, 选择 org-mode, 再选择 org-highlight-links 变量, 此时 emacs 会在当前文件的目录下生成一个 .dir-locals.el 文件, 内容如下:
# ;;; Directory Local Variables
# ;;; For more information see (info "(emacs) Directory Variables")
((org-mode
  (org-highlight-links)))
# 这个文件中的代  码会在当前目录下的所有文件 buffer 中生效.
SPC f y			#拷贝当前文件的全路径.
SPC f a d		#列出最近访问的目录, 使用命令行工具 fasd 实现.
SPC f C d/u		#将当前文件的编码转换为 DOS/UNIX 编码.
SPC f e d		#打开 .spacemacs 或 .spacemacs.d/init.el 文件.
SPC f e i		#打开 .emacs 或 .emacs.d/init.el 文件.
SPC f e l		#打开系统中已经安装的 el 文件.
SPC f c			#复制文件.
SPC f b			#打开标签.
SPC f s/S		#保存当前 buffer 或 所有 buffer
}

```


#### buffer {#buffer}

```cfg
SPC b .		#打开 Buffer Selection Transient State, 在该模式下可以进行更多的操作, 由 hydra 提供.
SPC b b		#切换到已经打开的 buffer.
SPC b d		#关闭一个 buffer.
SPC b f		#在 finder 中打开当前文件, 只在 Mac 系统下生效.
SPC b B/i	#以类似 Dired Mode 的形式打开 buffer 列表, 在这个列表中可以执行和 Dired Mode 类似的操作.
SPC b h		#进入 \*spacemacs\* buffer.
SPC b k		#使用正则表达式来删除 buffer.
SPC b N		#新建一个 buffer.
SPC b m		#删除除当前 buffer 外的所有 buffer.
SPC b R		#使用 emacs 自动备份的文件恢复文件.
SPC b s		#跳转到 scratch buffer.
SPC b w		#关闭/打开 buffer 的 read-only.
SPC b Y		#复制整个 buffer 的内容.
SPC b P		#将剪切板的内容粘贴到整个 buffer.
SPC <tab>	#在当前 buffer 和上一个打开的 buffer 中进行切换

```


#### layout {#layout}

```cfg
SPC l L		#加载 layout 文件
SPC l l		#在 layout 之间切换
SPC l s		#将 layout 保存到文件
SPC l <tab>		#在当前 layout 和上一个 layout 之间切换
SPC l o		#配置 layout
SPC l R		#重命名 layout
SPC l ?		#显示更多的与 layout 相关的命令
```


#### window {#window}

```cfg
SPC w -		#上下拆分窗口
SPC w /		#左右拆分窗口
SPC w .		#示更多的与 window micro state 的相关的命令
SPC w 2/3	#左右显示 2/3 个窗口
SPC w =		#将窗口等分
SPC w b		#切换到 minibuffer
SPC w d		#删除当前窗口
SPC w h/j/k/l	#向 左/下/上/右 移动窗口
SPC w m			#最大化显示当前窗口
SPC W H/J/K/L	#将当前窗口向 左/下/上/右 移动
SPC w u/U		#取消/重置上次操作
SPC w o			#切换到其他 frame
SPC w F			#创建一个新的 frame
SPC w 1/2/3/4	#切换到对应的编号的窗口
SPC w w			#依次切换到其他窗口
SPC w W			#使用字母标识需要跳转的窗口, 并按下字母进行跳转
SPC t g			#将当前显示的窗口与其他窗口进行黄金分割显示
SPC t -			#开启/关闭 将光标始终显示在中心行
```


#### multiple-cursor {#multiple-cursor}

```cfg
- cgn
https://macplay.github.io/posts/vim-bu-xu-yao-duo-guang-biao-bian-ji-gong-neng/

- evil-mc
  g-r-xxx
https://github.com/gabesoft/evil-mc

```


### Org {#org}


#### org-mode {#org-mode}

```cfg
   1)presentation
  touch ***.org
  C-c-e   export menuone
  R-B     broswer to reveal.js html

  2)org-mode
  s    #+begin_src ... #+end_src
  e    #+begin_example ... #+end_example  : 单行的例子以冒号开头
  q    #+begin_quote ... #+end_quote      通常用于引用，与默认格式相比左右都会留出缩进
  v    #+begin_verse ... #+end_verse      默认内容不换行，需要留出空行才能换行
  c    #+begin_center ... #+end_center
  l    #+begin_latex ... #+end_latex
  L    #+latex:
  h    #+begin_html ... #+end_html
  H    #+html:
  a    #+begin_ascii ... #+end_ascii
  A    #+ascii:
  i    #+index: line
  I    #+include: line


   3)parameter
#+begin_src c -n -t -h 7 -w 40
  ...code...
#+end_src
其中：
  c 为所添加的语言
  -n 显示行号
  -t 清除格式
  -h 7 设置高度为 7 -w 40 设置宽度为 40
以‘#‘开头的行被看作注释，不会被导出区块注释采用如下写法：

#+BEGIN_COMMENT
  块注释
  ...
#+END_COMMENT

}

```


#### customize {#customize}

M-x customize-group 后选择对应的插件名称，可以进入可视化选项区对指定的插 件做自定义设置。

当选择 Save for future session 后，刚刚做的设计就会被保存在你的 配置文件（ init.el ）中。


#### config {#config}

```lisp
;; 添加 Org-mode 文本内语法高亮
(require 'org)								;'
(setq org-src-fontify-natively t)

;; 设置默认 Org Agenda 文件目录
(setq org-agenda-files '("~/org"))			;'

;; 设置 org-agenda 打开快捷键
(global-set-key (kbd "C-c a") 'org-agenda)	;'

C-c . 		插入当前日期
C-u C-c . 	插入当前日期和时间
C-c C-s 	选择想要开始的时间
C-c C-d 	选择想要结束的时间
C-c a 		可以打开 Agenda 模式菜单并选择不同的可视方式（ r ）

```


#### fcit {#fcit}

```lisp
  spacemacs/chinese layer
  (chinese :variables chinese-enable-fcitx t )
  ;; 或者
fcitx.el - Better fcitx integration for Emacs.
```