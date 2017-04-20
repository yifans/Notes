# TeX 环境搭建

## 下载发行版镜像
- 选择 `Texlive`, 不要选择长时间为更新的 `CTeX` 套装
- 下载地址，在科大，可以直接使用学校的开源镜像：
http://mirrors.ustc.edu.cn/CTAN/systems/texlive/Images/texlive2016.iso

##　安装步骤

### 安装　`TeXlive`
- Windows环境参考：http://zhuanlan.zhihu.com/LaTeX/19779481

- Linux环境参考:
  * http://zhuanlan.zhihu.com/LaTeX/20069414
  * http://www.latexstudio.net/archives/8806

### 安装一个编辑器

可以安装的`TeXstudio`：http://texstudio.sourceforge.net/
如果撰写中文文档，修改默认编译方式：Options -> Configure Texstudio -> Build -> Default 修改为XeLaTeX，并使用`ctex`宏包（不是CTeX套装）

## 学习使用
### 实体书推荐
- `LaTeX入门` 作者: 刘海洋 ISBN: 9787121202087

### 视频教程
- ChinaTex 旧视频教程：http://www.chinatex.org/?page_id=218
  这一教程使用`CTeX`套装讲解，可以作为入门
- ChinaTex 新视频教程, 需要购买 https://item.taobao.com/item.htm?spm=a1z10.1-c.w4004-3473795048.2.y81q5C&id=43823508044

### 网站
- LaTeX开源小屋 http://www.latexstudio.net/ ，其维护的 [LaTeXStudio 知识王国](https://github.com/latexstudio/LaTeX-TeXWiki) 值得参考

### 配套文档
- 使用`texdoc` 命令查看系统文档，如查看`ctex宏包`文档：`texdoc ctex`
