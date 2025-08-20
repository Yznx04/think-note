---
date: 
  created: 2025-8-20 20:57:13

tags:
  - Linux
  - Docker
  - Deepin23
---

# deepin23社区版安装与配置docker

最近将老笔记本安装deepin23社区版使得它焕发第二春。对于后端程序员来说，docker是不可缺少的技术，同时，为了方便后续的学习和实践，进行了docker
的安装，记录一下，避免后续忘记了。

## 安装

deepin23中已经内置来`docker.io`，关于docker.io和docker.ce区别就在于一个是Debian团队维护的，一个是docker官方维护的。
同时，docker.io的命令缺乏部分参数，但是不影响正常使用。

安装命令：

```
sudo apt install docker.io -y
```

deepin的常用用户一般不是root, 所以需要使用sudo执行。等待命令执行完成，docker也就安装好了。如果需要使docker开机自启动，执行命令

```
sudo systemctl enable docker
```

## 配置

### 配合用户有权限使用docker

由于使用的是sudo命令进行安装，安装完成后普通用户是无法直接使用的，使用`docker info`都会报权限不足的错误。解决方案是将当前用户加入到docker的
用户组当中：

```
usrmod -aG docker $USER
```

然后，重启你的电脑。等待电脑重启完后，就可以用普通用户执行docker的命令来。

### 配置docker镜像源

在国内，不配置docker镜像源基本没法用，同时，不知为何，大部分docker镜像源都不太好用了。目前仅有一个镜像源不错：[轩辕镜像](https://docker.xuanyuan.me/#mirror-tutorial)

配置方式：

```
sudo vim /etc/docker/daemon.json
```

写入内容：

```json
{
    "registry-mirrors": [
        "https://docker.xuanyuan.me"
    ]
}
```

然后执行：

```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

大功告成！