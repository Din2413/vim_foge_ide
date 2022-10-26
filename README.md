<h1 align="center">代码编辑器：将Vim打造成爱不释手的IDE</h1>

# Vim基本用法

<h3>vim操作模式</h3>

1、Normal Mode 普通模式</br>
功能：在这种模式下可以移动光标等;</br>
进入：默认进入vim之后，处于这种模式。在其他模式下狂按ESC后进入此模式;</br>
```
gi 快速跳转到最后一次编辑的地方并进入插入模式

" word指的是以非空白符分割的单词，WORD指的是以空白符分割的单词
w/W 移动到下一个word/WORD开头
e/E 移动到下一个word/WORD结尾
b/B 移动到上一个word/WORD开头

f{char} 往后搜索，移动到同一行的char字符上，可以使用分号(;)/逗号(,)继续改搜索该行的下/上一个
t{char} 往后搜索，移动到同一行的char的前一个字符上，可以使用分号(;)/逗号(,)继续改搜索该行的下/上一个
F 表示往前搜索

0 移动到行首
$ 移动到行尾

gg 移动到文件开头
G  移动到文件结尾

H 移动到屏幕开头
M 移动到屏幕中间
L 移动到屏幕结尾

ctrl + u 向上翻页
ctrl + f 向下翻页

x 快速删除一个字符，可配合数字删除多个字符，如：4x表示删除4个字符
d 配合文本对象快速删除特定内容
比如：daw (d around word)删除单词以及周围空格，dt) (d to )) 删除直到)的内容，dd删除一行，4dd删除4行；

r 替换一个字符
s 删除一个字符并且进入插入模式
c 配合文本对象快速删除特定内容并且进入插入模式
比如：cw 删除单词并进入插入模式

/ 前向搜索
? 后向搜索
n 移动搜索结果的下一个
N 移动搜索结果的上一个

ctrl + w + w 在窗口间循环切换 （一个缓冲区可以切割成多个窗口，每个窗口可以打开不同的缓冲区）
ctrl + w + l 切换到右边的窗口
ctrl + w + h 切换到左边的窗口
ctrl + w + j 切换到下边的窗口
ctrl + w + k 切换到上边的窗口
```

2、Visual Mode 可视模式</br>
功能：在这种模式下可以选定一些字符、行、多列;</br>
进入：在普通模式下，按v进入;</br>

3、Insert Mode 插入模式</br>
功能：在这种模式下可以编辑输入等;</br>
进入：普通模式下，可以按i、a、o、I、A、O等进入;</br>
```
ctrl + h 删除上一个字符
ctrl + w 删除上一个单词
ctrl + u 删除当前行内容
```

4、Command-Line 命令行模式</br>
功能：可以输入各种命令;</br>
进入：普通模式下按冒号(:)进入;</br>
```
:e 打开另一个文件
:ls 列举当前缓冲区（每一个打开的文件对应一个缓冲区）
:b n 跳转到第n个缓冲区
:bpre :bnext 跳转到当前缓冲区的上一个或下一个缓冲区
:bfirst :blast 跳转到第一个或最后一个缓冲区

:sp 垂直分割当前缓冲区窗口，后加文件可直接在新的窗口中打开指定文件
:vs 水平分割当前缓冲区窗口，后加文件可直接在新的窗口中打开指定文件
```

5、Ex Mode Ex模式</br>
功能：多行的Command-Line模式;</br>
进入：普通模式下按Q进入Ex模式;</br>

6、Select Mode 选择模式</br>
功能：在gvim下常用的模式，用鼠标拖选区域的时候，就进入了选择模式。和可视模式不同的是，在这个模式下，选择完了高亮区域后，敲任何按键就直接输入并替换选择的文本了;</br>
进入：普通模式下，可以按gh进入;</br>

<h3>vim配置文件</h3>

