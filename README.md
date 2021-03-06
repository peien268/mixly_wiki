# Mixly Wiki 

## Mixly Wiki 编写准备

### 注册github账号
https://github.com/join?source=header-home

### 安装github同步软件github-desktop 
https://desktop.github.com/

### 安装好用的文本编辑器sublime
http://www.sublimetext.com/

### 克隆项目到本地
* 打开github-desktop 软件，依次点击：File-Clone a Repository-URL，在URL中输入https://github.com/hznupeter/mixly_wiki.git
* 设置项目本地存储地址

![](images/clone_repo.png)

## 编写项目
* 打开github-desktop 软件，依次点击Repository-open in sublime Text,用sublime打开该项目进行编辑。
![](images/sublime.png)

## 项目目录说明
```
|--doc
   |--build  /*生成目录*/
      |--doctrees
      |--gettext
      |--html
   |--source /*源文件目录*/
      |--_static /*静态html文件目录*/
      |--_templates /*自定义模板目录*/
      |--arduino /*arduino部分wiki目录*/
         |--images /*arduino引用图片*/
            |--02  /*02.XXX.rst 文件引用的图片目录*/
               |-- analogRead.png /*所有图片都用png格式，文件命名格式为该函数名*/
               |-- analogRead-example.png /*模块使用范例截图*/
               |-- analogRead.en.png /*analogRead.png对应的英文图片*/
               |-- analogRead-example.en.png /*analogRead-example.png对应的英文图片*/
      |--basic /*软件基础部分wiki目录*/
      |--locale /*多语言目录*/
      |--MicroPython /*micropython部分wiki目录*/
      |--Python /*python部分wiki目录*/

```
以 arduino为例进行目录说明，arduino目录中包含多个rst文件，rst为wiki的核心文件，通过编辑该类文件创建wiki。

在编写mixly wiki过程中可以参考 arduino语法。

编写wiki所使用rst文档采用的是Sphinx，常用语法可以参考下面链接。
https://zh-sphinx-doc.readthedocs.io/en/latest/contents.html

## Arduino 语法参考
http://www.cnblogs.com/xczr/p/7832015.html

https://www.arduino.cc/reference/en/


## wiki编写说明
根据mixly模块顺序，介绍每一个模块。包括截图、描述、参数、返回值、范例、注释（注意点）。

编写文件可以参考```source\arduino\02.Input-Output.rst```

显示效果可以参考 https://mixly-wiki-test.readthedocs.io/zh_CN/latest/arduino/02.Input-Output.html

## 提交代码

修改文本后，按照下图操作提交代码。
![](images/commit.png)

## 本地预览
* 安装python3.x
* 打开cmd，输入以下命令，配置基础环境
```
pip install -U Sphinx
pip install sphinx_rtd_theme
pip install --upgrade recommonmark
```
* 跳转到本地项目路径，执行生成命令
```
cd Documents\GitHub\mixly_wiki\doc
make html
```
![](images/cmd.png)
* 打开build/html/index.html本地预览。

## 在线预览
在提交代码之后，浏览https://mixly-wiki-test.readthedocs.io/zh_CN/latest/


## 支持pdf导出(高级应用)

### Mac 配置环境

Sphinx 生成 PDF 的过程先将 rst 转换为 tex，再生产PDF。这个过程遇到了比较多的坑，最后总结下来过程如下：
首先，安装 Tex 环境。在 Mac 上，推荐安装 MacTex 而不是 BasicTex，对于新手来说 BasicTex 上需要自己处理很多以来问题。完成后使用 tlmgr 更新 TexLive。

$ brew cask install mactex
$ sudo tlmgr update --self

然后，在 conf.py 中设置 latex_engine 和 latex_elements 两个参数。
latex_engine = 'xelatex'
latex_elements = {
    'papersize': 'a4paper',
    'pointsize': '11pt',
    'preamble': r'''
\usepackage{xeCJK}
\setCJKmainfont[BoldFont=STZhongsong, ItalicFont=STKaiti]{STSong}
\setCJKsansfont[BoldFont=STHeiti]{STXihei}
\setCJKmonofont{STFangsong}
\XeTeXlinebreaklocale "zh"
\XeTeXlinebreakskip = 0pt plus 1pt
\parindent 2em
\definecolor{VerbatimColor}{rgb}{0.95,0.95,0.95}
\setcounter{tocdepth}{3}
\renewcommand\familydefault{\ttdefault}
\renewcommand\CJKfamilydefault{\CJKrmdefault}
'''
}

### 编译pdf

$ make latexpdf

make latexpdf 会完成 rst转换为 tex 并将 tex 生成 PDF，可以手动分开：
$ make latex
$ cd build/latex
$ make

在 build/latex 下可以查看到生成的 PDF 文档。
