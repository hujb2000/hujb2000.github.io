---
layout: post
title:  "Shell Script Guides"
date:   2015-12-01 13:35:30
categories: allen.hu update
---



# 背景知识

简单就是力量: Power cloaked in simplicity.

对常用标准工具组与选项的需求终于明朗化,POSIX标准即为最后的结果, POSIX并非UNIX标准化的唯一结果,POSI之外另外其它标准.

* 软件工具的原则

1. 一次做好一件事

在很多方面,这都是最重要的原则.

2.  使用正则表达式

两种正则表达式:
用于grep一致的正则达式(POSIX称之为基本型表达式,Basic Regular Expressions, BRE), 或是用用于egrep一致的正则表达式(POSIX称之为扩展型正则表达式,
Extended Regular Expressions,ERE).

3. 避免喋喋不休

UNIX工具程序一向遵循"你叫它做什么，你就会得到什么"的设计哲学.

# 入门

* 自给自足的脚本, 位于第一行的#!

当Shell执行一个程序时,会要求UNIX内核启动一个新的进程(process),以便在该进程里执行所指定的程序.

* shell的基本元素

1. 命令与参数
2. 变量
myvar=thiis_is_a_long_string;
echo $myvar

先写变量名称,紧接着=字符,最后是新什,取出变量时需要于变量前加下$字符,当所赋予的值内容空格时,请加上引号
fullname= "$fist $middle $ last"
3. 华丽的printf输出
printf不像echo那样会自动提供一个换行符号,你必须显式地将换行符号指定成\n.

4. 重定向
< 改变标准输入
> 改变标准输出
>> 附加到文件
| Pipe

5. 特殊文件:/dev/null /dev/tty
/dev/null就是大家所知道的位桶(bit bucket),传udup到此文件的数据都会被系统丢掉.

5.查找命令
用两个连续的冒号来表示,如果将冒号直接置于最前端或尾端,可以分别表示查找时最先查找或最后查找当前目录 .

6. 访问shell脚本参数
基于历史的原因,当它超过9,就应该用大括号把数字框起来
echo first arg is $1
echo tenth arg is ${10}

7. 简单的执行跟踪
用set -x 命令执行跟踪的功能打开,然后再用set +x命令关闭

8. 国际化
internationalization i18n, localization 110n

LANG: 未设置任何LC_XXX变量时所使用的默认值,
LC_ALL: 用来覆盖掉所有其他LC_XXX变量的值
对local的支持,某些需要300MB的文件系统.

# 替换与查找

1992, POSIX标准将grep,egrep,fgrep三个改版整合成一个grep程序, 它的行为是通过不同的选项加以控制的.

* 简单的grep
who | grep hujiabao

^tolstory: 一行的开头
tolstory$: 一行的结尾

* 在文件里进行替换

执行文件替换的正确程序应该是set

sed -i "s/default_server//" /etc/nginx/nginx.conf


ONBUILD指令在本Dockerfile不起作用, 等下一个包含该镜像指令的时候执行

docker run -it --entrypoint= 来覆盖Dockerfile里ENTRYPOINT指令

