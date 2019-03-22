## 什么是DockerFile 

DockerFile 是用来构建docker镜像的构建文件，是由一系列命令和参数构成的脚本。



## 构建步骤：

1、编写DockerFile 文件

2、docker build

3、docker run



## DockerFile 文件的样子：

参考：<https://hub.docker.com/_/centos>

![img](file:///C:/Users/SI-GZ-0952/Documents/My Knowledge/temp/c6cd6ca0-4beb-11e9-9db9-0da96a56c8d2/128/index_files/1553181572633-q50.png)

![img](file:///C:/Users/SI-GZ-0952/Documents/My Knowledge/temp/c6cd6ca0-4beb-11e9-9db9-0da96a56c8d2/128/index_files/1553181645332-lp2.png)



## DockerFile说明：

1、每条保留字指令，都必须为大写字母，并且至少带一个参数

2、指令从上到下，顺序实行

3、# 表示注释

4、每一条执行都会创建一个新的镜像层，并对镜像层进行提交



## DockerFile  执行的大致流程

1、docker 从基础镜像运行一个容器

2、执行一条指令并对容器做出修改

3、执行类似docker commit的操作，提交一个新的镜像层

4、docker 基于上一个指令的镜像运行一个容器

5 、直到所有指令都运行执行完成



\## Docker 系统结构（保留字指令） 

FROM :  基础镜像，当前新镜像是基于哪个镜像

MAINTAINER：镜像维护着的姓名和邮箱地址

RUN ： 容器构建时需要运行的命令

EXPOSE ： 当前容器对外暴露出的端口

WORKDIR：执行在创建容器后，终端默认登录景来容器的工作目录

ENV：用来构建镜像过程中设置的环境变量

ADD：将宿主目录下的文件拷贝进镜像，并且ADD命令会自动处理URL和解压tar压缩包

COPY：类似ADD，拷贝文件和目录到镜像中。将从构建上下文目录中 < 源路径 > 的文件或者目录复制到新的一层的镜像内的<目标路径>位置

VOLUME：容器数据卷，用于数据保存和持久化

CMD：指定一个容器启动时要运行的命令 （DockerFile中可能存在多个CMD，单只有最后一个CMD生效。最后一个CMD也会被docker run 的参数替换）

ENTRYPOINT：执行一个容器需要运行的命令（和CMD一样，都是指定容器启动程序及参数）

ONBUILD：当构建一个被继承的DockerFile时运行命令，父镜像在被子镜像继承后，父镜像的onbuild会被触发



案例：自定义镜像 tomcat

1 mkdir -p /zzyyuse/mydockerfile/tomcat

2 在目录下  touch a.txt

3 将jdk和tomcat安装的压缩包拷贝到创建的目录中

4 在/zzyyuse/mydockerfile/tomcat 目录下创建DockerFile文件

5 构建  docker build -t zzyytomcat8 .

6 run  

docker run -it -d -p 9080:8080 --name mytomcat8 -v /zzyyuse/mydockerfile/tomcat8/webapps/:/usr/local/apache-tomcat-8.5.37/webapps/ -v /zzyyuse/mydockerfile/tomcat8/tomcat8logs/:/usr/local/apache-tomcat-8.5.37/logs/ --privileged=true zzyytomcat8

7 验证  

http://192.168.227.128:9080/test/a.html