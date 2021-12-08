---
title: docker-note
---

## 命令

1. `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

   OPTIONS：

   * ***-d*** : 后台运行

   * ***-p*** : 端口映射，`-p 8080:80` 主机:容器

   * ***-v*** : 绑定挂载卷，可挂载目录或文件，`-v /test:/data` 主机:容器 `-v /test:/data:ro` 只读

   * ***--name*** 名字: 设置容器名称

   * ***-n*** : 指定容器hostname `-n yyy`

   * **-i:** 以交互模式运行容器，通常与 -t 同时使用

   * **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用

   * ***-it*** : 容器与你的终端通信输入输出

   * ***-m*** : 设置容器使用内存最大值

   * ***-e*** : 设置环境变量 `-e username="ritchie"`

   * ***--rm*** : 容器退出时自动清理容器并删除文件系统，等价于`docker rm -v`

   * ***--link <name or id>:alias*** :  可以用来链接2个容器，并且可以获取容器的环境变量，可容器名链接

     `docker run --link A:a`

   * ***--network=host*** : 指定容器的网络连接类型，支持`bridge(默认)/host/none/container`四种类型

   * ***--restart=always*** : Docker重启时，容器自动启动；容器退出时总是重启容器

2. `docker build` 命令用于使用 Dockerfile 创建镜像。

   `docker build -t runoob/ubuntu:v1 . `

   `docker build -f /path/to/a/Dockerfile .`

   `docker build github.com/creack/docker-firefox`  使用URL创建镜像

   *  ***-t*** : 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
   * ***-f***  : 指定要使用的Dockerfile路径

3. `docker ps [OPTIONS] `

   OPTIONS:

   * ***-a*** : 查看所有容器，包括停用
   * ***-s*** : 显示总文件大小
   * ***-q*** : 只显示容器id

4. `docker rm [OPTIONS] CONTAINER [CONTAINER...]`

   `docker rm 容器id(前4位即可)`

   OPTIONS：

   * ***-f*** : 强制删除正在运行的容器
   * ***-l*** : 移除容器间的网络连接，而非容器本身
   * ***-v*** : 删除与容器关联的卷
   * ***docker rm $(docker ps -a -q)*** : 删除所有已经停止的容器

5. ` docker attach [OPTIONS] CONTAINER`

   `docker attach 容器` 相当于操作cmd命令

   `docker attach --sig-proxy=false 容器` --sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。

6. ` docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`

   `docker exec -it 容器 /bin/bash` 进入容器进行操作

7. `docker inspect`

8. `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]` 从容器创建一个新的镜像

   `docker commit 容器 镜像名称:版本`

   - ***-p*** : 在commit时，将容器暂停
   - ***-a*** : 提交的镜像作者
   - ***-c*** : 使用Dockerfile指令来创建镜像
   - ***-m*** : 提交时的说明文字

9. `docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
    docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH`  用于容器与主机之间的数据拷贝

   `docker cp /www/runoob 96f7f14e99ab:/www/`

   `docker cp  96f7f14e99ab:/www /tmp/`

10. `docker info : 显示 Docker 系统信息，包括镜像和容器数

11. `docker diff 容器` 查看容器文件结构

12. `docker logs -t -f 容器` 

13. `docker logs [OPTIONS] CONTAINER`

    `docker logs -f -t -n 10 容器`

    * ***-f*** : 跟踪日志输出
    * ***-t*** : 显示时间戳
    * ***-n或--tail*** : 列出最后N条容器日志

14. `docker rmi [OPTIONS] IMAGE [IMAGE...] ` 删除一个或多个镜像

    * ***-f*** : 强制删除

15. ` docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]` 标记本地镜像，将其归入某一仓库

    * `docker tag openjdk:8 yyy/openjdk:v1`

16. `docker save [OPTIONS] IMAGE [IMAGE...]`

    `docker save -o images.tar image1:8 openjdk:8` 把镜像`openjdk`和`image1`打包成`images.tar`

17. `docker load [OPTIONS]`

    `docker load -i images.tar`  `openjdk`和`image1`载入进来，如果本地镜像库已经存在这两个镜像，将会被覆盖

18. `docker export [OPTIONS] CONTAINER` 

    `docker export -o postgres-export.tar postgres` 把容器`postgres`打包成`postgres-export.tar`

19. ` docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]`

    `docker import postgres-export.tar postgres:latest` docker import将container导入后会成为一个image，而不是恢复为一个container

    ```
     总结一下docker save和docker export的区别：
    1. docker save保存的是镜像（image），docker export保存的是容器（container）；
    2. docker load用来载入镜像包，docker import用来载入容器包，但两者都会恢复为镜像；
    3. docker load不能对载入的镜像重命名，而docker import可以为镜像指定新名称。
    ```

20. `docker history IMAGE` 查看镜像的创建历史，如dockerfile

1. `docker start 容器..` 开启一个或多个暂停的容器
2. `docker stop 容器..` 停止一个或多个容器
3. `docker restart 容器..` 重启容器
4. `docker kill 容器` 杀掉一个运行的容器
5. `docker pause 容器` 暂停容器中所有的进程
6. `docker unpause 容器` 恢复容器中所有的进程



## Compose

