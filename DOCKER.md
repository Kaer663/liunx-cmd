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
