# Qt TCP/IP 网络通讯

| 服务器                                                       | 客户端                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 套接字服务器类 `QTcpServer` 对象用于监听是否有客户端连接此服务器；<br />一旦监听到有客户端连接，服务器对象触发 `newConnection` 信号。<br />使用服务器对象的`nextPendingConnection()` 方法返回用于通讯的套接字类对象。 <br />套接字类 `QTcpSocket` 用于与客户端进行通讯； | 客户端只有一个负责通讯的套接字类对象。客户端使用 `connectToHost()` 方法与服务器建立连接 |

## 一、主要 API 函数

### 1. QTcpServer

> 套接字服务器类

#### 构造函数

~~~c++
/// 参数为其父对象
QTcpServer::QTcpServer(QObject *parent = nullptr);
~~~

#### 监听

~~~c++
/// 监听是否有客户端连接到服务器
/// QHostAddress 是封装好的 IPv4、IPv6 格式的 IP 地址。
/// address 是服务器要监听的地址，QHostAddress::Any表示监听本机所有网口的IP地址
/// port 是监听的网络端口，0 表示随机绑定一个可用端口
/// 返回值：监听动作成功返回 true，否则返回 false
bool QTcpServer::listen(const QHostAddress &address = QHostAddress::Any, quint16 port = 0);

// 判断当前对象是否在监听, 是返回true，没有监听返回false
bool QTcpServer::isListening() const;
// 如果当前对象正在监听，返回监听的服务器地址信息, 否则返回 QHostAddress::Null
QHostAddress QTcpServer::serverAddress() const;
// 如果服务器正在侦听连接，则返回服务器的端口; 否则返回0
quint16 QTcpServer::serverPort() const;
~~~

#### 信号函数

~~~~c++
/// 当接收新连接导致错误时，发出如下信号。socketError 参数描述了错误的相关信息
signals: void QTcpServer::acceptError(QAbstractSocket::SocketError socketError);

/// 当监测到有新连接可用时，发出以下信号
signals: void QTcpServer::newConnection();
~~~~

#### 阻塞等待客户端发起连接请求

- 不推荐在单线程程序中使用，建议使用非阻塞方式处理新连接，即使用信号 `newConnection() `。

~~~c++
/// msec: 指定阻塞的最大时长，单位为毫秒（ms）
/// timeout: 传出参数，如果操作超时 *timeout 为true，没有超时 *timeout 为 false
bool QTcpServer::waitForNewConnection(int msec = 0, bool* timedOut = nullptr);
~~~

#### 获得通信套接字

~~~c++
/// 得到和客户端建立连接之后用于通信的 QTcpSocket 套接字对象。
QTcpSocket *QTcpServer::nextPendingConnection();
~~~

### 2. QTcpSocket

> 套接字通信类，不管是客户端还是服务器端都需要使用。

#### 构造函数

~~~c++
QTcpSocket::QTcpSocket(QObject *parent = nullptr);
~~~

#### 连接到服务器

- 需要指定服务器端绑定的IP和端口信息

~~~c++
[virtual] void connectToHost(const QHostAddress &address, quint16 port, QIODevice::OpenMode openMode = ReadWrite)

[virtual] void connectToHost(const QString &hostName, quint16 port, QIODevice::OpenMode openMode = ReadWrite, QAbstractSocket::NetworkLayerProtocol protocol = AnyIPProtocol)
/// 如
socket->connectToHost("192.168.1.1",3333);
~~~

#### 等待连接成功

~~~c++
waitForConnected();
~~~

#### 接收数据

~~~c++
// 指定可接收的最大字节数 maxSize 的数据到指针 data 指向的内存中
qint64 QIODevice::read(char *data, qint64 maxSize);
// 指定可接收的最大字节数 maxSize，返回接收的字符串
QByteArray QIODevice::read(qint64 maxSize);
/// 将当前可用操作数据全部读出，通过返回值返回读出的字符串
/// 该功能无法报错； 返回一个空的 QByteArray 可能意味着当前没有数据可供读取，或者发生了错误。
QByteArray QIODevice::readAll();
~~~

