# pinpoint 构建目录

## 使用方法
通过maven镜像挂载pinpoint(src目录)源码，和maven的cache目录(root目录)来构建pinpoint

构建命令
```bash
# 通过进入容器内部手动构建
docker run -it -w /mnt \
               -v $PWD/src:/mnt \
               -v $PWD/root:/root \
               -v $PWD/jdk:/usr/local/jdk \
               -e JAVA_6_HOME=/usr/local/jdk/jdk1.6.0_45 \
               -e JAVA_7_HOME=/docker-java-home \
               -e JAVA_8_HOME=/usr/local/jdk/jdk1.8.0_151 \
               maven:3.5.2-jdk-7 bash

# 直接构建并退出maven容器
docker run --rm -it -w /mnt \
               -v $PWD/src:/mnt \
               -v $PWD/root:/root \
               -v $PWD/jdk:/usr/local/jdk \
               -e JAVA_6_HOME=/usr/local/jdk/jdk1.6.0_45 \
               -e JAVA_7_HOME=/docker-java-home \
               -e JAVA_8_HOME=/usr/local/jdk/jdk1.8.0_151 \
               maven:3.5.2-jdk-7 mvnw clean install -Dmaven.test.skip=true
```

构建完成后，可以在src目录的各个组件target目录中找到构建完成的jar或war文件。
