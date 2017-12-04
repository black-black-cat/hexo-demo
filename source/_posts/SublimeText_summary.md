title: 记录一下 SublimeText 编辑器使用经验
date: 2017-01-19 15:16:01

---

## 简介
Sublime Text （ST）是一款跨平台的文本编辑器，支持基于Python的包（Package），可通过包扩充本身的功能。Sublime Text是专有软件，需要用户购买许可证注册使用，但可以免费试用且试用时长无限制。大多数的包使用自由软件授权发布，并由社区建置维护。

## 在 Windows 右键菜单中使用 ST

[注册脚本][1] 将文件保存为ANSI编码,生成的右键菜单中的中文标题就可以避免乱码

### 通过注册表添加右键菜单选项
sublime_addright.reg
```
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\*\shell\SublimeText3]
@="Open with SublimeText3"
"Icon"="D:\\Program Files\\Sublime Text 3\\sublime_text.exe,0"

[HKEY_CLASSES_ROOT\*\shell\SublimeText3\command]
@="D:\\Program Files\\Sublime Text 3\\sublime_text.exe \"%1\""


[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3]
@="Open with SublimeText3"
"Icon"="D:\\Program Files\\Sublime Text 3\\sublime_text.exe,0"

[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3\command]
@="D:\\Program Files\\Sublime Text 3\\sublime_text.exe \"%1\""
```

### 通过注册表删除右键菜单选项
sublime_delright.reg
```
Windows Registry Editor Version 5.00
[-HKEY_CLASSES_ROOT\*\shell\SublimeText3]
[-HKEY_CLASSES_ROOT\Directory\shell\SublimeText3]

```
上述的路径都要更改为sublime安装的实际路径
windows 10 系统中，给 `%1` 加上双引号，例如：
`@="D:\\Program Files\\Sublime Text 3\\sublime_text.exe \"%1\""`

[参考 百度经验][2]

##快捷键
>shift+鼠标右键拖动 ==> ctrl+shift+G：包围html标签
`ctrl+D`：先选中一个词，逐个重复选中相同的词
`alt+F3`：先选中一个词，全部选中相同的词
`ctrl+shift+D`：复制光标所在的一行到下一行，可重复操作
`ctrl+shift+left | right`：光标移到前（后）一个空标签的编辑区
`ctrl+shift+up | down` : 上下移动整行
ctrl+k+数字： 折叠该数字的层级
ctrl+k+j： 展开所有折叠
ctrl+shift+/： 多行注释
ctrl+shift+' : 选中html标签
ctrl+k k : 删除至行末
ctrl+k backspace : 删除至行首
ctrl + m : 跳转到括号的开头/结尾
ctrl + shift + m ： 选中括号中的全部内容
**F2大法**
ctrl + f2: 给**光标处***标上(移除)书签
f2: 下一个书签
shift + f2: 上一个书签
alt: 编辑全部标上书签（标上书签时光标所在之处）
ctrl + shift: 移除全部标签

#### 自定义快捷键
```
{ "keys":["ctrl+shift+c"], "command":"copy_path"},
{ "keys": ["alt+s"], "command": "save_all" },
// 触发自动缩进
{ "keys": ["alt+i"], "command": "reindent" }
```

#### 快速写标签
`$`：自动编号
`$@6*7`：从6开始自动编号，共7项
`$@-6*7`：逆序排列，以6为结尾，共7项
`（）+（）+（）`：加号表示并列结构

#### 插件
emmet：html与CSS高效编辑
docblockr:js语法检查
js and node.js snippet:快捷输入
lint:js语法检查

#### 跳出括号的设置
[此贴的21楼][3]
```
// 跳出括号
{"keys": ["enter"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
    [
        { "key": "following_text", "operator": "regex_contains", "operand": "^[)\\]\\>\\'\\\"\\ %>\\}\\;\\,]", "match_all": true },
        { "key": "preceding_text", "operator": "not_regex_match", "operand": "^.*\\{$", "match_all": true  },
        { "key": "auto_complete_visible", "operator": "equal", "operand": false }
    ]
}

```

#### 设置快速切换项目
```
// 设置快速切换项目
{ "keys": ["ctrl+alt+p"], "command": "prompt_select_workspace" }
```

#### package列表镜像
https://dn-52cik.qbox.me/channel_v3.json
[出处][4]
安装来源是github

## package
sftp -- 本地与服务器的文件传输，支持保存时上传。[参考][5]


## 代码规范
```
// soft tab 的意思是tab键转成4个空格
"tab_size": 4,
"translate_tabs_to_spaces": true,
```

## 其他
解决快捷键冲突的问题，试试windowsHotkeyExplorer
bz2问题
dependency-metadata.json
```
{"platforms": ["*"], "url": "https://github.com/codexns/sublime-bz2/issues", "version": "1.0.0", "description": "Python bz2 module", "sublime_text": "*"}
```
dependency-metadata.json
```
{"version": "1.0.0", "url": "https://github.com/codexns/sublime-bz2/issues", "platforms": ["*"], "description": "Python bz2 module", "sublime_text": "*"}
```


  [1]: https://my.oschina.net/adairs/blog/466777
  [2]: http://jingyan.baidu.com/article/cdddd41c68c32753ca00e157.html
  [3]: https://ruby-china.org/topics/4824
  [4]: http://www.cnblogs.com/52cik/p/Package-Control.html
  [5]: http://www.jianshu.com/p/bf7913f23d74