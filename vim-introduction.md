# 有关Vim的一些简单介绍

## Vim的历史

1991年，荷兰的Bram MoolenaarBram正式发布了Vim。最开始(1998年)只是单纯地复制开源的vi,当时Vim还是Vi IMitation的简称。1992年，Vim被移植到Unix和MS-DOS上，这时候Vim的全名才变成了Vi IMproved。


## Vim的基本介绍及Suger

Vim编辑器功能虽强大，但同时不得不承认其陡峭的学习曲线。初学者往往认为这个编辑器太难用，已有的编辑器那么多，完全没必要花那么多时间经历学习它，而熟练使用者则将它看作瑞士军刀，不管编辑任何文本，首先考虑的都是它。至于有没有学习的必要，只有用过之后才知道。


### Vim的常用操作

1. 移动

h,j,k,l   左，下，上，右
w         以单词为单位向右移动光标 eg:5w
W         与w类似，只是不把符号或标点当作单词处理
b         以单词为单位向左移动光标
B         与b类似，只是不把符号或光标当左单词处理
e         与w类似，只是光标在单词末尾
E         与e类似，忽略其他边界字符

^         光标移动到该行第一个非空字符处
0         光标移动到该行行首
$         光标移动到该行行尾
gg        光标移动到文件首行
G         光标移动到文件末尾


2. 插入

i         在当前光标前进入插入模式
I         在当前行行首进入插入插入模式
a         在当前光标后进入插入模式
A         在当前行行尾进入插入模式
o         在光标下方的新行进入插入模式
O         在光标上方的新行进入插入模式
:r !date  在光标处插入当前日期与时间(read the output from running the **date** utility, inserting the result after the current line)


3. 删除

x         删除光标所在位置字符 eg:5x
dd        删除当前行
dw        删除光标所在处的单词
D         删除至行尾


4. 替换

r         替换光标所在处的一个字符
R         替换光标所在处的字符，直到按下`ESC`键为止(进入替换模式)


5. 复制与粘贴

y         复制
yw        复制一个单词
yy        复制当前行
p         粘贴缓冲区内容到光标所在处

6. 撤销

u         撤销最后一次命令的执行
ctrl+r    redo


### Vim的模式

用惯GUI编辑器后转向Vim最不能忍受的就是它的操作方式了，以前`Ctrl+S`就能搞定，现在得通过`:w`保存，鼠标等也不能方便的定位。而Vim下的一系列操作都离不开**模式**。Vim常用的模式有：

- Normal Mode
- Insert Mode
- Visual Mode
- CommandLine Mode/Ex Mode

下面重点介绍Ex Mode。
Vim的底层其实是行编辑器ex。从Vim的Nomal模式输入`Q`进入Ex Mode,在Ex模式输入`vi`返回到Normal模式。

**Ex Mode的用处**

- delete 缩写为d
- move 缩写为m
- copy 缩写为t/co

Ex模式下的操作需要指定行来执行命令。指定行的方式有三种：

- 绝对行号
- 相对位置
- 搜索匹配的位置

**绝对行号**
`5,15d`   删除5到15行的内容
`5,15m0`  将5到15行的内容移到0行后面(即开始位置)
`5,15t1`  将5到15行的内容拷贝到第1行后面

`.`表示当前行,`$`表示最后一行，`%`表示每一行，相当于`1,$`。
`%d`     删除所有行
`%t$`    拷贝所有行到末尾

**相对行号**
`5,.m$`  将5到当前行的内容移动到末尾

`+`和`-`放在数字中间时，表示数字范围
`5,.m$-5` 将5到当前行内容移动到文件末尾的前5行

**搜索的匹配位置**
`/pattern/d`      删除光标后第一个匹配行
`/pattern/+d`     删除光标后的第一个匹配行的下一行
`/pattern/,$m1`   拷贝光标后的第一个匹配行到末尾的内容到第一行后面
`/pattern1/,/pattern2/d`  删除光标后模式1的第一行到模式2的第一行

`g`代表全局范围,针对所有的匹配
`g/pattern/d`     删除文件的所有匹配行
`g!/pattern/d`    删除除文件匹配行的其他行

**Ex模式其他用法**
`5,$w newfile`      将5到末尾的内容保存到新文件中
`5,15w >>otherfile` 将5到15行内容追加到另一文件
`r filename`        将目标文件内容插入到光标下
`5r /path/filename` 将目标文件内容插入到第5行下

`x`    保存并退出
`w`    保存
`q`    退出

