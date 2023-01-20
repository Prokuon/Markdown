# Qt类帮助文档翻译

>- 以QPushButton为例对Qt帮助文档进行了翻译
>
>- 对一些关键词汇进行了总结与汇总

## Contents

- [Properties](# Properties)	属性
- [Public Functions](#Public-functions)   公有成员函数
- [Reimplemented Public Functions](#Reimplemented-Public-Functions)   重新实现的公共成员函数
- [Public Slots](#Public-Slots)   公共槽函数
- [Protected Functions](#protected-functions)   受保护的成员函数
- [Reimplemented Protected Functions](#reimplemented-protected-functions)   重新实现的受保护的成员函数
- [Detailed Description](#Detailed-Description)   详细说明

# QPushButton Class

The QPushButton widget provides a command button. [More...](#details)

> QPushButton 小部件提供了一个命令按钮

​		Header（头文件）:	`#include<QPushButton>`
​		qmake:	 `QT += widgets`
​		Inherits（继承）:	QAbstractButton
Inherited By（被继承）:	QCommandLinkButton

- List of all members, including inherited members 

> - 所有成员的列表，包括被继承的成员

## Properties

- autoDefault : bool
- default : bool
- flat : bool 

> [QPushButton的default和autoDefault 属性](https://blog.csdn.net/yaowangII/article/details/84580597)

## Public Functions

| 返回值  |                                                              |
| ------- | ------------------------------------------------------------ |
|         | QPushButton(const QIcon &*icon*, const QString &*text*, QWidget **parent* = nullptr) |
|         | QPushButton(const QString &*text*, QWidget **parent* = nullptr) |
|         | QPushButton(QWidget **parent* = nullptr)                     |
| virtual | [~QPushButton](qpushbutton.html#dtor.QPushButton)()          |
| bool    | [autoDefault](qpushbutton.html#autoDefault-prop)() const     |
| bool    | [isDefault](qpushbutton.html#default-prop)() const           |
| bool    | [isFlat](qpushbutton.html#flat-prop)() const                 |
| QMenu * | [menu](qpushbutton.html#menu)() const                        |
| void    | [setAutoDefault](qpushbutton.html#autoDefault-prop)(*bool*)  |
| void    | [setDefault](qpushbutton.html#default-prop)(*bool*)          |
| void    | [setFlat](qpushbutton.html#flat-prop)(*bool*)                |
| void    | [setMenu](qpushbutton.html#setMenu)(QMenu **menu*)           |

## Reimplemented Public Functions

| 返回值        |                                                              |
| ------------- | ------------------------------------------------------------ |
| virtual QSize | [minimumSizeHint](qpushbutton.html#minimumSizeHint)() const override |
| virtual QSize | [sizeHint](qpushbutton.html#sizeHint)() const override       |

## Public Slots

void	showMenu()

## Protected Functions

void	initStyleOption(QStyleOptionButton *option) const

## Reimplemented Protected Functions

| 返回值       |                                                              |
| ------------ | ------------------------------------------------------------ |
| virtual bool | [event](qpushbutton.html#event)(QEvent **e*) override        |
| virtual void | [focusInEvent](qpushbutton.html#focusInEvent)(QFocusEvent **e*) override |
| virtual void | [focusOutEvent](qpushbutton.html#focusOutEvent)(QFocusEvent **e*) override |
| virtual void | [keyPressEvent](qpushbutton.html#keyPressEvent)(QKeyEvent **e*) override |
| virtual void | [paintEvent](qpushbutton.html#paintEvent)(*QPaintEvent* *) override |

## Detailed Description