~/.vimrc是控制vim行为的配置文件，无论窗口外观、字体显示，还是操作方式、插件属性均可通过编辑该文件进行深度定制；</br>
~/.vim/syntax/用于存放语法描述脚本；</br>
~/.vimspell/用于存放拼写检查脚本；</br>
~/.vim/doc/用于存放各插件帮助文件；</br>
~/.vim/plugin/用于存放每次vim启动运行的插件脚本；</br>

<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/vim%E5%91%BD%E4%BB%A4%E9%80%9F%E6%9F%A5%E5%8D%A1.png" alt=""/><br />
 （vim 命令速查）
</div>

<h3>vim自定义快捷键</h3>
vim存在很多预置快捷键，再加上各类插件的快捷键，大量快捷键出现在单层空间中难免引起冲突。为缓解冲突文件，vim引入 <leader> 前缀键，以此衍生出更多的快捷键命名空间。例如将r键配置为<leader> r、<leader> <leader> r等多个快捷键。</br>
前缀键默认为"\"，使用如下命令，可以将前缀键定义为逗号：
 
```
led mapleader=","
```

在定义前缀键之后，使用如下命令，定义快捷键用于删除当前文件中所有行尾多余空格：

```
" noremap为非递归映射，map为递归映射
" 1、前者可解决后者映射命令存在包含关系时陷入递归陷阱的问题
" 比如 map dd jddk 用于将dd命令映射为jddk（下移一行、删除、上移一行），但实际执行时，执行j之后遇到dd，vim认为仍然需要映射，因此dd又被映射为jddk，导致一直循环映射
" 2、映射命令存在生效模式选择，n代表普通模式生效、i代表插入模式生效、v代表可视模式生效、c代表命令行模式生效
" nnoremap首字符为n，则代表普通模式下生效的非递归映射
nnoremap <leader>W :%s/\s\+$//<cr>:let @/=''<CR>
```

# Vim源码安装
正常Linux发行版（如：Ubuntu、Fedora、Debian等）中预置的 Vim 大多都存在功能阉割，或版本较久。因此，在搭建基于Vim的代码编辑器时，最好将预置Vim升级成全功能的最新版。

此外，Vim 插件中存在大量由 perl、python、lua、ruby 等主流脚本语言编写的插件，在源码编译/安装Vim编辑器之前，需先对 python、lua、ruby、perl 等进行安装，然后再Vim编译时增加 --enable-pythoninterp、--enable-luainterp、--enable-rubyinterp、---enable-perlinterp 等选项用于支持 python、lua、ruby、perl 编写的插件。

```
" 第一步：在安装新版本的vim之前，卸载原来安装的老版本vim
sudo apt-get remove vim  
sudo apt-get remove vim-runtime  
sudo apt-get remove gvim  
sudo apt-get remove vim-tiny  
sudo apt-get remove vim-common  
sudo apt-get remove vim-gui-common 

" 第二步：安装 python、lua、ruby、perl
sudo apt install git python-dev ruby-dev lua5.1-policy lua5.1-policy-dev  libncurses5-dev

" 第三步：下载 Vim 源码
git clone git@github.com:vim/vim.git

" 第四步：编译安装Vim
" PS: vim8不能同时支持python和python3，源码编译时请勿同时配置python2和python3
cd vim/
./configure --enable-multibyte \
            --enable-python3interp=yes \
            --with-python3-config-dir=/usr/lib/python3.6/config \
            --enable-luainterp=yes \
            --with-lua-prefix=/usr \
            --enable-rubyinterp=yes \
            --with-ruby-command=ruby \
            --enable-perlinterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope
sudo make
sudo make install

" 第五步：如上安装完成之后，执行vim --version可以发现并未支持perl，可以查看一下vim/src/auto/config.log,发现异常大多为：/usr/bin/ld: cannot find -lperl
" 4.1 看出libperl.so位置
cd /; sudo find . -name "libperl.so*"
" 4.2 在-L/usr/lib/x86_64-linux-gnu/perl/5.26/CORE下创建libperl.so链接文件
cd /usr/lib/x84_64-linux-gnu/perl/5.26/CORE
sudo ln -s /usr/lib/x86_64-linux-gnu/libperl.so.5.26 libperl.so
" 4.3 重新执行一遍configure、make、make install

" 第六步：设置系统环境变量，在/etc/profile系统环境变量中，增加export行，并执行source立即生效
sudo vim /etc/profile
export PATH="$PATH:/usr/local/bin/"
sudo source /etc/profile
```