**注：**使用`x`，如果文件没有被修改，则其修改时间不变，而`wq`则不管文件是否修改过，都会写入新的修改时间


### Sugers

:s/old/new/g      将当前行的所有old都替换成new,没有g则只替换第一个
:#,#s/old/new/g   将给定两行间的的所有old替换为new。#代表行号 eg:1,5s/old/new/g
:%s/old/new/g     将文件中所有old替换为new
:%s/^/xxx/g       在每行行首插入xxx
:%s/$/xxx/g       在每行行尾插入xxx

da[               删除[]之间文本(包含[)
di[               删除[]中的文本(不包括[])

da"               删除""之间为本(包含")
di"               删除""中的文本（不包括""）

daw
diw

dat               删除Html/Xml标签内的文本(包含标签)
dit               删除Html/Xml标签内的文本(不包含标签)

dap               删除光标所在段落（包含段后的空行）
dip               删除光标所在段落(不包含段后的空行)

va{               选中{}之间的内容(包括{})
vi{               选中{}之间的内容(不包括{})

ca(
ci(

**注：**`[`、`"`等符号可替换为其他

gi                跳转到上次编辑的地方
`>>`              缩进
`<<`              取消缩进
`==`              对齐
`gg=G`            全文对齐
`=i{`             对齐{}之间的文本

### 寄存器

寄存器类型很多，具体可通过:help registers查看，这里只介绍3种：

- 默认寄存器(Unamed Register)
- 数字寄存器(Numbered Register)
- 命令寄存器(Named Register)

**默认寄存器**
默认寄存器又称无名寄存器，使用y、d、x、c、s等命令时，对应的文本会自动放入该寄存器。即使在复制或删除文本时，已经指定了其他的寄存器(eg:"ayy)，这些文本仍然会同时存放在默认寄存器。

**数字寄存器**
数字寄存器有10中，编号从0到9，并且都以`"`开头，通过`reg`可查看各寄存器内容。
"0      保存最近复制的文本
"1      保存最近删除的文本，除非删除内容少于一行
"2      保存倒数第二次删除的文本，除非删除内容少于一行
"3-"9 依次类推

**命名寄存器**
命名寄存器，也称字母寄存器。从`"a`到`"z`,`"A`到`"Z`。其中小写的会替换掉以前寄存器内容，而大写的则会在原寄存器内容上追加。eg:`"ayy`复制当前行到`"a`中，然后`"ap`粘贴`"a`寄存器中的内容到当前处。


## Vimrc的基本配置

<leader>的存在是为了防止和已有的命令冲突，所以在映射的命令前加个leader前缀。

有关autocommands的详细内容，请通过`:help usr_40.txt`查看。

>An autocommand is a command that is executed automatically in response to some event, such as a file being read or written or a buffer change.

>Autocommands are a way to tell Vim to run certain commands whenever certain events happen.

Autocommand格式如下：

	:autocmd [group] {events} {file_pattern} [nested] {command}

- [group] and [nested] are optional.
- {events} parameter is a list of events(comma separated) that trigger the command.
- {file_pattern} is a filename, usually with wildcards.
- {command} is the command to be executed.

可通过`help autocmd-events`查看完整的event列表。
常见的有BufNewFile,BufWritePre,BufRead,FileType等。

    :autocmd BufRead,BufNewFile *.rb set shiftwidth=2

当读取或者新建.rb文件时，会自动地设置缩进为2。查看完整的event列表。
常见的有BufNewFile,BufWritePre,BufRead,FileType等

**Delete autocommand**
>To delete an autocommand, use the same command as what it was defined with, but leave out the {command} at the end and use a !.

Example:

    :autocmd! FileWritePre *

This will delete all autocommands for the "FileWritePre" event that use the "*" pattern.

**List defined autocommands**
>To list all the currently defined autocommands, use `autocmd`.

但列表可能太长，可以只列出给定group/event/pattern的autocommands.例如，只列出所有的BufNewFile autocommands:

	:autocmd BufNewFile

要列出所有.c有关的autocommands,可用：

	:autocmd * *.c


## Vim 插件介绍

Vim基于KISS(Keep It Simple Stupid)原则，具有强大的扩展功能，每个扩展功能可以以插件的形式来展现，而插件则实际上只是一个用Vim script编写的文本文件，并在Vim启动时自动加载这些文本文件。

插件分为两类：

1. 全局插件

适用于所有的文件

2. 文件类型插件

适用于某些具体类型的文件


## Vim学习资料

1. Vim文档(通过:help user-manual查看)
2. [Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/)
