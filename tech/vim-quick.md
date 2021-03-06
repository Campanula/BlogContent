---
date: 2017-02-12T22:59:42+08:00
tags: ["vim"]
title: VIM速查表
topics: ""
---

## 前言

本文翻译自：`http://bencrowder.net/files/vim-fu/`，参考了 [VIM中文帮助](http://blog.aboutc.net/vim/8/vim-chinese-documentation)、 Google翻译结果和实际操作结果，对原文的部分内容重新整理，删除和添加了部分内容并加入了一些技巧。如有翻译不当或在实际操作中出现的任何问题都可以在文章后回复。

<!--more-->

> 注：
1. 文中以`:`开头为**命令行模式**，未注明均为**普通模式**。(了解vim模式`:help vim-modes`)
2. `<C-r>`意为`Ctrl + r`，其他同理。
3. 主要关注点：**光标的移动**，**文本的编辑**和**多文件的切换**。
4. 有两个不得不提的键:`<TAB>`**各种模式的下的补全**和`<ESC>`**各种模式下的切换**。无论你是使用什么终端，或是使用什么编辑器，这两个键都显得格外重要。

---

## 帮助
> `:help` 加载帮助
`:help j` 获取"j"命令的相关帮助
`:help :split` 获取":split"命令帮助
`:help z*` 获取以"z"开头的相关命令帮助
`:help function-list` 显示vim提供的函数列表

---
## 撤销,恢复和重复

> `u` 撤销(undo)
`<C-r>` 恢复撤销前的状态
`:redo` 恢复(同`<C-r>`)
`.` 重复最后一个命令
`[n][command]` 重复[n]次[command]命令
`:qa` 退出所有窗口
`:wqa` 保存退出所有窗口

---
## 移动光标：hjkl
>          ^
         k
    < h     l >
         j
         v

---
## 移动光标：行

> `0` 跳转到当前行首
`^` 跳转到当前行的第一个非空字符(空格/TAB)
`$` 跳转到当前行的末尾
`gg` 跳转到文件第一行(goto)
`G` 跳转到文件最后一行
`47G` 跳转到文件第47行
`:47` 跳转到文件第47行(同`47G`)

---
## 移动光标：字符

> `f[char]` 跳转到第一个[char]字符(find)
`3f[char]` 跳转到第三个[char]字符
`F[char]` 向左跳转到第一个[char]字符
`t[char]` 跳转到第一个[char]字符的前一个字符(till before - right)
`T[char]` 向左跳转到第一个[char]字符的后一个字符(till after - left)
`;` 重复最后一次的 f/F/t/T 移动命令


---
## 移动光标：单词和文本块

> `w` 跳转到下一个单词的开头(word)
`3w` 跳转到第三个单词的开头
`e` 跳转到下一个单词的结尾(end of word)
`b` 跳转到上一个单词的开头(backward beginning)
`(` 跳转到上一个句子的开头
`)` 跳转到下一个句子的开头
`{` 跳转到上一个段落的开头
`}` 跳转到下一个段落的开头

---
## 移动光标：代码块

> `%` 在当前大括号/中括号/小括号的开始位置`{/[/(`和结束位置`}/]/)`之间跳转
`[[` 跳转到上一个函数的开头(如果光标在函数体内则跳转到当前函数的开头)
`]]` 跳转到下一个函数的开头
`[{` 跳转到当前程序块的开头(当前程序块为当前程序的上一层，不是固定的)
`]}` 跳转到当前程序块的结尾

    更多移动光标命令请查看":help cursor-motions"

---
## 搜索

> `/[word]` 搜索[word]字符串
`?[word]` 向上搜索[word]字符串
`n` 跳转到下一个匹配的字符串(保持最后一个搜索命令的方向)(next match)
`N` 跳转到上一个匹配的字符串(保持最后一个搜索命令的方向)
`*` 搜索当前光标下的单词
`#` 向上搜索当前光标下的单词

---
## 插入模式
> `i` 在光标位置前进入插入模式
`I` 在当前行的第一个非空字符进入插入模式
`o` 在当前行的下一行添加一个空行进入插入模式
`O` 在当前行的上一行添加一个空行进入插入模式
`a` 在光标位置后进入插入模式
`A` 在当前行的末尾进入插入模式
`s` 删除光标位置下的字符并进入插入模式
`S` 删除当前行内容并进入插入模式

<br>

> 注：插入模式下使用 `<C-o>` 可以进入**插入普通模式**(窗口底部会由`-- INSERT --`变为`-- (insert) --`)，允许你执行完一个命令后，再返回插入模式。

> 如：在**插入模式**下选择保存在寄存器中的内容进行粘贴时，可以`<C-o>`, `:reg`, `<C-r>3`，其中：`:reg`是查看寄存器列表，`<C-r>3`是把寄存器列表中编号为`3`的内容粘贴在此处。

---
## 删除文本

> `x` 删除光标位置下的字符
`dw` 删除光标之后的单词剩余部分(delete word)
`diw` 删除一个单词
`dd` 删除当前行
`D` 删除从光标位置到当前行的末尾(同`d$`)
`df[char]` 删除从光标位置到[char]字符(delete find [char])
`d)` 删除从光标位置到下一个句子的开始
`d}` 删除从光标位置到该段落的末尾
`di{` 删除花括号之间的内容(delete inner {})(同`diB`)
`di(` 删除小括号之间的内容(delete inner ())(同`dib`)
`dit` 删除闭合标签之间的内容(html/xml等标签，delete inner tag)
`dat` 删除左右尖括号及之间的内容(delete a tag)
`da<` 删除左右尖括号及之间的内容(delete a <>)
`di"` 删除引号之间的内容(delete inner "")
`da"` 删除左右引号及之间的内容(delete a "")
`:5,10d` 删除5-10行
`3dd` 删除从当前行开始的3行
`<C-w>` 删除光标前的一个单词(插入模式)
`<C-u>` 从光标位置删除到行首(插入模式)

<br>

> 这里加 shift 大写，意为行尾
注：`d`/`c`开头的命令会将删除的文本放到寄存器(通过`:reg`查看)，可以理解为剪切。
关于"a"n和"i"nner可以参考`:help object-select`**文本对象选择**部分
另：一般向右的操作包含光标下的字符，向左的操作不包含光标下的字符

---
## 更改文本

> `J` 将下一行合并的当前行的末尾(Join line)
`3,9j` 合并3-9行
`~` 切换光标下字符的大小写
`u` 更改选定的文本为小写(可视模式)
`U` 更改选定的文本为大写(可视模式)
`<C-a>` 把当前光标下或之后的数值加1
`<C-x>` 把当前光标下或之后的数值减1
`r[char]` 替换光标下的字符为[char]. (replace)
`R` 进入替换模式
`cw` 删除光标之后的单词剩余部分并进入插入模式(change word)
`cc` 删除当前行内容并进入插入模式(同`S`)
`C` 删除从光标位置到当前行的末尾并进入插入模式(同`c$`)
`cf[char]` 删除从光标位置到[char]字符并进入插入模式

<br>

> 这里`c`开头加 shift 大写，意为行尾
`c`开头"change"更改(删除并插入)，`d`开头"delete"删除，和`y`开头"yank/copy"，格式相同，可相互参考使用

---
## 缩进文本

> `>>` 缩进当前行
`<<` 向左缩进当前行
`<C-d>` 缩进当前行(插入模式)
`<C-t>` 向左缩进当前行(插入模式)
`:3,9>>>>>` 将3-9行缩进5个TAB
`>` 缩进选定的行(可视模式)
`<` 向左缩进选定的行(可视模式)
`>i{` 缩进花括号之间的内容(indent inner {})(同`>iB`)
`>a{` 缩进花括号及之间的内容(indent a {})(同`>aB`)
`=}` 缩进当前段落
`gg=G` 全文缩进/格式化

---
## 复制和粘贴

> `v` 进入可视模式，以字符为单位选择
`V` 进入可视模式，以行为单位选择
`<C-v>` 进入列块可视模式(如果映射`<C-v>`为"粘贴"时请注意)
`gv` 重新选择最后选定的区域
`y` 抽出选择的文本到寄存器(可视模式)(yank/copy)
`"+y` 抽出选择的文本到系统剪切板(可视模式)(好像不太好使)
`:co 10` 复制当前行到第11行(copy)
`:co` . 复制当前行到下一行(同`yyp`)
`:5,10co 20` 复制5-10行到第21行
`yy` 复制当前行
`y$` 复制到行尾
`yw` 复制光标之后的单词剩余部分(yank word)
`yb` 复制光标之前的单词剩余部分
`yiw` 复制一个单词
`yip` 复制当前段落(yank inner paragraph)
`yas` 复制一个句子(yank a sentence)
`yi<` 复制尖括号之间的内容(Yank inner <>)
`11y` 复制11行
`p` 粘贴(paste)
`P` 粘贴到光标前
`<C-r>"` 粘贴(插入模式)
`"ayy` 复制当前行到寄存器"a"(可使用范围"a-z")
`"ap` 粘贴从寄存器"a"

---
## 文件和目录

> `:e!` 重新载入当前文件，放弃任何更改(edit)
`:e [file]` 编辑文件[file]
`:r [file]` 将[file]文件内容插入到下一行(read)
`:r !date` 将"date"命令返回的结果插入到下一行
`:pwd` 输出当前工作目录到状态栏
`:cd [dir]` 切换当前工作目录到[dir]
`<C-g>` 显示当前文件信息(文件名及行数等)
`gf` 打开光标下的文件路径(相当于以`:e`的方式打开)
`ga` 显示光标下的字符在当前使用的 encoding 下的内码
`:saveas [file]` 另存为[file]文件(文件不存在，使用`:saveas!`覆盖已存在文件)
`:w > [file]` 将当前文件内容写入[file]文件(文件不存在，同`:saveas`)
`:3,9w >> [file]` 将3-9行的内容追加到[file]文件(文件已存在)
`:w` 保存当前文件
`:x` 保存并退出
`:q!` 不保存退出
`:qa!` 强行退出所有文件，不保存

> `:sh`  切换到shell终端，使用`<C-d>`返回
`<C-z>` 同上，使用`fg`返回(属终端快捷键范畴)

---
## 缓冲区

> `:ls` 查看缓冲区列表(同 `:files`, 或 `:buffers`)
`:bn` 编辑下一个缓冲区(buffer next)
`:bp` 编辑上一个缓冲区(buffer previous)
`:b[n]` 编辑缓冲区列表中第[n]个缓冲区
`:b <Tab>` 选择要切换的 buffer 文件
`:bd` 卸载当前缓冲区(buffer delete)

---
## 分割窗口

> `:sp` 水平分割当前窗口(split)
`:vs` 垂直分割当前窗口(vertical split)
`:sp [file]` 水平分割一个新窗口，并编辑文件[file]
`:close` 关闭当前窗口(同`:q`)
`:only` 关闭其他窗口
`<C-w> h` 光标移动到左边一个窗口
`<C-w> j` 光标移动到下边一个窗口
`<C-w> k` 光标移动到上边一个窗口
`<C-w> l` 光标移动到右边一个窗口
`<C-w> w` 光标移动到下一个窗口

---
## 标签页

> `:tabs` 查看标签页列表
`:tabe` 打开一个新标签页(tab edit)(同`:tabnew`)
`:tabe` [file] 打开一个新标签页，并编辑文件[file].
`:tabc` 关闭当前标签页(tab close)(同`:q`)
`gt` 转到下一个标签页(go to)(同`:tabn`/`:tabnext`)
`gT` 转到上一个标签页(同`:tabp`/`:tabprevious`)

---
## 滚屏

> `H` 跳转到屏幕的顶部(home)
`M` 跳转到屏幕的中间(middle)
`L` 跳转到屏幕的底部(low)
`zt` 将当前行滚动至屏幕顶部(top)
`zz` 将当前行滚动至屏幕中间(同`z.`)
`zb` 将当前行滚动至屏幕中间(bottom)(同`z-`)
`<C-f>` 滚动至下一页(forwards)
`<C-b>` 滚动至上一页(backwards)
`<C-d>` 向下滚动半屏(downwards)
`<C-u>` 向下滚动半屏(upwards)

---
## 折叠

> `3zF` 创建折叠操作符，并折叠3行
`zo` 打开光标下的折叠(open)
`zc` 关闭光标下的折叠(close)
`zR` 打开所有的折叠
`zd` 删除光标下的折叠操作符(delete)

---
## 自动完成

> `<C-n>` 自动完成当前的单词
`<C-p>` 自动完成当前的单词，光标定位在自动完成列表的最后一行
`<C-x><C-o>` 使用"Omnicomplete"全能补全函数(:help omnifunc)(同`<C-x-o>`)

---
## 标记和历史

> `ma` 在当前光标位置设置位置标记(可使用范围"a-zA-Z")
``a` 跳转到"a"标记
`g;` 转到上一次编辑的地方
`:his` 查看执行的命令历史记录(默认参数为"c"即"cmd")
`:his s` 查看搜索字符串的历史记录(history search)
`:his a` 查看包括搜索/命令等所有历史记录(了解更多参数`:help :history`)

---
## 键映射

> `:map` 查看已映射的键列表
`:imap` 查看插入模式下已映射的键列表
`:nmap` 查看普通模式下已映射的键列表
`:imap jj <Esc>` 插入模式下键入`jj`映射到`<ESC>`(返回普通模式)
`:nmap <C-h> <C-w>h` 普通模式下映射`<C-h>`到`<C-w>h`(光标移动到左边一个窗口)

---
## 替换

> `:%s/w1/r2/g` 将文件中所有的"w1"替换为"r2"
`:.,$s/w1/r2/g` 将当前行到文件末尾所有的"w1"替换为"r2"
`:s/w1/r2/g` 将当前行中所有的"w1"替换为"r2"(同`:g/w1/s//r2/g`)
`:3s/w1/r2/g` 将第3行到文件末尾所有的"w1"替换为"r2"
`:3,9s/w1/r2/` 将3-9行第一个"w1"替换为"r2"
`:3,9s/^/#/` 将3-9行行首添加"#"号(可用于注释)
`:3,9s/^/\/\//` 将3-9行行首添加`//`双斜线
`:3,+3s/^#//` 将第3行及其后3行行首的"#"号去掉
`:.-3s/^/#/` 将当前行上的第三行行首添加"#"号

> `:g/print/d` 删除包含"print"字符串的所有行
`:g!/print/d` 删除不包含"print"字符串的所有行
`:%s/\s\+$//` 去除行尾空白字符(`\s`表示空白字符`空格/TAB`，`\+`表示一个或多个)
`:%s/^\([a-z]\)/\U\1/` 首字母大写(`\1`表示第一个`\(`和`\)`之间的匹配文本)
`:g/^$/,/./-j` 压缩空行
`:%s/^M$//` 去除行尾的`^M` (`^M`使用`<C-v><C-m>`录入)
`:%s/^I//` 删除文件所有行的第一个`TAB`(`^I`使用`TAB`键录入)
`:%s/^\d.//` 删除文件所有行行首的数字和"."(如：`5.`)
