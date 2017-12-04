---
title: Windows 命令行
date: 2017-01-17 11:06:35
tags:
---

查看帮助的参数 `/?`

```bat
:查看端口占用
netstat -aon | findstr "80"

:根据pid查看任务
tasklist | findstr "9988"

:根据程序名字
tasklist | findstr "chrome"

pip list | findstr "Jinja"

:根据imagename，杀进程，强制的 /f
taskkill /f /im chrome*

rmdir (rd)
mkdir (md)

type nul > example.txt
del example.txt

```

## 文件夹缩写
用缩写处理文件夹名中的空格
六个字母加波浪加序号，首个单词不足六个字母则省掉空格拼上接下来的单词
同一缩写对应多个文件夹时，序号可以标识出指定文件夹。
例如
program files --> progra~1
program files(86) --> progra~2
```python
sampleFile = os.path.join('C:\Progra~1\Micros~1\Office15\\2052', 'PROTTPLV.PPT')
getDir('C:\Progra~2\Google\Chrome\Application', 'chrome.exe')
```

## cmder

* Cmder.exe所在目录加入环境变量的PATH
* 资源管理器右键菜单注册Cmder打开：打开cmder，输入`cmder.exe /register all `

没加环境变量的话

* Open a terminal as an Administrator
* Navigate to the directory you have placed Cmder
* Execute .\cmder.exe /REGISTER ALL If you get a message "Access Denied" ensure you are executing the command in an Administrator prompt.