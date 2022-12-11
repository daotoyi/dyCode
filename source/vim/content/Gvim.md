+++
lastmod = "2022-12-11 12:20:36"
categories = ["Python"]
draft = false
toc = true
+++

## Gvim {#gvim}


### gvimmode {#gvimmode}

```sh
gvim.exe -y		# insert mode ,cannot normal mode
gvim.exe -R		# ReadOnly
```


### Question {#question}

```sh
# 1)windows, Vundle: PlugnInstatll #“git 不是内部或外部命令”或者“缺少某一个 lib”
C:\Program Files (x86)\Git\libexec\git-core;
C:\Program Files (x86)\Git\bin;
reboot

:echo &rtp	#rtp 就是 RuntimePath，vim 的运行时路径，插件、脚本搜索就是检查的这个

# 2)vindle 版本问题
vundle 新版和旧版还是差的比较多的。旧版：vundle#rc()、Bundle；新版：vundle#begin()、Plugin；
旧版：https://github.com/gmarik/vundle.git
新版：https://github.com/VundleVim/Vundle.vim
:echo globpath(&rtp, 'autoload/vundle.vim') 在 vim 中执行这个看看，如果能看到多个路径，那就是旧版的

```


### basic {#basic}

```sh
:set ic		#不区分大小写
:set noic
:so $MYVIMRC 或者 :source ~/.vimrc 或者 ~/.vimrc 任一命令重载

:{作用范围}s/{目标}/{替换}/{替换的标志}		#当前行、全文、选区
:%s/zempty/handsome/g						#全文
:n1,n2s/zempty/handsome/g					#n1-n2 之间行
:'<,'>s/zempty/handsome/g					#可视模式 (Visual-mode) 下选区中的替换操作


${替换的标志}
  g  			== global
  空 			== 光标位置第一个
  handsome	== 当前行
  i/I			== 大小写不敏感，敏感
  gi			== global&&不区分大小写
  gc			== c 表示需要确认

:!command		#Linux 命令
:r !command		#添加执行结果到光标处

删除行尾的^M
：%s/\r//g
```


### basic-operate {#basic-operate}

```cfg
#all page:
Ctrl + f 键 f 的英文全拼为：forward；
Ctrl + b 键 b 的英文全拼为：backWord

#half page:
Ctrl + d 键 d 的英文全拼为：down；
Ctrl + u 键 u 的英文全拼为：up；

w 移至次一个字（word）字首。当然是指英文单字。
W 同上，但会忽略一些标点符号。
e 移至前一个字字尾。
E 同上，但会忽略一些标点符号。
b 移至前一个字字首。
B 同上，但会忽略一些标点符号。
H 移至萤幕顶第一个非空白字元。
M 移至萤幕中间第一个非空白字元。
L 移至萤幕底第一个非空白字元。

#特殊移动
) 移至下一个句子（sentence）首。
( 移至上一个句子（sentence）首。
} 移至下一个段落（paragraph）首。
{ 移至上一个段落（paragraph）首。
  sentence 是以 . ! ? 为区格。
  paragraph 是以空白行为区格。
% 这是匹配 {}，[]，() 用的
  例如您的游标现在在 { 上，只要按 %，就会跑到相匹配的 } 上。写程序时很好用的

```


### env_Vim {#env-vim}

```sh
# 1)$VIM 被用来确定 Vim 中不同的用户文件的位置，比如用户启动脚本“.vimrc”;允许每个使用者需要时修改$VIM 环境变量
setenv VIM /home/paul/vim
:let $VIM = "/home/paul/vim/"

# 2)$VIMRUNTIME 用来找出各种支持文件，像在线文档和文件使用语法高亮一样。
:let $VIMRUNTIME = "/home/piet/vim/vim54"

# 3)$HOME
# 使用"~"就如同使用"$HOME",但它只能在选项开始之前和空格或逗号后面使用。
:set path=~mool/include,/usr/include
# ${注意}：扩充环境变量和"~/"仅用":set"命令，而不是":let"命令


git config --global http.proxy
git config --global --unset https.proxy

```


## Auto_install {#auto-install}

```sh
let hasVundle=1
let vundle_readme=expand('~/.vim/bundle/vundle/README.md')
if !filereadable(vundle_readme)
    echo "Installing Vundle..."
    echo ""
    silent !mkdir -p ~/.vim/bundle
    silent !git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/vundle
    let hasVundle=0
endif

set rtp+=~/.vim/bundle/vundle/
call vundle#rc()

# 这里配置你的插件列表 xxx

if hasVundle == 0
    echo "Installing Plugins, please ignore key map error messages"
    echo ""
    :PluginInstall
endif
```


### vim_plug {#vim-plug}

```sh

# 1)vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

cd vim-plug/
cp plug.vim ~/vimfiles/autoload/plug.vim	#这个只对当前用户生效
cp plug.vim $VIM/vim8.2/autoload/plug.vim	#对所有用户生效

cat .vimrc << EOF

call plug#begin('~/.vim/plugged')

" Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
Plug 'junegunn/vim-easy-align'

Plug 'https://github.com/junegunn/vim-github-dashboard.git'

Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" On-demand loading
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Using a non-default branch
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug '~/my-prototype-plugin'

" Initialize plugin system
call plug#end()

EOF

Plug 'junegunn/vim-easy-align'
Plug 'https://github.com/junegunn/vim-github-dashboard.git'
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }
Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug '~/my-prototype-plugin'
```


### Pathogen {#pathogen}

