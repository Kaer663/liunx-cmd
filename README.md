# 一、Linux 常用命令

1. `init 0` - 关机
2. `init 6` - 重启
3. `ls`、`ls -l`、`ll` - 列出当前目录下的文件
4. `cd` - 切换目录
5. `pwd` - 查看当前路径
6. `cd -` - 切换最近使用过的两个目录
7. `ctrl+c` - 中断当前程序
8. `ctrl+l` / `clear` - 清屏
9. `ip addr` / `ifconfig` - 查看网卡信息
10. `ping 127.0.0.1` - 看网络是否通畅

# 二、Linux shell 命令技巧

1. **tab 补全**

   - 命令 + (1 次) tab
   - 命令 + (2 次) tab

2. **上下键盘** - 查看最近的历史命令

3. **history**

   - 查看命令历史
   - `!22` - 调用历史中编号为 22 的命令
   - `!h` - 调用历史中最后一次以 h 开头的命令

4. **获取帮助**

```bash
ls --help
man ls
```

# 三、Linux 创建用户修改密码

1. **添加用户**

```bash
useradd zhangsan
```

2. **设置密码**

```bash
passwd zhangsan
```

3. **删除用户**

```bash
userdel -rf zhangsan
#-r：递归的删除目录下面文件以及子目录下文件。
```

# 四、文件管理

1. **创建文件**

```bash
touch file1
```

2. **删除文件**

```bash
rm -rf file11

# -r：递归的删除目录下面文件以及子目录下文件。
# -f：强制删除，忽略不存在的文件，从不给出提示
```

3. **修改文件名**

```bash
mv  file1 file11
```

4. **查看文件内容**

```bash
cat file1
```

5. **复制文件**

```bash
cp file2 file22
```

6. **移动文件**

```bash
mv file1 file11
```

7. **编辑文件**

```bash
vi file1
```

8. **批量创建文件**

```bash
touch file{1..10}

rm -rf file{1..10}
```

9. **查看文件前 3 行**

| 把前面的执行结构给后端

```bash
cat file1 | head -3
```

10. **查看文件后 3 行**

```bash
cat file1 | tail -3
```

11. **liunx 服务器上面查找文件**

- find

```bash
find / -name httpd.conf
# find 目录 -name 文件名
```

2.updatedb 查找速度快

- 1、建立一个小型数据库 updatedb
- 2、再数据库里面搜索 locate httpd.conf
  mlocate 是新型的 locate 比 updatedb 速度更快。

```bash
yum install mlocate -y
```

12. **查找文件里面内容 找到 httpd.conf 里面有 listen**

```bash
cat httpd.conf | grep listen
cat httpd.conf | grep -ignore listen / cat httpd.conf | grep -i listen #忽略大小写

```

13、**查找文件里面内容 vi 搜索**
输入 /Listen 搜索 Listen N 下一个

```bash
vi httpd.conf

```

# 五、Linux 目录管理

1. **创建目录**

```bash
mkdir dir1 dir2 dir3
```

2. **删除目录**

```bash
rm -rf dir1 dir2
```

- `-r`：递归的删除目录下面文件以及子目录下文件。
- `-f`：强制删除，忽略不存在的文件，从不给出提示。
- `rm -rf dir*`：以 `dir` 开头的所有文件删除。

3. **重命名目录或移动目录**

```bash
mv dir1 dir11
```

4. **查看目录**

- `ls/ll`

5. **递归创建目录**

- `mkdir -p a/b/c/d/e/f/g`

6. **递归查看目录**

```bash
tree a
```

7. **复制目录**

- `cp -rf wwwroot/ mywwwroot/`

8. **tree 命令不存在的话需要安装**

```bash
yum install tree -y
```

# docker

1. 安装 centos

安装需要的软件包：

```bash
yum install -y yum-util
```

配置 docker 源

```bash
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

```

配置阿里源

```bash

yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

搜索 docker 验证

```bash
yum search docker
```

安装 docker

```bash
yum install docker-ce docker-ce-cli containerd.io -y
```

- containerd.io - daemon to interface with the OS API (in this case, LXC - Linux Containers), essentially decouples Docker from the OS, also provides container services for non-Docker
  container managers
- docker-ce - Docker daemon, this is the part that does all the management work, requires the
  other two on Linux
- docker-ce-cli - CLI tools to control the daemon, you can install them on their own if you want
  to control a remote Docker

2. -v 指定路径挂载数据卷

```bash
 docker run -tid --name nginx-82 -p 82:80 -v /mnt/web/:/usr/share/nginx/html nginx
```

3. mongodb 指定密码

```bash
docker run -d --name auth_mongo \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=123456 \
-p 27017:27017 \
-v /mnt/persistence/mongo/data:/data/db \
mongo --auth
```