#### 发送数据

~~~c++
// 发送指针 data 指向的内存中的 maxSize 个字节的数据
qint64 QIODevice::write(const char *data, qint64 maxSize);
// 发送指针 data 指向的内存中的数据，字符串以 \0 作为结束标记
qint64 QIODevice::write(const char *data);
// 发送参数指定的字符串
qint64 QIODevice::write(const QByteArray &byteArray);
~~~

​		在 Qt 中不管调用读操作函数接收数据，还是调用写函数发送数据，操作的对象都是本地的由 Qt 框架维护的一块内存。因此，调用了发送函数数据不一定会马上被发送到网络中，调用了接收函数也不是直接从网络中接收数据，关于底层的相关操作是不需要使用者来维护的。

#### 信号函数

> 在使用 `QTcpSocket` 进行套接字通信的过程中，如果该类对象发出 `readyRead()` 信号，说明对端发送的数据达到了，之后可以调用 `read` 函数接收数据了

~~~c++
signals: void QIODevice::readyRead();
// 调用 connectToHost() 函数并成功建立连接之后发出 connected() 信号。
signals: void QAbstractSocket::connected();
// 在套接字断开连接时发出 disconnected() 信号。
signals: void QAbstractSocket::disconnected();
~~~

#### 断开连接

~~~c++
/// 中止当前连接并重置套接字。 
/// 与 disconnectFromHost() 不同，此函数立即关闭套接字，丢弃写入缓冲区中的任何未决（pending）数据。
void QAbstractSocket::abort();

/// 试图关闭套接字。如果有等待写入的数据，QAbstractSocket将进入ClosingState并等待所有数据被写入。
/// 最终，它将进入UnconnectedState并发出disconnected()信号。
[virtual] void QAbstractSocket::disconnectFromHost()
~~~

其他

~~~c++
bool QAbstractSocket::flush();
/* 这个函数尽可能多地从内部写缓冲区写到底层网络套接字，不阻塞。如果有数据被写入，该函数返回true；否则返回false。
如果你需要QAbstractSocket立即开始发送缓冲区的数据，请调用此函数。成功写入的字节数取决于操作系统。在大多数情况下，你不需要调用这个函数，因为一旦控制权返回到事件循环，QAbstractSocket将自动开始发送数据。在没有事件循环的情况下，请调用waitForBytesWritten()代替。 */
~~~

#### 3. QByteArray

> Qt 字节数组类
>
> 用于存储原始的字节数组，并能始终确保数据后跟一个 `'\0'` 终止符。与 `const char* ` 类似，但是使用比`const char* ` 好用。
>
> 适用场景：存储原始二进制数据时，以及当内存保护至关重要时。

#### 构造函数

1. 将 `const char*` 类型的值传递给它的构造函数。

~~~c++
/// 构造一个字节数组，它包含数组数据 data 前 size 个字节的数据
/// 如果 data 为 0，则构造一个空字节数组。
/// 如果 size 为负数，则认为 data 指向以 '\0' 结尾的字符串，
/// 长度动态确定。终止字符 '\0' 不被视为字节数组的一部分,QByteArray 对字符串数据进行「深拷贝」。
QByteArray::QByteArray(const char *data, int size = -1)
~~~

2. 使用 `resize()` 方法设置数组的大小，使用 `operator[]()` 来访问和修改对应索引(从 0 开始)位置的字节。

~~~c++
QByteArray ba;
ba.resize(5);
ba[0] = 0x3c;
ba[1] = 0xb8;
ba[2] = 0x64;
ba[3] = 0x18;
ba[4] = 0xca;
~~~

3. 指定字符填充的字节数组

~~~c++
/// 构造一个大小为 size 的字节数组，每个字节都设置为字符 ch。
QByteArray::QByteArray(int size, char ch)
~~~