```sh

# 2)Pathogen
mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
cat .vimrc << EOF
call pathogen#infect()	#.vimrc 文件中 filetype plugin indent on 之前的任何地方添加
  #execute pathogen#infect()
syntax on
filetype plugin indent on

EOF
#需要手动安装、更新、卸载插件

${安装卸载}
# 1）在当前用户目录~/.vim/下新建 bundle 目录，将新安装插件放到该目录下后，Pathogen 会自动在 bundle 目录下生成对应插件子目录并使该插件生效。
# 2）而如果需要卸载插件，只需把~/.vim/bundle 目录下对应的插件目录删除即可


```


### vundle {#vundle}

```sh

# 3)vundle
cat .vimrc << EOF
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" let Vundle manage Vundle, required
Plugin 'gmarik/Vundle.vim'

" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'

" more Plugin commands
" ...
call vundle#end()            " required
filetype plugin indent on    " required

EOF

cat vundle/git-help << EOF
" Keep Plugin commands between vundle#begin/end.

" plugin on GitHub repo	#格式为 Plugin '用户名/插件仓库名'
" Plugin 'tpope/vim-fugitive'

" plugin from http://vim-scripts.org/vim/scripts.html	#来自 http://vim-scripts.org/vim/scripts.html 的插件
" Plugin 'L9'		#Plugin '插件名称' 实际上是 Plugin 'vim-scripts/插件仓库名' 只是此处的用户名可以省略

" Git plugin not hosted on GitHub	#由 Git 支持但不再 github 上的插件仓库 Plugin 'git clone 后面的地址
"Plugin 'git://git.wincent.com/command-t.git'

" git repos on your local machine (i.e. when working on your own plugin)
"	#本地的 Git 仓库(例如自己的插件) Plugin 'file:///+本地插件仓库绝对路径'
"Plugin 'file:///home/gmarik/path/to/plugin'

" The sparkup vim script is in a subdirectory of this repo called vim." Pass the path to set the runtimepath properly.
"	#插件在仓库的子目录中.正确指定路径用以设置 runtimepath. 以下范例插件在 sparkup/vim 目录下
" Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}

" Install L9 and avoid a Naming conflict if you've already installed a different version somewhere else.
"	#安装 L9，如果已经安装过这个插件，可利用以下格式避免命名冲突
" Plugin 'ascenator/L9', {'name': 'newL9'}

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required

" To ignore plugin indent changes, instead use:	#忽视插件改变缩进,可以使用以下替代:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ

EOF

${
在 Github 上 vim-scripts 用户下的仓库,只需要写出 repos（仓库）名称
在 Github 其他用户下的 repos, 需要写出"用户名/repos 名"
不在 Github 上的插件，需要写出 git 全路径}

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.

 ---1)plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
plugin from http://vim-scripts.org/vim/scripts.html
Plugin 'L9'

---2)Git plugin not hosted on GitHub
Plugin 'git://git.wincent.com/command-t.git'

---3)git repos on your local machine (i.e. when working on your own plugin)
Plugin 'file:///home/gmarik/path/to/plugin'

 The sparkup vim script is in a subdirectory of this repo called vim.
 Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}

 Install L9 and avoid a Naming conflict if you've already installed a different version somewhere else.
 Plugin 'ascenator/L9', {'name': 'newL9'}
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

 Brief help
 :PluginList       - lists configured plugins
 :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
 :PluginSearch foo - searches for foo; append `!` to refresh local cache
 :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal

 see :h vundle for more details or wiki for FAQ
 Put your non-Plugin stuff after this line'

```


## Config {#config}


### AutoSetTitle {#autosettitle}


#### model {#model}

```sh
# 1)modle
# "新建.c,.h,.sh,.java 文件，自动插入文件头 "
autocmd BufNewFile *.cpp,*.[ch],*.sh,*.java exec ":call SetTitle()"
# "定义函数 SetTitle，自动插入文件头"
func SetTitle()
    if &filetype == 'sh'
        call setline(1,"\#########################################################################")
        call append(line("."), "\# File Name: ".expand("%"))
        call append(line(".")+1, "\# Author: ma6174")
        call append(line(".")+2, "\# mail: ma6174@163.com")
        call append(line(".")+3, "\# Created Time: ".strftime("%c"))
        call append(line(".")+4, "\#########################################################################")
        call append(line(".")+5, "\#!/bin/bash")
        call append(line(".")+6, "")
    else
        call setline(1, "/*************************************************************************")
        call append(line("."), "    > File Name: ".expand("%"))
        call append(line(".")+1, "    > Author: ma6174")
        call append(line(".")+2, "    > Mail: ma6174@163.com ")
        call append(line(".")+3, "    > Created Time: ".strftime("%c"))
        call append(line(".")+4, " ************************************************************************/")
        call append(line(".")+5, "")
    endif
    if &filetype == 'cpp'
        call append(line(".")+6, "#include<iostream>")
        call append(line(".")+7, "using namespace std;")
        call append(line(".")+8, "")
    endif
    if &filetype == 'c'
        call append(line(".")+6, "#include<stdio.h>")
        call append(line(".")+7, "")
    endif
    autocmd BufNewFile * normal G	"新建文件后，自动定位到文件末尾"
    endfunc
```


#### model {#model}

```sh
# 2)model
autocmd BufNewFile *.sh,*.py exec ":call AutoSetFileHead()"
function! AutoSetFileHead()
    "对于 .sh 文件 "
    if &filetype == 'sh'
        call setline(1, "#!/bin/bash")
    endif

    "对于 python3 文件 "
    if &filetype == 'python'
        call setline(1, "#!/usr/bin/env python3")
        call append(1, "# Author: ")
        call append(2, "# Email: shark@126.com")
    endif

    normal G
    normal o
    normal o
endfunc
```


