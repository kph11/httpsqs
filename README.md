# httpsqs
fork of zhangyan's httpsqs

# 编译安装
```
ulimit -SHn 65535

wget http://httpsqs.googlecode.com/files/libevent-2.0.12-stable.tar.gz
tar zxvf libevent-2.0.12-stable.tar.gz
cd libevent-2.0.12-stable/
./configure --prefix=/usr/local/libevent-2.0.12-stable/
make
make install
cd ../

wget http://httpsqs.googlecode.com/files/tokyocabinet-1.4.47.tar.gz
tar zxvf tokyocabinet-1.4.47.tar.gz
cd tokyocabinet-1.4.47/
./configure --prefix=/usr/local/tokyocabinet-1.4.47/
#注：在32位Linux操作系统上编译Tokyo cabinet，请使用./configure --enable-off64代替./configure，可以使数据库文件突破2GB的限制。
#./configure --enable-off64 --prefix=/usr/local/tokyocabinet-1.4.47/
make
make install
cd ../

wget http://httpsqs.googlecode.com/files/httpsqs-1.7.tar.gz
tar zxvf httpsqs-1.7.tar.gz
cd httpsqs-1.7/
make
make install
cd ../
```
# 使用方法
```
[root@xoyo ~]# httpsqs -h
-l <ip_addr> 监听的IP地址，默认值为 0.0.0.0
-p <num> 监听的TCP端口（默认值：1218）
-x <path> 数据库目录，目录不存在会自动创建（例如：/opt/httpsqs/data）
-t <second> HTTP请求的超时时间（默认值：3）
-s <second> 同步内存缓冲区内容到磁盘的间隔秒数（默认值：5）
-c <num> 内存中缓存的最大非叶子节点数（默认值：1024）
-m <size> 数据库内存缓存大小，单位：MB（默认值：100）
-i <file> 保存进程PID到文件中（默认值：/tmp/httpsqs.pid）
-a <auth> 访问HTTPSQS的验证密码（例如：mypass123）
-d 以守护进程运行
-h 显示这个帮助

eg:
ulimit -SHn 65535
httpsqs -d -p 1218 -x /data0/queue
```

# 使用注意
请使用命令“killall httpsqs”、“pkill httpsqs”和“kill `cat /tmp/httpsqs.pid`”来停止httpsqs。
请不要使用命令“pkill -9 httpsqs”和“kill -9  httpsqs的进程ID”来结束httpsqs，否则，内存中尚未保存到磁盘的数据将会丢失。

# HTTP使用参数
name: 队列的名称
opt: 要执行的操作
* put
* get
* view
* maxqueue: 表示设置最大队列长多
* status
pos: 查看的时候的位置
num: 用来指定最大的队列长度

# 预定义的返回值
```
HTTPSQS_AUTH_FAILED
HTTPSQS_PUT_END
HTTPSQS_PUT_ERROR
HTTPSQS_GET_END
HTTPSQS_EMPTY
HTTPSQS_RESET_ERROR
HTTPSQS_MAXQUEUE_CANCEL
HTTPSQS_SYNCTIME_CANCEL
HTTPSQS_ERROR

HTTPSQS_PUT_OK
HTTPSQS_RESET_OK
HTTPSQS_MAXQUEUE_OK
HTTPSQS_SYNCTIME_OK
```

# ubuntu环境安装
apt install libbz2-dev
apt install libevent-dev
apt install libtokyocabinet-dev

