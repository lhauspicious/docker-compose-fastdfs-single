#  Fastdfs-single
使用docker compose 创建fastdfs单机版服务(tarcker,storage,nginx)
## 使用
1. 在Linux中[安装docker](https://blog.csdn.net/meiko_zhang/article/details/81320721).  
2. 安装git    
```  
sudo apt-get install git
```
3. clone项目    
 ```
 git clone  https://github.com/meiko-zhang/fastdfs-single.git 
 ```
	    
4. 进入fastdfs-single 目录  
```
 cd fastdfs-single
```
      
5. 修改docker-compose.yml
```
version: '3.0'

services:
    fastdfs:
        build: .
        # 创建的镜像名称.可以自行修改
        image: meiko/fastdfs-single:5.11
        # 该容器是否需要开机启动+自动重启。若需要，则取消注释。
        restart: always
        # 启动容器名称,可修改
        container_name: fastdfs-single
        environment:
            # nginx服务端口,可修改
            - WEB_PORT=8888
            # docker所在主机的IP地址,修改为自己主机IP
            - IP=192.168.73.141
        volumes:
            # 将本地目录映射到docker容器内的fastdfs数据存储目录，将fastdfs文件存储到主机上，以免每次重建docker容器，之前存储的文件就丢失了。可修改
            - ${HOME}/docker-data/fdfs:/var/local/fdfs
        # 使docker具有root权限以读写主机上的目录
        privileged: true
        # 网络模式为host，即直接使用主机的网络接口
        network_mode: "host"

```  
 docker所在主机IP必须修改.
 
6. 执行docker-compose 命令  
```
 docker-compose up -d
```
       
    
测试及其他配置请[参考文档](https://www.centos.bz/2017/12/%E4%BD%BF%E7%94%A8docker-compose%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2%E5%88%86%E5%B8%83%E5%BC%8F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9Ffastdfs/).
    
项目文件[百度云地址](https://pan.baidu.com/s/1Mu0GRhoFkrgFkB68P2Et-Q).
