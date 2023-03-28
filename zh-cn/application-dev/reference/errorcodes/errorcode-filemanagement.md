# 文件管理错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

文件管理子系统错误码由四部分组成，分别是基础文件IO错误码、用户数据管理错误码、公共文件访问错误码和空间统计错误码组成。

## 基础文件IO错误码

### 13900001 操作不允许

**错误信息**
Operation not permitted

**可能原因**
当前用户文件操作不被允许

**处理步骤**
确认文件权限

### 13900002 没有这个文件或目录

**错误信息**
No such file or directory

**可能原因**
文件或目录不存在

**处理步骤**
确认文件路径是否存在

### 13900003 没有这样的进程

**错误信息**
No such process

**可能原因**
进程不存在

**处理步骤**
1.确认进程是否被意外杀死
2.确认相关服务是否已启动

### 13900004 系统调用被中断

**错误信息**
Interrupted system call

**可能原因**
系统调用被其他线程中断

**处理步骤**
1.检查多线程代码逻辑
2.重新进行系统调用

### 13900005 I/0错误

**错误信息**
I/O error

**可能原因**
I0请求非法

**处理步骤**
重新进行I0请求

### 13900006 没有这个设备或地址

**错误信息**
No such device or address

**可能原因**
设备或地址信息错误

**处理步骤**
确认设备或地址信息

### 13900007 参数列表太长

**错误信息**
Arg list too long

**可能原因**
参数列表过长

**处理步骤**
减少参数个数

### 13900008 坏的文件描述符

**错误信息**
Bad file descriptor

**可能原因**
此文件描述符已关闭

**处理步骤**
确认此文件描述符是否已关闭

### 13900009 没有子进程

**错误信息**
No child processes

**可能原因**
无法创建子进程

**处理步骤**
确认系统中最大进程数

### 13900010 资源暂时不可用

**错误信息**
Try again

**可能原因**
资源被阻塞

**处理步骤**
重新请求资源

### 13900011 内存溢出

**错误信息**
Out of memory

**可能原因**
内存溢出

**处理步骤**
1.确认内存开销
2.管理系统内存开销

### 13900012 拒绝许可

**错误信息**
Permission denied

**可能原因**
1.文件操作无权限
2.文件沙箱路径地址错误

**处理步骤**
1.确认权限
2.确认文件沙箱路径地址

### 13900013 错误的地址

**错误信息**
Bad address

**可能原因**
地址错误

**处理步骤**
确认地址是否正确

### 13900014 设备或资源忙

**错误信息**
Device or resource busy

**可能原因**
请求的资源不可用

**处理步骤**
重新请求资源

### 13900015 文件存在

**错误信息**
File exists

**可能原因**
需创建的文件已存在

**处理步骤**
确认文件路径是否正确

### 13900016 无效的交叉链接

**错误信息**
Cross-device link

**可能原因**
跨设备链接失败

**处理步骤**
确认跨设备是否正常

### 13900017 设备不存在

**错误信息**
No such device

**可能原因**
设备未被识别

**处理步骤**
确认设备间连接是否正常

### 13900018 不是一个目录

**错误信息**
Not a directory

**可能原因**
此路径不是文件夹目录

**处理步骤**
确认路径是否正确

### 13900019 是一个目录

**错误信息**
Is a directory

**可能原因**
此路径是文件夹目录

**处理步骤**
确认路径是否正确

### 13900020 无效的参数

**错误信息**
Invalid argument

**可能原因**
输入参数非法

**处理步骤**
确认参数合法性

### 13900021 打开太多的文件系统

**错误信息**
File table overflow

**可能原因**
进程打开过多的文件描述符

**处理步骤**
关闭不相关的文件描述符

### 13900022 打开的文件过多

**错误信息**
Too many open files

**可能原因**
系统打开过多的文件

**处理步骤**
关闭不需要的文件

### 13900023 文本文件忙

**错误信息**
Text file busy

**可能原因**
程序的可执行文件正在被使用