### Keyman {#keyman}

```cfg
nnoremap <F2> :g/^\s*$/d<CR> 		"去空行 "
nnoremap <C-F2> :vert diffsplit	 	"比较文件  "
map <M-F2> :tabnew<CR>  			"新建标签 "
map <F3> :tabnew .<CR>  			"列出当前目录文件 "
map <C-F3> \be  					"打开树状文件目录  "

map <F5> :call CompileRunGcc()<CR>	"C，C++ 按 F5 编译运行"
func! CompileRunGcc()
    exec "w"
    if &filetype == 'c'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'cpp'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'java'
        exec "!javac %"
        exec "!java %<"
    elseif &filetype == 'sh'
        :!./%
    endif
endfunc
# "C,C++的调试"
map <F8> :call Rungdb()<CR>
func! Rungdb()
    exec "w"
    exec "!g++ % -g -o %<"
    exec "!gdb ./%<"
endfunc

```


### number {#number}

```sh
number(){
" auto show number when Enter Insert,relativenumber when leave Insert "
set nu
augroup relative_numbser
 autocmd!
 autocmd InsertEnter * :set norelativenumber
 autocmd InsertLeave * :set relativenumber
 augroup END
```


## Plugin {#plugin}

```cfg
[1]: https://github.com/junegunn/vim-plug
[2]: https://github.com/altercation/vim-colors-solarized
[3]: https://github.com/Anthony25/gnome-terminal-colors-solarized
[4]: https://github.com/scrooloose/nerdtree
[5]: https://github.com/jistr/vim-nerdtree-tabs
[6]: https://github.com/Xuyuanp/nerdtree-git-plugin
[7]: https://github.com/Valloric/YouCompleteMe
[8]: https://github.com/Raimondi/delimitMate
[9]: https://github.com/Shougo/deoplete.nvim
[10]: https://github.com/w0rp/ale
[11]: https://github.com/sheerun/vim-polyglot
[12]: https://github.com/kien/ctrlp.vim
[13]: https://github.com/ggreer/the_silver_searcher
[14]: https://github.com/rking/ag.vim
[15]: https://github.com/vim-airline/vim-airline
[16]: https://github.com/vim-airline/vim-airline-themes
[17]: https://github.com/scrooloose/nerdcommenter
[18]: https://github.com/airblade/vim-gitgutter
[19]: https://github.com/tpope/vim-fugitive
[20]: https://github.com/suan/vim-instant-markdown
[21]: https://github.com/mattn/emmet-vim
[22]: https://github.com/othree/html5.vim
[23]: https://github.com/hail2u/vim-css3-syntax
[24]: https://github.com/ap/vim-css-color
[25]: https://github.com/pangloss/vim-javascript
[26]: https://github.com/mxw/vim-jsx
[27]: https://github.com/prettier/vim-prettier
[28]: https://github.com/FengShangWuQi/to-vim/blob/master/.vimrc

      https://github.com/lervag/vimtex
```


### ctags {#ctags}

```cfg
--exclude=lex.yy.cc	#ctags 不要扫描名字是这样的文件 cu
(shell command) ctags *.c
(ex command) :tag
(ex command) :set tags=./tags, ./../tags, ./*/tags

```


### taglist {#taglist}

```cfg

ctags --languages=c --langmap=c:+.ec:+.h -R
ctags -R *

${Q:Taglist: Failed to generate tags for}
taglist 只支持 exuberant ctags tool,不支持 GNU　ctags 或 UNIX ctags,mac 下自带的不是 exuberant　ctags,\
所以就会有问题了,解决办法也很简单,下载 exuberant ctags tool,然后装在一个与系统自带的 ctags 不冲突的路径下,\
然后在.vimrc 里加一行 let Tlist_Ctags_Cmd = '/path/to/ctags'就可以了

require ctags:
#ctags.exe 拷贝到 VIM 安装目录中的与 vim.exe 同级的文件夹中

 8.3 式文件名
==================================================
set tags=tags;
set autochdir

${let Tlist_Ctags_Cmd = 'E:/daoyi~1/ctags'} "#" 8.3 文件格式

if MySys() == "windows"                "设定 windows 系统中 ctags 程序的位置;配置该插件所依赖的 ctags 程序的路径"
  let Tlist_Ctags_Cmd = 'ctags'
elseif MySys() == "linux"              "设定 linux 系统中 ctags 程序的位置"
  let Tlist_Ctags_Cmd = '/usr/bin/ctags'
endif
let Tlist_Show_One_File = 1            "不同时显示多个文件的 tag，只显示当前文件的"
let Tlist_Exit_OnlyWindow = 1          "如果 taglist 窗口是最后一个窗口，则退出 vim"
let Tlist_File_Fold_Auto_Close = 1		"在切换 buffer 的时候折叠之前的符号列表"
let Tlist_Use_Right_Window = 1         "在右侧窗口中显示 taglist 窗口 "
let Tlist_Auto_Open = 1 				  "启动 VIM 时候自动启动 taglist 窗口"
let Tlist_WinWidth = 16
let Tlist_Inc_Winwidth= 0 						设置为 0 表示不增加 Taglist 窗口的默认宽度。

set ignorecase smartcase    " 搜索时忽略大小写，但在有一个或以上大写字母时仍保持对大小写敏感 "

Plugin 'taglist.vim'
let Tlist_Ctags_Cmd='ctags'
noremap <F8> :TlistToggle<CR>

:TlistToggle/:Tlist			控制 taglist 窗口的打开和关闭

```


