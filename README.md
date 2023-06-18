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

#### Alist

- [alist 安装指南](https://alist.nn.ci/zh/guide/install/docker.html#%E5%8F%91%E8%A1%8C%E7%89%88%E6%9C%AC)

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

- [how-to-install-and-use-docker-on-ubuntu-22-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)

#### docker-compose

- [how-to-install-and-use-docker-compose-on-ubuntu-22-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-22-04)

## 娱乐

### jellyfin

- [docker-jellyfin](https://hub.docker.com/r/linuxserver/jellyfin)

## Nas服务

### nginx + nas主页

docker 配置文件见 docker-compose.yam


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