**处理步骤**
关闭正在调试的程序

### 13900024 文件太大

**错误信息**
File too large

**可能原因**
文件大小超出最大文件大小

**处理步骤**
确认文件大小是否满足最大文件大小

### 13900025 设备上没有空间

**错误信息**
No space left on device

**可能原因**
设备存储空间不足

**处理步骤**
清理设备存储空间

### 13900026 非法移位

**错误信息**
Illegal seek

**可能原因**
在管道或FIFO中使用seek

**处理步骤**
确认seek使用

### 13900027 只读文件系统

**错误信息**
Read-only file system

**可能原因**
文件系统只支持读

**处理步骤**
确认文件是否只读

### 13900028 太多的链接

**错误信息**
Too many links

**可能原因**
文件已达最大链接数

**处理步骤**
清理无用链接

### 13900029 资源死锁错误

**错误信息**
Resource deadlock would occur

**可能原因**
资源死锁

**处理步骤**
终止死锁进程

### 13900030 文件名太长

**错误信息**
Filename too Long

**可能原因**
路径或文件名超过最大长度

**处理步骤**
确认路径或文件名长度

### 13900031 功能没有实现

**错误信息**
Function not implemented

**可能原因**
系统不支持此功能

**处理步骤**
确认系统版本

### 13900032 目录非空

**错误信息**
Directory not empty

**可能原因**
指定目录不为空

**处理步骤**
1.确认目录路径
2.确认路径为空

### 13900033 符号链接层次太多

**错误信息**
Too many symbolic liks encountered

**可能原因**
符号链接层次过多

**处理步骤**
清理无关符号链接

### 13900034 操作被阻塞

**错误信息**
Operation would block

**可能原因**
操作被阻塞

**处理步骤**
重新进行操作

### 13900035 请求描述符无效

**错误信息**
Invalid request desecriptor

**可能原因**
文件描述符非法

**处理步骤**
确认文件描述符是否合法

### 13900036 设备不是字符流

**错误信息**
Device not a stream

**可能原因**
文件描述符指向非流设备

**处理步骤**
确认文件描述符是否指向流设备

### 13900037 无可用数据

**错误信息**
No data available

**可能原因**
数据不可用

**处理步骤**
重新请求数据

### 13900038 对于定义的数据类型,值太大

**错误信息**
Value too large for defined data type

**可能原因**
值超出所定义的数据类型范围

**处理步骤**
修改数据类型

### 13900039 文件描述符在坏状态

**错误信息**
File descriptor in bad state

**可能原因**
文件描述符损坏

**处理步骤**
确认文件描述符合法性

### 13900040 应该重新启动被中断的系统调用

**错误信息**
Interrupted systen call should be restarted

**可能原因**
系统调用被中断

**处理步骤**
重新进行系统调用

### 13900041 超出磁盘配额

**错误信息**
Quota exceeded

**可能原因**
磁盘空间不足

**处理步骤**
清理磁盘存储空间

### 13900042 未知错误

**错误信息**
Unknown error

**可能原因**
内部错误

**处理步骤**
1.重试接口
2.重启服务

## 用户数据管理错误码

### 14000001 文件名非法

**错误信息**
Invalid display name

**可能原因**
文件名存在非法字符

**处理步骤**
删除非法字符

### 14000002 非法URI

**错误信息**
Invalid uri

**可能原因**
URI不合法

**处理步骤**
直接使用查询获取的uri

### 14000003 文件后缀非法

**错误信息**
Invalid file extension

**可能原因**
按照文件类型命名

**处理步骤**
检查文件名后缀

### 14000004 文件已进入回收站

**错误信息**
File has been put into trash bin

**可能原因**
文件已经被删除进入回收站

**处理步骤**
检查文件是否已经进入回收站

## 空间统计错误码

### 13600001 IPC通信失败

**错误信息**
IPC error

**可能原因**
调用服务不存在

**处理步骤**
检查服务是否启动

### 13600002 文件系统类型不支持