### netrw_taglist {#netrw-taglist}

```cfg

" =================== netrw =========================
let g:netrw_browse_split = 3	"0: split 1:vsplit 2:new tab 3:pri windows
let g:netrw_liststyle = 3	"4 model, thin/long/wide/tree
let g:netrw_banner = 1		"bannre on top, <l>l r
let g:netrw_winsize = 25	"width 25%
"let g:netrw_sort_by = 'time'
"let g:netrw_sort_direction = 'reverse'

" ================= winmanager =======================
" ================ taglist && netrw ==================
"let g:winManagerWindowLayout = "FileExplorer|TagList"
let g:winManagerWidth = 30
let g:defaultExplorer = 0
nmap <C-W><C-F> :FirstExplorerWindow<cr>
nmap <C-W><C-B> :BottomExplorerWindow<cr>
nmap <silent> <leader>wm :WMToggle<cr>

let g:winManagerWindowLayout='FileExplorer|TagList'
nmap wm :WMToggle<cr>
let g:winManagerWindowLayout = "BufExplorer,FileExplorer|TagList"
  #变量 g:winManagerWindowLayout 中，使用”,”分隔的插件，在同一个窗口中显示，\
  使用”CTRL-N“在不同插件间切换；使用”|”分隔的插件，则在另外一个窗口中显示。

```


### NERD_Tree {#nerd-tree}

```cfg

Plugin 'scrooloose/nerdtree'
map <F7> :NERDTreeToggle<CR>

#" 关闭 NERDTree 快捷键"
map <leader>t :NERDTreeToggle<CR>
" 显示行号"
let NERDTreeShowLineNumbers=1
let NERDTreeAutoCenter=1
" 是否显示隐藏文件"
let NERDTreeShowHidden=1
" 设置宽度"
let NERDTreeWinSize=21
" 在终端启动 vim 时，共享 NERDTree"
let g:nerdtree_tabs_open_on_console_startup=1
" 忽略一下文件的显示"
let NERDTreeIgnore=['\.pyc','\~$','\.swp']
" 显示书签列表"
let NERDTreeShowBookmarks=1

" 不显示隐藏文件
let g:NERDTreeHidden=0
" 过滤: 所有指定文件和文件夹不显示
let NERDTreeIgnore = ['\.pyc$', '\.swp', '\.swo', '\.vscode', '__pycache__']

```


### NerdTree {#nerdtree}

```cfg

" <Nerdtree>-------------------{
    ">> Basic settings
        let g:NERDTreeChDirMode = 2  "Change current folder as root
        autocmd BufEnter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) |cd %:p:h |endif

    ">> UI settings
        let NERDTreeQuitOnOpen=1   " Close NERDtree when files was opened"
        let NERDTreeMinimalUI=1    " Start NERDTree in minimal UI mode (No help lines)"
        let NERDTreeDirArrows=1    " Display arrows instead of ascii art in NERDTree"
        let NERDTreeChDirMode=2    " Change current working directory based on root directory in NERDTree"
        let g:NERDTreeHidden=1     " Don't show hidden files"
        let NERDTreeWinSize=30     " Initial NERDTree width"
        let NERDTreeAutoDeleteBuffer = 1  " Auto delete buffer deleted with NerdTree"
        let NERDTreeShowBookmarks=0   " Show NERDTree bookmarks"
        let NERDTreeIgnore = ['\.pyc$', '\.swp', '\.swo', '__pycache__']   " Hide temp files in NERDTree"
        let g:NERDTreeShowLineNumbers=1  " Show Line Number"

    " Open Nerdtree when there's no file opened"
        autocmd vimenter * if !argc()|NERDTree|endif
    " Or, auto-open Nerdtree"
        autocmd vimenter * NERDTree
    " Close NERDTree when there's no other windows"
        autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
    " Customize icons on Nerdtree"
        let g:NERDTreeDirArrowExpandable = '▸'
        let g:NERDTreeDirArrowCollapsible = '▾'

    ">> NERDTREE-GIT
        " Special characters
    let g:NERDTreeIndicatorMapCustom = {
        \ "Modified"  : "✹",
        \ "Staged"    : "✚",
        \ "Untracked" : "✭",
        \ "Renamed"   : "➜",
        \ "Unmerged"  : "═",
        \ "Deleted"   : "✖",
        \ "Dirty"     : "✗",
        \ "Clean"     : "✔︎",
        \ 'Ignored'   : '☒',
        \ "Unknown"   : "?"

    ">> NERDTree-Tabs
        "let g:nerdtree_tabs_open_on_console_startup=1 "Auto-open Nerdtree-tabs on VIM enter
    ">> Nerdtree-devicons
        "set guifont=DroidSansMono_Nerd_Font:h11
    ">> Nerdtree-syntax-highlighting
        "let g:NERDTreeDisableFileExtensionHighlight = 1
        "let g:NERDTreeDisableExactMatchHighlight = 1
        "let g:NERDTreeDisablePatternMatchHighlight = 1
        "let g:NERDTreeFileExtensionHighlightFullName = 1
        "let g:NERDTreeExactMatchHighlightFullName = 1
        "let g:NERDTreePatternMatchHighlightFullName = 1
        "let g:NERDTreeHighlightFolders = 1 " enables folder icon highlighting using exact match
        "let g:NERDTreeHighlightFoldersFullName = 1 " highlights the folder name
        "let g:NERDTreeExtensionHighlightColor = {} " this line is needed to avoid error
" }

#"
}

```


