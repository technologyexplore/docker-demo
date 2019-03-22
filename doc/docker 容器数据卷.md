
## 容器数据卷所解决的问题：

\* 持久化

\* 容器之间希望有可能共享数据



Docker容器产生的数据，如果不通过docker commit生成新的镜像，使得数据做为镜像的一部分保存下来，

那么当容器删除后，数据自然也就没有了。



## 如何使用：

两种方式：

### 1、直接通过命令添加

命令：docker run -it -v /宿主机绝对路径目录：/容器内目录 容器ID

查看数据卷是否挂在成功：docker inspect 容器ID

![img](file:///C:/Users/SI-GZ-0952/Documents/My Knowledge/temp/c4338f40-4be8-11e9-bd18-191520df3f5d/128/index_files/1553181023713-0zc.png)

命令（带权限）：docker run -it -v /宿主机绝对路径目录：/容器内目录:ro 容器ID

![img](file:///C:/Users/SI-GZ-0952/Documents/My Knowledge/temp/c4338f40-4be8-11e9-bd18-191520df3f5d/128/index_files/1553181044848-vtr.png)



多个容器，共享容一个目录，容器之间，数据会同步。



Docker挂载主机目录Docker访问出现cannot open directory .: Permission denied

解决办法：在挂载目录后多加一个--privileged=true参数即可



### 2、DockerFile 添加 （DockerFile中说明）