**错误信息**
Not supported filesystem

**可能原因**
操作的文件系统类型不支持

**处理步骤**
修改为正确的文件系统类型

### 13600003 挂载失败

**错误信息**
Failed to mount

**可能原因**
调用挂载命令失败

**处理步骤**
拔卡尝试重新挂载

### 13600004 卸载失败

**错误信息**
Failed to unmount

**可能原因**
设备繁忙

**处理步骤**
检查外卡文件是否被线程占用, 杀掉占用线程

### 13600005 卷状态错误

**错误信息**
Incorrect volume state

**可能原因**
操作的卷状态错误

**处理步骤**
检查当前卷状态是否正确

### 13600006 创建目录或者节点失败

**错误信息**
Prepare directory or node error

**可能原因**
目录或节点已存在

**处理步骤**
检查待创建目录或节点是否存在

### 13600007 删除目录或者节点失败

**错误信息**
Delete directory or node error

**可能原因**
目录或节点已删除

**处理步骤**
检查待删除目录或节点是否存在

### 13600008 操作对象不存在

**错误信息**
No such object

**可能原因**
1.输入错误的卷id
2.输入错误的包名

**处理步骤**
1.检查输入的卷是否存在
2.检查输入的应用包名是否存在

### 13600009 用户id超出范围

**错误信息**
User id out of range

**可能原因**
输入错误的用户id

**处理步骤**
检查输入的用户id是否处于正常范围

## 公共文件访问错误码

### 14300001 IPC通信失败

**错误信息**
IPC error

**可能原因**
1.server端服务不在
2.extension机制异常

**处理步骤**
检查server端服务是否存在

### 14300002 URI格式错误

**错误信息**
Invalid uri

**可能原因**
使用非法uri

**处理步骤**
检查URI格式

### 14300003 查询server端ability信息失败

**错误信息**
Fail to get fileextension info

**可能原因**
BMS接口异常

**处理步骤**
系统基础能力问题

### 14300004 js-server实际返回的结果异常

**错误信息**
Get wrong result

**可能原因**
server端返回实际数据不当

**处理步骤**
server端返回值检查

### 14300005 notify注册失败

**错误信息**
Fail to register notification

**可能原因**
1.server端服务不在
2.extension机制异常

**处理步骤**
检查server端服务是否存在

### 14300006 notify移除失败

**错误信息**
Fail to remove notification

**可能原因**
1.server端服务不在
2.extension机制异常

**处理步骤**
检查server端服务是否存在

### 14300007 notify代理初始化失败

**错误信息**
Fail to init notification agent

**可能原因**
未注册就去取消notify

**处理步骤**
是否注册过

### 14300008 js-server端通知代理失败

**错误信息**
Fail to notify agent

**可能原因**
1.服务不在
2.extension机制异常

**处理步骤**
检查client是否异常

## 错误码适配指导
文件管理子系统API支持异常处理。
同步接口异常处理示例代码:
```js
import fs from '@ohos.file.fs'

try {
    let file = fs.openSync(path, fs.OpenMode.READ_ONLY);
} catch (err) {
    console.error("openSync errCode:" + err.code + ", errMessage:" + err.message);
}
```
异步接口promise方法异常处理示例代码:
```js
import fs from '@ohos.file.fs'

try {
    let file = await fs.open(path, fs.OpenMode.READ_ONLY);
} catch (err) {
    console.error("open promise errCode:" + err.code + ", errMessage:" + err.message);
}
```

异步接口callback方法异常处理示例代码:
```js
import fs from '@ohos.file.fs'

try {
    fs.open(path, fs.OpenMode.READ_ONLY, function(e, file){ //异步线程的错误（如系统调用等）在回调中获取
        if (e) {
            console.error("open in async errCode:" + e.code + ", errMessage:" + e.message);
        }
    });
} catch (err) { //主线程的错误（如非法参数等）通过try catch获取
    console.error("open callback errCode:" + err.code + ", errMessage:" + err.message);
}
```