### nerdcommenter {#nerdcommenter}

```cfg

Plug 'scrooloose/nerdcommenter'

# <leader>cc // 注释
# <leader>cm 只用一组符号注释
# <leader>cA 在行尾添加注释
# <leader>c$ /* 注释 */
# <leader>cs /* 块注释 */
# <leader>cy 注释并复制
# <leader>c<space> 注释/取消注释
# <leader>ca 切换　// 和 /* */
# <leader>cu 取消注释

let g:NERDSpaceDelims = 1
let g:NERDDefaultAlign = 'left'
let g:NERDCustomDelimiters = {
            \ 'javascript': { 'left': '//', 'leftAlt': '/**', 'rightAlt': '*/' },
            \ 'less': { 'left': '/**', 'right': '*/' }
        \ }

-----

# " Create default mappings
let g:NERDCreateDefaultMappings = 1

# " Add spaces after comment delimiters by default
let g:NERDSpaceDelims = 1

# " Use compact syntax for prettified multi-line comments
let g:NERDCompactSexyComs = 1

# " Align line-wise comment delimiters flush left instead of following code indentation
let g:NERDDefaultAlign = 'left'

# " Set a language to use its alternate delimiters by default
let g:NERDAltDelims_java = 1

# " Add your own custom formats or override the defaults
let g:NERDCustomDelimiters = { 'c': { 'left': '/**','right': '*/' } }

# " Allow commenting and inverting empty lines (useful when commenting a region)
let g:NERDCommentEmptyLines = 1

# " Enable trimming of trailing whitespace when uncommenting
let g:NERDTrimTrailingWhitespace = 1

# " Enable NERDCommenterToggle to check all selected lines is commented or not
let g:NERDToggleCheckAllLines = 1

```


### vim0devicons {#vim0devicons}

```cfg

安装 Nerd Font 字体，网址在此。安装字体的方法每个电脑系统不一样。因为全部字体多到 3G，
  所以最快到方法是到官网首页点击 Download，下载 Droid Sans Mono Nerd 这个字体，8M 左右，下载好了
  如果是 Mac 的话，就选择压缩包里的 Droid Sans Mono Nerd Font Complete.otf，双击安装。
在 Terminal.app 或 iTerm2 的系统设置里，设置字体为 Droid Sans Mono Nerd。
在~/.vimrc 中插件管理处加入 Plugin 'ryanoasis/vim-devicons'，重启 vim 然后:PluginInstall 进行下载安装。
在~/.vimrc 中配置默认编码 set encoding=utf8 和默认字体 set guifont=DroidSansMono_Nerd_Font:h11

```


### winmanager {#winmanager}

```cfg
Winmanager(){

let g:NERDTree_title="[NERDTree]"
let g:winManagerWindowLayout="NERDTree|TagList"

#打开 Winmanager 界面时，会同时打开一个空的文件。这会影响后续使用，所以我们要在打开 Winmanager 时关掉这个空文件。
#.vim/plugin 目录下的 winmanager.vim 文件中找到以下函数定义并在第 5 行下添加第 6 行的内容：  exe 'q'
#在~/.vim/plugin 目录下的 winmanager.vim 文件中找到以下函数定义并在第 5 行下添加第 6 行的内容：
function! <SID>ToggleWindowsManager()
    if IsWinManagerVisible()
        call s:CloseWindowsManager()
    else
        call s:StartWindowsManager()
        exe '1wincmd w'
        exe 'q'
    end
endfunction

let g:AutoOpenWinManager = 1
${vim/plugin/winmanager.vim}文件，加入
if g:AutoOpenWinManager 	"set auto open Winmanager"
    autocmd VimEnter * nested  call s:StartWindowsManager()|'q'|4wincmd w
  #’q’解决出现空白窗口现象，后面 4wincmd w 表示模拟 4 次 w 按键使光标自动跳转到打开的文件，而不是 Nerdtree 或者 Tagbar 窗口。
endif


${~/.vimrc}文件
autocmd bufenter * if (winnr("$") == 2 && exists("b:NERDTreeType") &&b:NERDTreeType == "primary")  | qa | endif	#"自动退出 Winmanager

}

Supertab(){
let g:SuperTabDefaultCompletionType="<C-X><C-O>"
  " 设置按下<Tab>后默认的补全方式, 默认是<C-P>,"" 现在改为<C-X><C-O>. 关于<C-P>的补全方式"
其他的补全方式, 你可以看看下面的一些帮助:
:help ins-completion
:help compl-omni

let g:SuperTabRetainCompletionType=2
  #" 0 - 不记录上次的补全方式"
  #" 1 - 记住上次的补全方式,直到用其他的补全命令改变它"
  #" 2 - 记住上次的补全方式,直到按 ESC 退出插入模式为止"
}

```


### omnicppcomplete {#omnicppcomplete}

```cfg
let OmniCpp_NamespaceSearch = 1
let OmniCpp_GlobalScopeSearch = 1
let OmniCpp_ShowAccess = 1
let OmniCpp_ShowPrototypeInAbbr = 1 " 显示函数参数列表"
let OmniCpp_MayCompleteDot = 1   " 输入 .  后自动补全"
let OmniCpp_MayCompleteArrow = 1 " 输入 -> 后自动补全"
let OmniCpp_MayCompleteScope = 1 " 输入 :: 后自动补全"
let OmniCpp_DefaultNamespaces = ["std", "_GLIBCXX_STD"]
au CursorMovedI,InsertLeave * if pumvisible() == 0|silent! pclose|endif" 自动关闭补全窗口"
set completeopt=menuone,menu,longest
```


