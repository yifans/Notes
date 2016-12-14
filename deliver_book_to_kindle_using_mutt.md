# Deliver Book to kindle Using Mutt

今天了解了使用邮箱推送的方式给 Kindle 中上传书籍的方式，为了方便上传，写了一个 shell 脚本完成这一功能

## 步骤
### 安装 `mutt`

`sudo apt install mutt`
安装过程均使用默认设置

### 配置`mutt`
在家目录下建立文件 .muttrc
写入如下配置
```
## set email address and username
set from = "i@yifans.me"
set realname = "Yifan Song"
set use_from = yes
## 发送文件后不保存副本，否则会在家目录下生成`sent`文件
set copy=no
```

## 编写脚本`send_mail.sh`
内容为：
```
#!/bin/bash

if [ -z "$1" ]; then
    echo "Please input the book path"
else
    echo "Deliver book to kindle" | mutt -s "Deliver book to kindle" -c *****@qq.com  *****@kindle.cn -a "$1"
fi
```

解释
- `$1` 传递给脚本的第一个参数，用于指定文档路径，若不指定，会给出提示
- `echo "Deliver book to kindle"` 邮件内容
- `-s` 邮件主题
- `-c` 抄送
- `-a` 附件
- `****@kindle.cn` 为亚马逊的邮箱地址

## 批准电子邮箱

要批准此发件人的电子邮件地址：

- 访问管理您的内容和设备页面。
- 登录亚马逊帐户。
- 进入“管理您的内容和设备”下的“个人文档设置”。
- 在“获批准的个人文档电子邮件列表”下，点击“添加一个已获得批准的电子邮件地址”。
- 输入要审批的电子邮件地址，然后选择“添加地址”。

## 使用
- 执行
`./send_mail.sh a.mobi`
- 会将文件`a.mobi`作为附件发送至亚马逊邮箱，同时抄送一份到qq邮箱

## 上传成功
- 稍等一会儿，待上传完毕
- 在亚马逊kindle商店，“管理我的设备”，“我的内容”，“个人文档”下，可以找到刚才上传的文件。
