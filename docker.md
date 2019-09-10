~~~
docker pull registry:2.6.0-rc.1
~~~

~~~
mkdir -p /www/docker/registry
~~~

~~~
docker run --name registry --restart=always -p 5000:5000  -v /www/docker/registry:/var/lib/registry -d registry:2.6.0-rc.1
~~~



需要推送镜像的机器

~~~
vi /etc/docker/daemon.json
加上："insecure-registries":["192.168.144.128:5000"]  （地址为registry地址）
重启docker服务：
service docker restart
给需要push的镜像打上tag
 docker tag abrtech/alpine-oraclejdk8 192.168.144.128:5000/oraclejdk8（tag里的ip和端口，为registry地址）
 docker push 192.168.144.128:5000/oraclejdk8

~~~

其他服务器就可以pull了:docker pull 192.168.144.128:5000/oraclejdk8





Dockerfile（文件名称一定别写错了）

相关命令：

* FROM   来自哪个镜像
* ADD复制文件（从src到容器的dest）
* ARG  设置的是构建时的环境变量，在容器运行时不存在这些变量
* CMD容器启动命令，为执行容器提供默认值。
* * CMD ["executable","param1","param2"]
  * CMD ["param1","param2"] （为ENTRYPOINT制定提供预设参数）
  * CMD command param1 param2 在shell中执行
  * * 示例：CMD echo“thisis a test"  | wc -
* COPY复制文件，和ADD类似，COPY不支持URL和压缩包
* ENTRYPOINT入口点
* * ENTRYPOINT ["executable","param1","param2"]
  * ENTRYPOINT command param1 param2 
* ENV 设置环境变量
* EXPOSE声明暴露的端口
* LABEL为镜像添加元数据
* MAINTAINER制定维护者的信息
* RUN执行命令
* * RUN <command>
  * RUN ["executable","param1","param2"]
* USER设置用户，制定启动镜像时的用户或UID
* VOLUMN指定挂载点    `VOLUMN /data`
* WORKDIR指定工作目录





在Dockerfile所在目录 `docker build -t ...`