### fzf {#fzf}

```cfg
"<Leader>f 在当前目录搜索文件"
nnoremap <silent> <Leader>f :Files<CR>
"<Leader>b 切换 Buffer 中的文件"
nnoremap <silent> <Leader>b :Buffers<CR>
"<Leader>p 在当前所有加载的 Buffer 中搜索包含目标词的所有行，:BLines 只在当前 Buffer 中搜索"
nnoremap <silent> <Leader>p :Lines<CR>
"<Leader>h 在 Vim 打开的历史文件中搜索，相当于是在 MRU 中搜索，:History：命令历史查找"
nnoremap <silent> <Leader>h :History<CR>
"调用 Rg 进行搜索，包含隐藏文件"
command! -bang -nargs=* Rg
  \ call fzf#vim#grep(
  \   'rg --column --line-number --no-heading --color=always --smart-case --hidden '.shellescape(<q-args>), 1,
  \   <bang>0 ? fzf#vim#with_preview('up:60%')
  \           : fzf#vim#with_preview('right:50%:hidden', '?'),
  \   <bang>0)
```


### Bufexplorer {#bufexplorer}

```cfg
let g:miniBufExplMapWindowNavVim = 1
let g:miniBufExplMapWindowNavArrows = 1
let g:miniBufExplMapCTabSwitchBufs = 1
let g:miniBufExplModSelTarget = 1
let g:miniBufExplMoreThanOne=0

let g:bufExplorerDefaultHelp=0       " Do not show default help."
let g:bufExplorerShowRelativePath=1  " Show relative paths."
let g:bufExplorerSortBy='mru'        " Sort by most recently used."
let g:bufExplorerSplitRight=0        " Split left."
let g:bufExplorerSplitVertical=1     " Split vertically."
let g:bufExplorerSplitVertSize = 30  " Split width"
let g:bufExplorerUseCurrentWindow=1  " Open in new window."
autocmd BufWinEnter \[Buf\ List\] setl nonumber
```


### Vim_airline {#vim-airline}

```cfg

Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

set laststatus=2  "永远显示状态栏"
let g:airline_powerline_fonts = 1  " 支持 powerline 字体"
let g:airline#extensions#tabline#enabled = 1 "显示窗口 tab 和 buffer"
let g:airline_theme='moloai'   murmur 配色不错

if !exists('g:airline_symbols')
  let g:airline_symbols = {}
endif

let g:airline_left_sep = '»'
let g:airline_left_sep = '▶'
let g:airline_right_sep = '«'
let g:airline_right_sep = '◀'
let g:airline_symbols.crypt = ' '	#🔒
let g:airline_symbols.linenr = '☰'
let g:airline_symbols.linenr = '␊'
let g:airline_symbols.linenr = '␤'
let g:airline_symbols.linenr = '¶'
let g:airline_symbols.maxlinenr = ''
let g:airline_symbols.maxlinenr = '㏑'
let g:airline_symbols.branch = '⎇'
let g:airline_symbols.paste = 'ρ'
let g:airline_symbols.paste = 'Þ'
let g:airline_symbols.paste = '∥'
let g:airline_symbols.spell = 'Ꞩ'
let g:airline_symbols.notexists = 'Ɇ'
let g:airline_symbols.whitespace = 'Ξ'

set ambiwidth=double "防止特殊符号无法正常显示"

# " 开启 tabline"
let g:airline#extensions#tabline#enabled = 1
# " tabline 中当前 buffer 两端的分隔字符"
let g:airline#extensions#tabline#left_sep = ' '
# " tabline 中未激活 buffer 两端的分隔字符"
let g:airline#extensions#tabline#left_alt_sep = ' '
# " tabline 中 buffer 显示编号"
let g:airline#extensions#tabline#buffer_nr_show = 1
# " 映射切换 buffer 的键位"
nnoremap [b :bp<CR>
nnoremap ]b :bn<CR>
# " 映射<leader>num 到 num buffer"
map <leader>1 :b 1<CR>
map <leader>2 :b 2<CR>
map <leader>3 :b 3<CR>
map <leader>4 :b 4<CR>
map <leader>5 :b 5<CR>
map <leader>6 :b 6<CR>
map <leader>7 :b 7<CR>
map <leader>8 :b 8<CR>
map <leader>9 :b 9<CR>

let g:airline#extensions#tabline#enabled=1 "顶部 tab 显示"
nmap <tab> :bn<cr> "设置 tab 键映射"
```


### fzf-ag-rg {#fzf-ag-rg}

