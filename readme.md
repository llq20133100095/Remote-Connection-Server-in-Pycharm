# pycharm远程连接服务器（带有跳板机，且具有动态口令）
## 1.使用SecureCRT进行端口转发

要从pycharm连接带有跳板机的服务器，需要现在secrueCRT上进行端口转发，这样可以自定义ip地址直接连上服务器上。

例如：
- 跳板机地址为：A地址:32200
- 需要连接的服务器地址为：190.168.50.196:32200

### 1.1 端口转发
连接好跳板机后，选择端口转发：

![端口转发1](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%911.png)

![端口转发2](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%911.png)
- 其中“名称”自主命名
- 本地ip地址可以随便填写
- 本地端口最后填1024以上
- 远程ip填写要远程连接的服务器：如190.168.50.196
- 远程端口为32200

### 1.2 测试端口转发是否成功
为了验证配置的正确性，创建一条127.0.0.1:2222的连接（此时连接的username和passward为内网服务器的用户名和密码）：

![端口转发3](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%913.png)

## 2.使用pycharm进行远程连接

### 2.1 换pycharm编译器

- 打开pycharm，把当前pycharm编译器变为服务器上的编译器

![编译器1](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%BC%96%E8%AF%91%E5%99%A81.png)

![编译器2](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%BC%96%E8%AF%91%E5%99%A82.png)

- 输入ip地址，就是上面设置的127.0.0.1
- 输入用户名和端口

![编译器3](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%BC%96%E8%AF%91%E5%99%A83.png)

- 如果遇到需要秘钥的，则选择Key pair，导入秘钥文件Identity，再输入密码
- 最后拿到服务器上的python3地址，然后选择把文件上传的路径

## 3.遇到的问题

### 3.1 pycharm调用GPU

会出现ImportError:libcusolver.so.10.0: cannot open shared object file: No such file or directory。

原因是因为pycharm没有把环境变量装载进去。

- 设置cuda的环境变量，新增LD_LIBRARY_PATH=/usr/local/cuda/lib64

![环境变量1](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F1.png)


- 设置项目里的环境变量：run->edit configurations-> Templates -> python -> Environment variables

![环境变量2](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F2.png)

![环境变量3](https://github.com/llq20133100095/Remote-Connection-Server-in-Pycharm/blob/master/picture/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F3.png)
