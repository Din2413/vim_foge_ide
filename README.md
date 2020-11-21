<h1 align="center">代码编辑器：将Vim打造成爱不释手的IDE</h1>

# 介绍Vim基本用法

# 源码安装Vim编辑器
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
<img src="https://github.com/YearMonthDay/vim_foge_ide/blob/main/picture/vim%20version.png" alt=""/><br />
 （vim 版本信息）
</div>