```cfg

# "<Leader>f 在当前目录搜索文件"
nnoremap <silent> <Leader>f :Files<CR>
# "<Leader>b 切换 Buffer 中的文件"
nnoremap <silent> <Leader>b :Buffers<CR>
# "<Leader>p 在当前所有加载的 Buffer 中搜索包含目标词的所有行，:BLines 只在当前 Buffer 中搜索"
nnoremap <silent> <Leader>p :Lines<CR>
# "<Leader>h 在 Vim 打开的历史文件中搜索，相当于是在 MRU 中搜索，:History：命令历史查找"
nnoremap <silent> <Leader>h :History<CR>


# "Preview window on the right with 50% width"
let g:fzf_preview_window = ['right:50%', 'ctrl-/']
# " Preview window on the upper side of the window with 40% height, hidden by default, ctrl-/ to toggle"
let g:fzf_preview_window = ['up:40%:hidden', 'ctrl-/']
# " Empty value to disable preview window altogether"
let g:fzf_preview_window = []
# " [Buffers] Jump to the existing window if possible"
let g:fzf_buffers_jump = 1
# " [[B]Commits] Customize the options used by 'git log':"
let g:fzf_commits_log_options = '--graph --color=always --format="%C(auto)%h%d %s %C(black)%C(bold)%cr"'
# " [Tags] Command to generate tags file"
let g:fzf_tags_command = 'ctags -R'
# " Commands] --expect expression for directly executing the command"
let g:fzf_commands_expect = 'alt-enter,ctrl-x'


command! -bang -nargs=* Rg	"调用 Rg 进行搜索，包含隐藏文件"
  \ call fzf#vim#grep(
  \   'rg --column --line-number --no-heading --color=always --smart-case --hidden '.shellescape(<q-args>), 1,
  \   <bang>0 ? fzf#vim#with_preview('up:60%')
  \           : fzf#vim#with_preview('right:50%:hidden', '?'),
  \   <bang>0)

# " This is the default extra key bindings"
let g:fzf_action = {
  \ 'ctrl-t': 'tab split',
  \ 'ctrl-x': 'split',
  \ 'ctrl-v': 'vsplit' }

# " Default fzf layout"
# " - down / up / left / right"
let g:fzf_layout = { 'down': '~40%' }

# " In Neovim, you can set up fzf window using a Vim command"
let g:fzf_layout = { 'window': 'enew' }
let g:fzf_layout = { 'window': '-tabnew' }
let g:fzf_layout = { 'window': '10split enew' }

# " Customize fzf colors to match your color scheme"
let g:fzf_colors =
\ { 'fg':      ['fg', 'Normal'],
  \ 'bg':      ['bg', 'Normal'],
  \ 'hl':      ['fg', 'Comment'],
  \ 'fg+':     ['fg', 'CursorLine', 'CursorColumn', 'Normal'],
  \ 'bg+':     ['bg', 'CursorLine', 'CursorColumn'],
  \ 'hl+':     ['fg', 'Statement'],
  \ 'info':    ['fg', 'PreProc'],
  \ 'border':  ['fg', 'Ignore'],
  \ 'prompt':  ['fg', 'Conditional'],
  \ 'pointer': ['fg', 'Exception'],
  \ 'marker':  ['fg', 'Keyword'],
  \ 'spinner': ['fg', 'Label'],
  \ 'header':  ['fg', 'Comment'] }

# " Enable per-command history."
# " CTRL-N and CTRL-P will be automatically bound to next-history and"
# " previous-history instead of down and up. If you don't like the change,"
# " explicitly bind the keys to down and up in your $FZF_DEFAULT_OPTS."

let g:fzf_history_dir = '~/.local/share/fzf-history'

```


### leader {#leader}

```cfg

"""""""""""""""""""""""""""""""
"Leaderf settings"
"""""""""""""""""""""""""""""""
# "文件搜索"
nnoremap <silent> <Leader>f :Leaderf file<CR>

# "历史打开过的文件"
nnoremap <silent> <Leader>m :Leaderf mru<CR>

# "Buffer"
nnoremap <silent> <Leader>b :Leaderf buffer<CR>

# "函数搜索（仅当前文件里）
nnoremap <silent> <Leader>F :Leaderf function<CR>

# "模糊搜索，很强大的功能，迅速秒搜
nnoremap <silent> <Leader>rg :Leaderf rg<CR>

```


### RainbowParentheses {#rainbowparentheses}

```cfg

let g:rbpt_colorpairs = [
    \ ['brown',       'RoyalBlue3'],
    \ ['Darkblue',    'SeaGreen3'],
    \ ['darkgray',    'DarkOrchid3'],
    \ ['darkgreen',   'firebrick3'],
    \ ['darkcyan',    'RoyalBlue3'],
    \ ['darkred',     'SeaGreen3'],
    \ ['darkmagenta', 'DarkOrchid3'],
    \ ['brown',       'firebrick3'],
    \ ['gray',        'RoyalBlue3'],
    \ ['black',       'SeaGreen3'],
    \ ['darkmagenta', 'DarkOrchid3'],
    \ ['Darkblue',    'firebrick3'],
    \ ['darkgreen',   'RoyalBlue3'],
    \ ['darkcyan',    'SeaGreen3'],
    \ ['darkred',     'DarkOrchid3'],
    \ ['red',         'firebrick3'],
    \ ]

let g:rbpt_max = 16
let g:rbpt_loadcmd_toggle = 0
":RainbowParenthesesToggle       " Toggle it on/off

1）python 自动补全库会导致 vim 打开 pyton 和 vimrx 闪退。
  #Plug '/E:/Refinement/Gitee/Vim/jedi'

```


### latex {#latex}

```cfg
Plug 'lervag/vimtex'
let g:tex_flavor='latex'
let g:vimtex_view_method='zathura'
let g:vimtex_quickfix_mode=0
set conceallevel=1
let g:tex_conceal='abdmg'
```


## Other {#other}


### InitFile {#initfile}

