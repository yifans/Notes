#

1. 下载镜像文件

在科大，可以直接使用学校的开源镜像：
http://mirrors.ustc.edu.cn/CTAN/systems/texlive/Images/texlive2015-20150523.iso

2. 安装

Windows环境参考：http://zhuanlan.zhihu.com/LaTeX/19779481
Linux环境参考http://zhuanlan.zhihu.com/LaTeX/20069414

修正：
安装教程中提示将「After installation, get package updates from CTAN」选择为「否」。这是作者对此的误读，请选择为「是」。其意义是将 tlmgr 的 repository 选项设置为 http://mirror.ctan.org/systems/texlive/tlnet。若选择否，则 tlmgr 的 repository 选项设置为 iso 镜像的挂载位置。这个选项打开之后，并不会在 iso 安装完成之后立即联网更新宏包。

3. 安装一个编辑器

我安装的是TeXstudio：http://texstudio.sourceforge.net/
修改默认编译方式：Options -> Configure Texstudio -> Build -> Default 修改为XeLaTeX
