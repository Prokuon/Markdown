<<<<<<< HEAD
# Qt 实用手册

- [(1条消息) QT的延时函数_雪山飞狐W的博客-CSDN博客_qt延时函数](https://blog.csdn.net/qq_41429220/article/details/96627952)

- [(1条消息) 55黑马QT笔记之关闭子线程_Mango酱的博客-CSDN博客_qt 关闭子线程](https://blog.csdn.net/weixin_44517656/article/details/107139552)

- [Qt 一个信号对应多个槽，多个信号对应一个槽的执行顺序 - 一杯清酒邀明月 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ybqjymy/p/14636939.html#:~:text=Qt独创的信号槽,一对多或多对一。)

## 一 时间

## 1. 返回当前时间的格式化字符串

~~~c++
/// 返回当前时间的格式化字符串
QString currentTimeStr(void)
{
    QString t = QTime::currentTime().toString("[ hh:mm:ss.zzz ]");
    return t;
}
~~~

## 2. 延时函数

~~~c++
void delayms(int msec)
{
    QEventLoop loop;
    QTimer::singleShot(msec,&loop,&QEventLoop::quit);
    loop.exec();
}
~~~

=======
# Qt 实用手册

- [(1条消息) QT的延时函数_雪山飞狐W的博客-CSDN博客_qt延时函数](https://blog.csdn.net/qq_41429220/article/details/96627952)

- [(1条消息) 55黑马QT笔记之关闭子线程_Mango酱的博客-CSDN博客_qt 关闭子线程](https://blog.csdn.net/weixin_44517656/article/details/107139552)

- [Qt 一个信号对应多个槽，多个信号对应一个槽的执行顺序 - 一杯清酒邀明月 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ybqjymy/p/14636939.html#:~:text=Qt独创的信号槽,一对多或多对一。)

## 一 时间

## 1. 返回当前时间的格式化字符串

~~~c++
/// 返回当前时间的格式化字符串
QString currentTimeStr(void)
{
    QString t = QTime::currentTime().toString("[ hh:mm:ss.zzz ]");
    return t;
}
~~~

## 2. 延时函数

~~~c++
void delayms(int msec)
{
    QEventLoop loop;
    QTimer::singleShot(msec,&loop,&QEventLoop::quit);
    loop.exec();
}
~~~

>>>>>>> 90ec3a4511a0cdf137e7775c31d0a4e371431fa6
