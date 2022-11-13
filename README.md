# sp_nas_server
自用NAS服务器配置文件

## 1. 操作系统ubuntu

```bash
sudo apt update
sudo apt upgrade -y

// 开启远程ssh连接
sudo apt install openssh-server -y

```


## 2. 系统软件

### 1) 文件管理

#### 硬盘合并 mergerfs

选择mergerfs的原因主要如下：
第一、可以很方便的将多块硬盘合并挂在一个目录使用，不用考虑硬盘文件格式，比如我用的就是NTFS格式。
第二、方便后续文件备份。由于mergerfs的特殊硬盘以及文件管理模式，在用ntfs格式的前提下，我们可以很方便的将单个硬盘取出挂在windows下进行读取备份。




#### samba服务

```bash
# install
sudo apt-get install samba
sudo apt-get install samba-client

# 这里的用户得是linux里面有的用户 
smbpasswd -a jiayao 
New SMB password:  
Retype new SMB password:

# 重启smbd服务
sudo service smbd restart 

# 修改设置
sudo vi /etc/samba/smb.conf
```


### 2）Docker

```

// 安装docker
sudo apt install curl

// install docker
// 1.
Sudo apt-get remove docker docker-engine docker.io

// 2.
Sudo apt-get update

// 3.
Sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

// 4.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | Sudo apt-key add -

// 5.
Sudo apt-key fingerprint 0EBFCD88

// 6. ubuntu
Sudo add-apt-repository "deb [Arch=AMD64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"
// 6. ubuntu衍生版本
add-apt-repository "deb [Arch=AMD64] https://download.docker.com/linux/ubuntu $(. /etc/os-release; echo "$UBUNTU_CODENAME") stable"
// 7.
Sudo apt-get update

// 8.
Sudo apt-get install docker-ce
```

#### docker-compose

```brash
//1. Run this command to download the current stable release of Docker Compose:
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

// 2. Apply executable permissions to the binary:
sudo chmod +x /usr/local/bin/docker-compose

// 3. Test the installation.
docker-compose --version
## Nas服务

### nginx + nas主页

docker 配置文件见 docker-compose.yam

```

#### docker 常用操作命令

```brash
    # 查看当前启动的容器
    sudo docker-compose ps
    
    # 启动部分服务在后边加服务名，不加表示启动所有，-d 表示在后台运行
    sudo docker-compose up [nginx|php| ...] -d
    
    # 停止和启动类似
    sudo docker-compose stop [nginx|php| ...]

    # 停止并删除相关的容器
    sudo docker-compose down [nginx|php| ...]

    # 删除所有未运行的容器
    sudo docker rm $(sudo docker ps -a -q)

    # 删除所有未运行的镜像，-f 可以强制删除
    sudo docker rmi $(sudu docker images -q)

    # 重新构建过清理无效数据（注意如果执行 docker images -a 会出现一些 none 的镜像，这些是构建镜像的中间层不占用空间也不是垃圾数据，不用管，使用下面的命令就是清理无效数据）
    sudo docker system prune
```

更多可通过 `sudo docker -h` 或者 `sudo docker-compose -h` 查看