编译安装完成之后，执行 vim --version 即可看到如下结果：
<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/vim%E7%89%88%E6%9C%AC%E4%BF%A1%E6%81%AF.png" alt=""/><br />
 （vim 版本信息）
</div>

# Vim插件管理
vim \*.vim 传统格式的插件打包文件中存在 \*.vim （插件脚本）和 \*.txt （插件帮助文件）两类文件。

手动安装插件时，将解包后的 \*.vim 拷贝到 ~/.vim/plugin/， \*.txt 拷贝到 ~/.vim/doc/ 即可完成插件安装，重启vim后刚安装的插件即已生效，但帮助文件需执行 :helptags ~/.vim/doc/ 才能生效，后续可通过 :h *** 查看插件帮助信息。

传统格式插件需要解包和两次拷贝才能完成安装，相对比较繁琐，且还存在如下几个问题：

* 插件名字冲突：所有插件的帮助文档都在 doc/ 子目录、插件脚本都在 plugin/ 子目录，同个名字空间下必然引发名字冲突；
* 插件卸载易误：你需要先知道 doc/ 和 plugin/ 子目录下哪些文件是属于该插件的，再逐一删除，容易多删/漏删；

为使每个插件在.vim/下都有各自独立子目录，插件升级、卸载时，只需找到对应插件目录进行变更。<a href="https://github.com/VundleVim/Vundle.vim">vundle</a> 插件管理器应运而生，其可以让你在配置文件中管理插件，且可以非常方便的查找、安装、更新或卸载插件，并自动配置插件的运行路径和生成帮助文件。

通过如下命令安装 vundle 插件管理器：
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

在 ~/.vimrc 增加插件配置信息：
```
" vundle 环境设置
filetype off
" 将 Vundle 加入运行时路径中(Runtime path)
set rtp+=~/.vim/bundle/Vundle.vim
" vundle 管理的插件列表必须位于 vundle#begin() 和 vundle#end() 之间
call vundle#begin()
" vundle 插件管理器
Plugin 'VundleVim/Vundle.vim'
" 插件列表结束
call vundle#end()
filetype plugin indent on
```

执行如下命令可安装、卸载、更新、查询插件：
```
" 插件安装：先在 .vimrc vundle#begin() 与 vundle#end() 之间加入 Plugin 配置
" vim 主题插件
Plugin 'altercation/vim-colors-solarized'
" 后续进入 vim 命令行模式，执行如下命令安装插件
:PluginInstall

" 插件卸载：先从 .vimrc vundle#begin() 与 vundle#end() 之间删除 Plugin 配置
" 后续进入vim命令行模式，执行如下命令卸载插件
:PluginClean

" 插件更新：vim 命令行模式下执行如下命令更新插件
:PluginUpdate

" 插件搜索：vim 命令行模式下执行如下命令搜索foo插件
:PluginSearch foo
```
PS:可在插件网站 https://vimawesome.com 上搜寻符合预期的vim插件。

# 构建代码编辑器 
<h3>代码补全</h3>
传统的 Vim 代码补全基本以 omni 系列补全和符号补全为主，omni 补全系统是 Vim 自带的针对不同文件类型编写不同的补全函数的基础语义补全系统，搭配 neocomplete 可以很方便的对所有补全结果（omni补全/符号补全/字典补全）进行一个合成并且自动弹出补全框，虽然赶不上 IDE 的补全，但是已经比大部分编辑器补全好用很多了。</br>

然而传统 Vim 补全还是有两个迈不过去的坎：语义补全太弱，其次是补全分析无法再后台运行，对大项目而言，某些复杂符号的补全会拖慢你的打字速度。</br>

