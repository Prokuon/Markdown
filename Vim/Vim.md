# Vim

## 第01章

1.1 移动光标

*  `h、j、k、l` 移动光标

```
        ^
        k		    提示： h 的键位于左边，每次按下就会向左移动。
    < h   l >		      l 的键位于右边，每次按下就会向右移动。
        j			      j 键看起来很象一支尖端方向朝下的箭头。
        v
```

### 1.2 Vim进入与退出

* 退出 Vim 编辑器
     *  `:q!`  <回车> 放弃所有改动
     *  `:wq`  <回车> 保存改动

### 1.3 文本编辑之删除

* `x` 在正常模式下删除光标所在位置的字符

### 1.4 插入或添加文本

* `i` 输入欲插入文本 <ESC> 在光标前插入文本
* `A` 输入欲添加文本 <ESC> 在一行后添加文本

## 第02章

### 2.1 删除类命令

* `dw` 从当前光标删除至下一个单词
* `d$` 从当前光标删除至当前行末尾
* `dd` 删除整行

### 2.2 命令与对象

* 在正常模式下修改命令的格式是：
  * `operator   [number]   motion`
  * 其中：
    * `operator` - 操作符，代表要做的事情，比如 d 代表删除
    * `[number]` - 可以附加的数字，代表动作重复的次数
    * `motion`   - 动作，代表在所操作的文本上的移动，例如 w 代表单词(word)，
    * `$` 代表行末等等。

### 2.3 使用计数指定动作

* 欲重复一个动作，需在它前面加上一个数字，例：`2w`

### 2.5 操作整行

* `0` ==移动光标到行首==
* `dd` ==删除整行==

### 2.6 撤销类命令

* `u` ==撤消以前的操作==
* `U` 撤消在一行中所做的改动
* `CTRL-R` 撤消以前的撤消命令，恢复以前的操作结果

## 第03章

### 3.1 置入类命令

* `p` ==重新置入==已经删除的文本内容
  * 该操作可以将已删除的文本内容置于光标之后。	
  * 如果最后一次删除的是一个整行，那么该行将置于当前光标所在行的下一行。

### 3.2 替换类命令

* 要替换光标所在位置的字符，输入小写的 `r` 和要替换掉原位置字符的新字符即可。

### 3.3 更改类命令

*  更改类命令允许您改变从当前光标所在位置直到动作指示的位置中间的文本。
  * `ce` 或 `cw` 可以==替换当前光标到单词的末尾的内容==
  * `c$` 可以==替换当前光标到行末的内容==
  * 格式：`c   [number]   motion`

## 第04章

### 4.1 定位及文件状态

* `CTRL-G` 显示当前编辑文件中当前光标所在行位置以及文件状态信息
* `G` 可以使得当前光标直接跳转到文件==最后一行==
* `gg` 可以使得当前光标直接跳转到文件==第一行==
* `number + G` 跳转至==指定行==

### 4.2 搜索类命令

* `/ + string` ==查找字符串==
  * `n` 查找下一个
  * `N` 查找上一个
* `? + string` ==逆向查找==字符串

### 4.3 配对括号查找

* `%` 查找==匹配括号== `)、]、}`

### 4.4 替换命令

* `:s/old/new` 在==一行内替换头一个==字符串 old 为新的字符串 new
* `:s/old/new/g` 在==一行内替换所有==的字符串 old 为新的字符串 new
* `:#,#s/old/new/g` 在==两行内替换所有==的字符串 old 为新的字符串 new
* `:%s/old/new/g` 在==文件内替换所有==的字符串 old 为新的字符串 new
* `:%s/old/new/gc` 进行==全文替换时询问==用户确认每个替换需添加 `c` 标志

## 第05章

### 5.1 在 VIM 内执行外部命令

* `:! command` 执行外部命令
  * `:!ls` 显示当前目录内容
  * `:!rm FILENAME` 删除文件
* `:w FILENAME` 将当前文件保存到FILENAME文件中
* `v motion :w FILENAME` 将当前编辑文件中可视模式下选中的内容保存到文件
  FILENAME 中
* `:r FILENAME` 可提取磁盘文件 FILENAME 并将其插入到当前文件的光标位置后面
* `:r !dir` 可以读取 dir 命令的输出并将其放置到当前文件的光标位置后面

### 第06章