```cfg
# "新建.c,.h,.sh,.java 文件，自动插入文件头 "
"autocmd BufNewFile *.cpp,*.[ch],*.sh,*.java exec ":call SetTitle()"
# ""定义函数 SetTitle，自动插入文件头 "
func SetTitle()
    # "如果文件类型为.sh 文件 "
    if &filetype == 'sh'
        call setline(1,"\#########################################################################")
        call append(line("."), "\# File Name: ".expand("%"))
        call append(line(".")+1, "\# Author: ma6174")
        call append(line(".")+2, "\# mail: ma6174@163.com")
        call append(line(".")+3, "\# Created Time: ".strftime("%c"))
        call append(line(".")+4, "\#########################################################################")
        call append(line(".")+5, "\#!/bin/bash")
        call append(line(".")+6, "")
    else
        call setline(1, "/*************************************************************************")
        call append(line("."), "    > File Name: ".expand("%"))
        call append(line(".")+1, "    > Author: ma6174")
        call append(line(".")+2, "    > Mail: ma6174@163.com ")
        call append(line(".")+3, "    > Created Time: ".strftime("%c"))
        call append(line(".")+4, " ************************************************************************/")
        call append(line(".")+5, "")
    endif

    if &filetype == 'cpp'
        call append(line(".")+6, "#include<iostream>")
        call append(line(".")+7, "using namespace std;")
        call append(line(".")+8, "")
    endif

    if &filetype == 'c'
        call append(line(".")+6, "#include<stdio.h>")
        call append(line(".")+7, "")
    endif

    # "新建文件后，自动定位到文件末尾"
    autocmd BufNewFile * normal G
    endfunc
```


### KeyNmap {#keynmap}

```cfg

nmap <leader>w :w!<cr>
nmap <leader>f :find<cr>

map <C-A> ggVGY	" 映射全选+复制 ctrl+a"
map! <C-A> <Esc>ggVGY
map <F12> gg=G
# " 选中状态下 Ctrl+c 复制"
vmap <C-c> "+y"
nnoremap <F2> :g/^\s*$/d<CR> 	"去空行 "
nnoremap <C-F2> :vert diffsplit 	"比较文件  "
map <M-F2> :tabnew<CR>  "新建标签  "
map <F3> :tabnew .<CR>  "列出当前目录文件  "
map <C-F3> \be  	"打开树状文件目录  "

map <F5> :call CompileRunGcc()<CR> "C，C++ 按 F5 编译运行"
func! CompileRunGcc()
    exec "w"
    if &filetype == 'c'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'cpp'
        exec "!g++ % -o %<"
        exec "! ./%<"
    elseif &filetype == 'java'
        exec "!javac %"
        exec "!java %<"
    elseif &filetype == 'sh'
        :!./%
    endif
endfunc

# "C,C++的调试"
map <F8> :call Rungdb()<CR>
func! Rungdb()
    exec "w"
    exec "!g++ % -g -o %<"
    exec "!gdb ./%<"
endfunc

```


### VimTutur {#vimtutur}

```plaintext
noremap 是不会递归的映射 (大概是 no recursion)
前缀代表生效范围;
1) inoremap 就只在插入(insert)模式下生效
2) vnoremap 只在 visual 模式下生效
3) nnoremap 就在 normal 模式下(狂按 esc 后的模式)生效
```


### skill {#skill}

```cfg
au InsertLeave *.* write	#按 Esc 之后会自动保存当前文件
PS:Ctrl+[ 					#同上效果
au BufLeave,FocusLost * wa	#只要 buffer 失去焦点便自动保存

# 可以使用 imap 或 iabbrev 命令设置键映射或缩写词，可以在插入文本时使用。
imap <silent> <C-D><C-D> <C-R>=strftime("%e %b %Y")<CR>
imap <silent> <C-T><C-T> <C-R>=strftime("%l:%M %p")<CR>
  #Insert 模式下输入两次 CTRL-D 将促使 Vim 调用它的内置 strftime() 函数并插入生成的日期，同样，两次按下 CTRL-T 将插入当前时间。
  #使用相同的通用模式，让插入模式或缩写词执行任何 可编写脚本的操作。
    #只需要将相应的 Vimscript 表达式或函数调用放到第一个 <C-R>=（告诉 Vim 插入后面内容的计算结果）
    #\和最后一个 <CR>（告诉 Vim 实际地执行前面的表达式）


function! RemoveTrailingWhitespace()
    if &ft != "diff"
        let b:curcol = col(".")
        let b:curline = line(".")
        silent! %s/\s\+$//
        silent! %s/\(\s*\n\)\+\%$//
        call cursor(b:curline, b:curcol)
    endif
endfunction
autocmd BufWritePre * call RemoveTrailingWhitespace()

```


### tabNo {#tabno}

```cfg

# " 开启 tabline"
let g:airline#extensions#tabline#enabled = 1
# " tabline 中当前 buffer 两端的分隔字符"
let g:airline#extensions#tabline#left_sep = ' '
# " tabline 中未激活 buffer 两端的分隔字符"
let g:airline#extensions#tabline#left_alt_sep = ' '
# " tabline 中 buffer 显示编号"
let g:airline#extensions#tabline#buffer_nr_show = 1
# " 映射切换 buffer 的键位"
nnoremap [b :bp<CR>
nnoremap ]b :bn<CR>
# " 映射<leader>num 到 num buffer"
map <leader>1 :b 1<CR>
map <leader>2 :b 2<CR>
map <leader>3 :b 3<CR>
map <leader>4 :b 4<CR>
map <leader>5 :b 5<CR>
map <leader>6 :b 6<CR>
map <leader>7 :b 7<CR>
map <leader>8 :b 8<CR>
map <leader>9 :b 9<CR>

```