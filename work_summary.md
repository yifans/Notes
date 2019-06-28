# 控制组生存指南
- 毕业前，将在控制组学习的各个资料做一汇总
- 希望前人栽树，后人乘凉
- 希望后续组内师弟师妹们对本文档进行持续补充

# 学习
## Linux学习
- Linux是本组学习和科研的基本工具，必须掌握
- 实验室服务器均为CentOS7系统，学习也以CentOS7为重
- 个人计算机可以使用Ubuntu

### 入门
- 《快乐的Linux命令行》：本书更适合作为Linux入门学习
- 《鸟哥的Linux私房菜》：
  - 本书较厚，可以用作参考手册，有时间可以通读
  - 上册为基本操作，下册为服务器搭建指南
- 我的学习笔记
  - https://github.com/yifans/Notes/tree/master/Linux/Linux_itercast
  - 这是我2013年学习时的笔记，对应的视频课程已经找不到了
  - 该笔记是基于CentOS6的，学习时注意与CentOS7区分

### 其它
- 科大LUG协会：https://lug.ustc.edu.cn/wiki/
- 科大镜像：可以下载各种Linux发行版的镜像文件
  - mirrors.ustc.edu.cn

## 编程语言
### C
- 《c primer plus》
- 《C程序设计语言》 K&R
- 《UNIX环境高级编程》
- 《Linux程序设计 : 第4版》


### Python
- 安装 Anaconda Python 较为方便
#### 入门
- 《简明Python 教程》
- 廖雪峰教程：https://www.liaoxuefeng.com/wiki/1016959663602400
#### 进阶
- 《Python Cookbook》
- 《流畅的Python》十分推荐！
#### Python 与 EPICS
- pyepics
  * 官方文档：https://cars9.uchicago.edu/software/python/pyepics3/
  * training：https://epics.anl.gov/docs/APS2014 中的 CA Programming in Python
- pvaPy
  * github主页：https://github.com/epics-base/pvaPy
  * 文档：https://epics.anl.gov/extensions/pvaPy/production/index.html#

### Java
- 《Java核心技术》

### JavaScript
- 廖雪峰教程：https://www.liaoxuefeng.com/wiki/1022910821149312
- 《JavaScript高级程序设计（第3版）》

### Shell
- 《鸟哥的Linux私房菜》
- 《Linux Shell脚本攻略》https://book.douban.com/subject/6889456/
- 《Advance Bash-Scripting Guide》 Shell编程最权威的书，有开源版本

## 计算机基础
### 操作系统
- 《深入理解计算机系统》，也称为 CSAPP，
  - 计算机科学极佳的入门书
  - B站课程 https://github.com/EugeneLiu/translationCSAPP/blob/master/contribution.md
  - github主页：https://github.com/EugeneLiu/translationCSAPP/blob/master/contribution.md
- 《Operating Systems: Three Easy Pieces》很通俗易懂
- 《现代操作系统》
- 哈尔滨工业大学操作系统教程：https://study.163.com/series/1202806603.htm

### 数据库
- 《MySQL必知必会》
- 《SQL必知必会》
- 《高性能MySQL》


### 计算机网络
- 浙江大学 计算机网络教程 https://v.youku.com/v_show/id_XNjQxNTUwNzk2.html?spm=a2h0k.11417342.soresults.dtitle
- 《TCP/IP详解 卷1：协议》


## 加速器物理
- 加速器物理学 S.Y.Lee
- 加速器物理基础，陈佳洱，可以作为王老师加速器物理课程的资料补充
- 同步辐射光源物理引论，刘祖平
- 电子直线加速器设计基础，裴元吉
 

