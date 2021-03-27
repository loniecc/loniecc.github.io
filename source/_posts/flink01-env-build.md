---
title: Flink 环境搭建
date: 2021-03-04 12:11:25
tags:
---

## 前言
运行Flink需要环境，为了快速开始编码学习，我们直接使用Flink本地部署+IDE搭建开发环境
1. 搭建Flink环境
2. 开发&运行Flink程序

## Flink 本地环境搭建
### Idea 直接运行式
1. [下载Flink](https://ci.apache.org/projects/flink/flink-docs-release-1.12/zh/try-flink/local_installation.html)
2. 创建项目
```
mvn archetype:generate \
-DarchetypeGroupId=org.apache.flink \
-DarchetypeArtifactId=flink-walkthrough-datastream-java \
-DarchetypeVersion=1.12.0 \
-DgroupId=frauddetection \
-DartifactId=frauddetection \
-Dversion=0.1 \
-Dpackage=spendreport \
-DinteractiveMode=false
```
3. 用Idea 打开创建好的项目
4. 在Idea 打开配置`File-Project Structure-Libraries-±–java`,添加第一步解压出来的Flink包里的lib 和 opt 包
5. 随便写点啥，运行吧，然后就能在控制台打印出来了
6. 特别注意
		1. 不要引入Spring Boot，不要仗着Idea是高级版就无脑创建Spring Boot项目
		2. 没有主包的，create 一个，然后mark一下

### 提交jar式

#### 搭建运行环境
[搭建本地Flink 集群](https://ci.apache.org/projects/flink/flink-docs-release-1.12/zh/try-flink/local_installation.html)
#### IDE 开发Flink
1. 创建项目
```
mvn archetype:generate \
-DarchetypeGroupId=org.apache.flink \
-DarchetypeArtifactId=flink-walkthrough-datastream-java \
-DarchetypeVersion=1.12.0 \
-DgroupId=frauddetection \
-DartifactId=frauddetection \
-Dversion=0.1 \
-Dpackage=spendreport \
-DinteractiveMode=false
```


2. 使用Idea 打开
3. 配置模块下的pom 打包插件如下
```
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <!--设置程序的入口类-->
                            <mainClass>aaa.bbb.ccc</mainClass>
                            <addClasspath>true</addClasspath>
                            <classpathPrefix>lib/</classpathPrefix>
                        </manifest>
                    </archive>
                    <classesDirectory>
                    </classesDirectory>
                </configuration>
            </plugin>
        </plugins>
</build>		 
```
4. 提交到Flink
``` 
/Users/lonie/open_source/flink-1.12.1/bin/flink run  target/demo-0.0.1-SNAPSHOT.jar
```
5. 查看TaskManager 的日志即可  