新一代的 Vim 补全系统，<a href="https://github.com/ycm-core/YouCompleteMe">YouCompleteMe</a> 和 <a href="https://github.com/Shougo/deoplete.nvim">Deoplete</a> ，都支持异步补全和基于 clang 的语义补全，前者集成度高，后者扩展方便。对于 C/C++ 的话，推荐使用 YCM，因为 deoplete 的 clang 补全插件不够稳定，太吃内存，并且反应比较慢。</br>

使用如下步骤安装YouCompleteMe插件：
```
" YouCompleteMe可采用Vundle安装和git手动安装两种，官方推荐Vundle安装，若前者安装不上，可采用手动安装，这里采用Vundle安装方式，手动方式不做赘述
" Vundle插件管理增加如下配置，并vim命令行中执行:PluginInstall进行安装,整个安装过程较慢，请耐心等待
Plugin "ycm-core/YouCompleteMe"

" 如上步骤安装完成之后，便可跳转到~/.vim/bundle/YouCompleteMe执行如下命令完成插件安装
" 整个安装过程可能会提示各种异常，具体可见下方异常解决
./install.py --all
```

在安装YouCompleteMe插件过程中，提示异常和对应解决方案如下所示：</br>
1、CMake 3.14 or higher is required.  You are running version 3.10.2，即cmake版本较低，需>3.14</br>
解决方案：安装cmake-3.17.1
```
" 第一步：下载cmake-3.17.1源码
wget https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1.tar.gz
" 解压cmake-3.17.1
tar -xvf cmake-3.17.1.tar.gz

" 第二步：配置、编译安装
./bootstrap
make
sudo make install
```

2、Your C++ compiler does NOT fully support C++17，即gcc版本较低，不支持C++17</br>
解决方案：安装gcc8.1.0（参考<a href="https://blog.csdn.net/davidhopper/article/details/79681695">GCC 9.1编译器安装方法</a>）
```
" 第一步：下载gcc8.1.0源码
wget ftp://ftp.mirrorservice.org/sites/sourceware.org/pub/gcc/releases/gcc-8.1.0/gcc-8.1.0.tar.xz
" 解压gcc8.1.0
tar -Jxvf gcc-8.1.0.tar.xz

" 第二步：下载依赖包，默认的下载服务器ftp://gcc.gnu.org/pub/gcc/infrastructure/下载会失败
" 需修改download_prerequisites将默认服务器替换成http://mirror.linux-ia64.org/gnu/gcc/infrastructure/镜像服务器
cd gcc-8.1.0
./contrib/download_prerequisites

" 第三步：运行configure命令生成Makefile
./gcc-8.1.0/configure --prefix=/usr/local/gcc-8.1

如果配置过程中出现一下错误，意味着缺少gcc-multilib库，则执行sudo apt-get install gcc-multilib进行安装解决
/usr/bin/ld: cannot find Scrt1.o: No such file or directory
/usr/bin/ld: cannot find crti.o: No such file or directory
/usr/bin/ld: skipping incompatible /usr/lib/gcc/x86_64-linux-gnu/7/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc
/usr/bin/ld: skipping incompatible /usr/lib/gcc/x86_64-linux-gnu/7/libgcc.a when searching for -lgcc
/usr/bin/ld: cannot find -lgcc
collect2: error: ld returned 1 exit status
configure: error: I suspect your system does not have 32-bit development libraries (libc and headers). If you have them, rerun configure with --enable-multilib. If you do not have them, and want to build a 64-bit-only compiler, rerun configure with --disable-multilib.

" 第四步：运行make命令编译构建GCC编译器
make

" 第五步：运行sudo make install命令安装GCC编译器
sudo make instal

" 第六步：指定本机使用最新版本GCC编译器，使用update-alternatives命令配置增加最新版本编译器
" update-alternatives --install <链接> <名称> <路径> <优先级>
sudo update-alternatives --install /usr/bin/gcc gcc /usr/local/bin/gcc 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/local/bin/g++ 50
" 查询本机已有GCC编译器情况
sudo update-alternatives --query gcc
" 查询本机已有G++编译器情况
sudo update-alternatives --query g++
```

