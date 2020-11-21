<h1 align="center">代码编辑器：将Vim打造成爱不释手的IDE</h1>

# Vim基本用法

~/.vimrc是控制vim行为的配置文件，无论窗口外观、字体显示，还是操作方式、插件属性均可通过编辑该文件进行深度定制；

~/.vim/syntax/用于存放语法描述脚本；

~/.vim/spell/用于存放拼写检查脚本；

~/.vim/doc/用于存放各插件帮助文件；

~/.vim/plugin/用于存放每次vim启动运行的插件脚本；

<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/vim%E5%91%BD%E4%BB%A4%E9%80%9F%E6%9F%A5%E5%8D%A1.png" alt=""/><br />
 （vim 命令速查）
</div>

# Vim源码安装
正常Linux发行版（如：Ubuntu、Fedora、Debian等）中预置的 Vim 大多都存在功能阉割，或版本较久。因此，在搭建基于Vim的代码编辑器时，最好将预置Vim升级成全功能的最新版。

此外，Vim插件中存在大量由perl、python、lua、ruby等主流脚本语言编写的插件，在源码编译/安装Vim编辑器之前，需先对python、lua、ruby、perl等进行安装，然后再Vim编译时增加--enable-pythoninterp、--enable-luainterp、--enable-rubyinterp、---enable-perlinterp等选项用于支持python、lua、ruby、、perl编写的插件。

```
# 第一步：安装python、lua、ruby、perl
sudo apt install git python-dev ruby-dev lua5.1-policy lua5.1-policy-dev  libncurses5-dev

# 第二步：下载Vim源码
git clone git@github.com:vim/vim.git

# 第三步：编译安装Vim
cd vim/
./configure --enable-pythoninterp=yes --with-python-config-dir=/usr/lib/python2.7/config --enable-luainterp=yes --with-lua-prefix=/usr --enable-rubyinterp=yes --with-ruby-command=ruby --enable-perlinterp=yes
sudo make
sudo make install
```

编译安装完成之后，执行vim --version即可看到如下结果：
<div align="center">
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/vim%E7%89%88%E6%9C%AC%E4%BF%A1%E6%81%AF.png" alt=""/><br />
 （vim 版本信息）
</div>

# Vim插件管理
vim \*.vim传统格式的插件打包文件中存在\*.vim（插件脚本）和\*.txt（插件帮助文件）两类文件。

手动安装插件时，将解包后的\*.vim拷贝到~/.vim/plugin/，\*.txt拷贝到~/.vim/doc/即可完成插件安装，重启vim后刚安装的插件即已生效，但帮助文件需执行 :helptags ~/.vim/doc/ 才能生效，后续可通过 :h *** 查看插件帮助信息。

传统格式插件需要解包和两次拷贝才能完成安装，相对比较繁琐，且还存在如下几个问题：

* 插件名字冲突：所有插件的帮助文档都在 doc/ 子目录、插件脚本都在 plugin/ 子目录，同个名字空间下必然引发名字冲突；
* 插件卸载易误：你需要先知道 doc/ 和 plugin/ 子目录下哪些文件是属于该插件的，再逐一删除，容易多删/漏删；

为使每个插件在.vim/下都有各自独立子目录，插件升级、卸载时，只需找到对应插件目录进行变更。vundle（https://github.com/VundleVim/Vundle.vim） 插件管理器应运而生，其可以让你在配置文件中管理插件，且可以非常方便的查找、安装、更新或卸载插件，并自动配置插件的运行路径和生成帮助文件。

<h3>通过如下命令安装vundle插件管理器：</h3>

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

<h3>在~/.vimrc增加插件配置信息：</h3>

```
" vundle 环境设置
filetype off
" 将Vundle加入运行时路径中(Runtime path)
set rtp+=~/.vim/bundle/Vundle.vim
" vundle 管理的插件列表必须位于 vundle#begin() 和 vundle#end() 之间
call vundle#begin()
" vundle插件管理器
Plugin 'VundleVim/Vundle.vim'
" 插件列表结束
call vundle#end()
filetype plugin indent on
```

<h3>执行如下命令可安装、卸载、更新、查询插件：</h3>

```
# 插件安装：先在.vimrc vundle#begin()与vundle#end()之间加入Plugin配置
# vim主题插件
Plugin 'altercation/vim-colors-solarized'
# 后续进入vim命令行模式，执行如下命令安装插件
:PluginInstall

# 插件卸载：先从.vimrc vundle#begin()与vundle#end()之间删除Plugin配置
# 后续进入vim命令行模式，执行如下命令卸载插件
:PluginClean

# 插件更新：vim命令行模式下执行如下命令更新插件
:PluginUpdate

# 插件搜索：vim命令行模式下执行如下命令搜索foo插件
:PluginSearch foo
```
PS:可在插件网站 https://vimawesome.com 上搜寻符合预期的vim插件。
