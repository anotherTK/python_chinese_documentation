# 使用Python解释器

## 2.1 启动编译器

python 解释器通常安装在/usr/local/bin/python3.7，将/usr/local/bin放入Unix shell的搜索路径，通过下面的命令启动：
```
python3.7
```
因为解释器所在目录的选择是安装选项，所以其他的位置也是可能的。

在windows机器上，python安装路径一般是C:\python337，但你可以改变路径当你安装的时候。为了增加该路径在系统路径中，你可以在dos窗口中输入下面的命令：
```
set path=%path%;c\python37
```
输入终止符退出解释器。如果没有正常工作，可以输入quit()命令。

解释器的线编辑特性包含互动编辑，历史替换以及代码补全。可能最快的检查是否支持线编辑是输入Control-P看是否有动作。如果没有什么发生，则不支持。

解释器操作起来有点像Unix shell，当被连接到tty设备的标准输入调用时，它读取并执行命令。当通过文件名和参数调用时，它读取并执行那个文件中的脚本。

第二中方式启动解释器的方法是```python -c command [args]```，这样会执行command里面的语句家，类似shell的-c选项。因为python语句经常包含空格和其他字符（对于shell有点特殊），建议采用单引号引用command。

一些python模块也和脚本一样用，通过一下命令唤起，
```
python -m module [args] ...
```
这样能够执行模块里面的源文件。

当使用脚本文件时，增加-i选项有时是有帮助的，这样在执行脚本文件后，进入交互模式。

### 2.1.1 参数解析

熟悉了解释器后，脚本的名称和额外的参数都被转换成一个字符串的列表并复制给argv变量（在sys模块中）。你能够获得这个列表通过import sys. 这个列表的长度最少是1， 当没有脚本和参数给定，sys.argv[0]是空字符串。当脚本的名称是‘-’，表示标准输入，sys.argv[0]设置为‘-’。当使用-c选项，sys.argv[0]设置为‘-c’。当-m模块使用，sys.argv[0]设置为模块的全名。在-c和-m选项后的其他参数不会被脚本解释器处理，但保留在sys.argv变量中。

### 2.1.2 交互模式

当命令从tty中读取，解释器被说成是交互模式。在这个模式下执行下一条命令，开始采用主要提示，三个大于号。对于连续行，采用次要提示，三个点。解释器打印欢迎信息，表明其版本号和授权书。

当输入多行代码需要连续行。

## 2.2 解释器和环境
### 2.2.1 源代码编码

默认地，python源文件都是采用utf-8编码，这样全世界绝大部分的语言都能同时采用字符串，定义符和注释。即使标准库只使用ascii字符，这是任何便携式代码都应遵守的一条惯例。为了正确的显示这些字符，你编辑器必须识别utf-8编码的文件。并且必须使用一种能够显示所有字符的字体。

为了声明区别于默认的编码方式，一个特殊的注释文件应该被添加到文件的第一行，语法如下所示：
```
# -*- coding: encoding -*-
```
其中的encoding是一种python支持的编码方式。

一个特殊情况是，当源代码开始以申明Unix shell的文件方式，那么编码申明放在第二行：
```
#!/usr/bin/env python3
# -*- coding: encoding -*-
```