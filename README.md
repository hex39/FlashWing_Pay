# FlashWing_Pay
微服务架构的闪翼支付平台

嫌弃了git本地仓库直接建立在桌面，浪费了C盘的空间，我在D盘又新建了文件夹，将git仓库初始化。发现clone下载速度巨慢，通过设置代理socks：1080的方式，让下载速度变快：

```c
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

可是这个方法只能加速 https 的速度，我再想要push的时候，每次都需要输入密码。

把换成了SSH的方式：

```c
$ git remote -v                   //查看传输方式
```

```c
$ git remote rm origin            //移除当前方式
```

```c
$ git remote add origin SSH地址
//设置成SSH方式
```

使用git在本地新建一个分支后，需要做远程分支关联，如果没有关联，git会在下面的操作中提示你显示的添加关联。关联目的是在执行git pull, git push操作时就不需要指定对应的远程分支，你只要没有显示指定，git pull的时候，就会提示你。

```c
$ git branch --set-upstream
```

$ git push -u origin master 上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

```
$ git push -u origin master
```

接下来就能无脑 git push / pull  命令了！



因为昨日安装nacos失败，貌似是因为不支持MySQL5.5的原因，搞了一天半，终于安装上MySQL8，如下：

下载解压8的包，在bin的**同级**目录，创建my.ini文件：

```ini
[mysqld]
# These are commonly set, remove the # and set as required.
basedir=D:\MySQL\mysql-8.0.19-winx64
datadir=D:\MySQL\mysql-8.0.19-winx64\data
port=3307
server_id=2
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 
default-authentication-plugin=mysql_native_password
```

管理员打开cmd，cd到解压目录，输入： 进行初始化

```
mysqld --defaults-file=D:\MySQL\mysql-8.0.19-winx64\my.ini --initialize --console
```

留意root@localhost后的字符串，复制保存该默认密码

再执行以下命令，安装MySQL8：

```
mysqld install MySQL8 --defaults-file=D:\MySQL\mysql-8.0.19-winx64\my.ini
```

打开MySQL8注册表，修改imagePath值：

```
"D:\MySQL\mysql-8.0.19-winx64\bin\mysqld" --defaults-file=D:\MySQL\mysql-8.0.19-winx64\my.ini MySQL8
```

cmd中启动MySQL8服务：

```
net start MySQL8
```

然后输入刚才记下的随机密码登录：

```
mysql -uroot -p -P3307
```

登录后重新设置密码： 

```sql
ALTER USER 'root'@'localhost'IDENTIFIED BY '新的密码';
```

MySQL8至此安装完毕，测试连接通过。