# 科研
## EPICS
- EPICS是本组工作的基础
- EPICS资料基本都是英文，中文资料都不靠谱（中文与EPICS相关的毕业论文和期刊论文可以做参考）
- EPICS官网：https://epics.anl.gov/，下面对左侧每一栏内容做一解释
  - Home 本网站内容概览
  - News：各个版本发布的Release Note
    * Meetings 每年两次的 EPICS Collaboration Meetings，进入每个会议的链接可以找到会议报告PPT，从中可以知道EPICS社区的最新动向，从中可以得到启发
    * Codeathons 不知道是啥
  - About EPICS 自身介绍
    * Council EPICS组委会，可以看到国际上主要使用和开发EPICS的呻吟声
    * Contact EPICS各个部分遇到问题该找谁，更优先的tech-talk中提问
    * 10 Things EPICS优势
  - Base EPICS核心 版本信息
    * EPICS7 可以下载
    * EPICS R3.15 文档较为全面，主要有
      - EPICS Application Developer's Guide EPICS开发资料
      - EPICS R3.15 Channel Access Reference Manual CA协议的手册
      - Channel Access Protocol Specification CA协议说明
    * EPICS R3.14.12
      - Record Reference Manual 各个记录的说明（非常重要）
  - Modules 各个驱动程序的下载地址
  - Extensions
    * 包括了CA客户端和服务端软件和各种编程语言接口
    * 使用比较多的有：
      - Archiver Appliance
      - StripTool 画图
      - Gateway
      - pvaPy 和 PyEpics3， Python接口
      - VDCT
      - procServ 后台运行程序
      - RecSync
      - WiresharkCA
  - Distributions epics各种发行版
  - Downloads 各个部分
  - Search 没啥用
  - EPICS V4 新版本EPICS
  - IRMIS 我们没有用
  - Talk EPICS邮件列表，十分重要，找资料，找工作
    * Tech-Talk 技术讨论
    * Core-Talk 内核开发讨论
    * 后两个已经失效
  - Bugs 提交bug
  - Documents
    * wiki 这部分资料注意时效
    *  CA 旧文档
    *  Training（十分重要），EPICS历次培训班资料
    *  Logo 各个大小的logo
- 学习途径
  - 一定在Linux上学习
  - 安装EPICS，可以参考组内安装手册
  - 看Training上的ppt，可以先看 APS EPICS Training, 2014 中的 Introduction to EPICS来入门
  - 做ioc开发：看Record Reference Manual
  - 做驱动开发：EPICS Application Developer's Guide
  - 做上层应用开发，需要接口：看Extensions
  - 遇到问题：找tech-talk的历史邮件或直接提问
  - 找课题灵感：看Collaboration Meetings
- EPICS V4资料
  - 由于epics7还在开发中，这部分资料比较杂乱，不成系统，主要可以参考的资料包括
  - EPICS V4 Developer's Guide：http://epics-pvdata.sourceforge.net/informative/developerGuide/developerGuide.html
  - pvAccess Protocol Specification，http://epics-pvdata.sourceforge.net/pvAccess_Protocol_Specification.html，pvAccess协议细节
  - EPICSv4 Overview and Architectures，http://epics-pvdata.sourceforge.net/arch.html，EPICS V4的软件结构等
  - EPICS V4 Normative Types，http://epics-pvdata.sourceforge.net/alpha/normativeTypes/normativeTypes.html
  - 各个模块的API文档：http://epics-pvdata.sourceforge.net/literature.html#swdoc（有C++和Java两种）
  - 可以参考我毕业论文第二章内容

  

- 其它资料
  - 

## 找文献
- jacow：加速器各个会议文章汇总：http://www.jacow.org/，也可看到将要召开的会议时间和地点
  - IPAC 加速器会议
  - ICALEPCS：控制会议
  - PCaPAC：控制workshop
- cnki 中国知网
- 万方：查找学位文章：http://www.wanfangdata.com.cn/index.html
- google 学术
- Web of Science https://www.webofknowledge.com/ 查sci文章

## 投文章
### 会议文章
- IPAC：投递时要选择审稿
- ICALEPCS
- PCaPAC
- 以上都要注意摘要提交时间，一般为为开会的前半年
### 期刊文章
- SCI
  - NIM-a
  - ieee transactions on nuclear science
  - 核技术(英文版) 
- EI和中文核心
  - 审稿的ipac
  - 原子能科学技术
  - 核电子学与探测技术
  - 强激光与粒子束

## 科研工具
- LaTeX
  - 写文章和毕业论文必备
  - 入门书籍《LaTeX入门》 刘海洋
  - 下载TexLive发行版（可以从科大镜像下载：http://mirrors.ustc.edu.cn/CTAN/），配合TexStudio使用
  - MAC用户可以使用MacTEX
  - 找模板：http://www.latexstudio.net/
  - 科大毕业论文模板：https://github.com/ustctug/ustcthesis
  - jacow投稿模板：http://www.jacow.org/Authors/LaTeX
  - 在线写作：https://www.overleaf.com/


# 生活
## NSRL生活
- 找老师和保修的通讯录：http://www.nsrl.ustc.edu.cn/10902/list.htm
- 师资队伍索引：http://www.nsrl.ustc.edu.cn/10920/list.htm
## USTC生活
- 中国科大网络资源一览：https://github.com/zzh1996/USTC-Network-Resources
  * 本链接值得详细看，认真看，仔细参考
  * 正版软件，可以下载windows、office、matlab等：ms.ustc.edu.cn