YouCompleteMe配置：</br>
1、增加YCM配置文件，该文件只对C、C++生效，在.vimrc中let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'的配置（参考工程中的.ycm_extra_conf.py文件）；</br>
2、.vimrc中的其他YCM配置选项;
```
" YouCompleteMe
" Python Semantic Completion
let g:ycm_python_binary_path = '/usr/bin/python3'
" C family Completion Path
let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'
" 跳转快捷键
nnoremap <c-k> :YcmCompleter GoToDeclaration<CR>|
nnoremap <c-h> :YcmCompleter GoToDefinition<CR>| 
nnoremap <c-j> :YcmCompleter GoToDefinitionElseDeclaration<CR>|
" 停止提示是否载入本地ycm_extra_conf文件
let g:ycm_confirm_extra_conf = 0
" 语法关键字补全
let g:ycm_seed_identifiers_with_syntax = 1
" 开启 YCM 基于标签引擎
let g:ycm_collect_identifiers_from_tags_files = 1
" 从第2个键入字符就开始罗列匹配项
let g:ycm_min_num_of_chars_for_completion=2
" 在注释输入中也能补全
let g:ycm_complete_in_comments = 1
" 在字符串输入中也能补全
let g:ycm_complete_in_strings = 1
" 注释和字符串中的文字也会被收入补全
let g:ycm_collect_identifiers_from_comments_and_strings = 1
" 弹出列表时选择第1项的快捷键(默认为<TAB>和<Down>)
let g:ycm_key_list_select_completion = ['<C-n>', '<Down>']
" 弹出列表时选择前1项的快捷键(默认为<S-TAB>和<UP>)
let g:ycm_key_list_previous_completion = ['<C-p>', '<Up>']
" 主动补全, 默认为<C-Space>
let g:ycm_key_invoke_completion = ['<C-Space>']
" 停止显示补全列表(防止列表影响视野), 可以按<C-Space>重新弹出
let g:ycm_key_list_stop_completion = ['<C-y>']
```

<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/YouCompleteMe.gif" alt=""/><br />
 （YouCompleteMe效果图）
</div>

<h3>项目管理</h3>
NERDTree是Vim编辑器的文件系统浏览器。使用此插件，用户可以直观地浏览复杂的目录层次结构，快速打开文件以进行读取或编辑，以及执行基本的文件系统操作。

vim的Vundle插件管理安装NERDTree：
```
Plugin 'preservim/nerdtree'
```

.vimrc增加NERDTree插件配置：
```
" vim启动时，自动打开NERDTree
autocmd vimenter * NERDTree
" vim未指定文件启动时，自动打开NERDTree
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif
" vim在打开目录启动时，自动打开NERDTree
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | exe 'cd '.argv()[0] | endif
```

NERDTree常用快捷键：
```
ctrl + w + h 光标 focus 左侧树形目录
ctrl + w + l 光标 focus 右侧文件显示窗口
ctrl + w + w 光标自动在左右侧窗口切换
ctrl + w + r 移动当前窗口的布局位置

o 在已有窗口中打开文件、目录或书签，并跳到该窗口
go 在已有窗口 中打开文件、目录或书签，但不跳到该窗口
P 跳到根结点
p 跳到父结点
K 到同目录第一个节点
J 到同目录最后一个节点
```

<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/NERDTree.png" alt=""/><br />
 （NERDTree效果图）
</div>

<h3>代码检查</h3>
代码检查有利于在你编辑代码的同时就帮你把潜在错误编注出来，从而不用等到编译或者运行时才发现问题，提前暴露问题。</br>

知名的 vim 代码检测插件有</a href="https://github.com/vim-syntastic/syntastic">syntastic</a> 、<a href="https://github.com/dense-analysis/ale">ALE</a> 等。前者比较老旧，不能实时检查，且保存文件检查器运行时间较长，效率较低；后者功能相对强大，支持实时检测与并发运行，且可同步在标识栏/状态栏显示检测结果。

未完待续...
