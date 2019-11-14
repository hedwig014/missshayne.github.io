---
title: mac tomcat安装与shell命令配置
date: 2019-11-12 20:55:33
tags: ['tomcat', '后端']
---
1. 记录安装tomcat碰到的问题
2. 自定义tomcat shell命令   

<!-- more -->
### 安装tomcat碰到的问题
1. 安装tomcat(tar.gz)   
下载链接：http://tomcat.apache.org   
2. 将tomcat移动到~/Development下并解压，重命名（也可放在其他文件夹下,建议/usr/local)   
移动: mv /Users/shayne/Downloads/apache-tomcat-8.5.47.tar.gz ~/Development   
解压: tar zxvf apache-tomcat-8.5.47.tar.gz   
重命名: mv apache-tomcat-8.5.47 Tomcat
3. 进入Tomcat的bin目录下给文件设置运行权限   
sudo chmod 755 *.sh   
4. 启动tomcat   
进入Tomcat/bin下，运行startup.sh,遇到两个问题
> logs文件夹不存在   
  手动创建了logs，终端提示tomcat started，但在浏览器输入localhost:8080,没有看到tomcat的默认页   
  解决： 下载包的问题，重新下载
5. 停止tomcat   
运行shutdown.sh

### 自定义tomcat shell命令
每次运行tomcat，都要进入到相关目录，很繁琐，就想到了自定义命令，虽然网上已有一大堆，但还是记录下，增强记忆   
1. 进入usr/local/bin下，vi tomcat
``` bash
#!/bin/bash
case $1 in
  start)
    sh /Users/shayne/Development/Tomcat/bin/startup.sh
  ;;
  stop)
    sh /Users/shayne/Development/Tomcat/bin/shutdown.sh
  ;;
  restart)
    sh /Users/shayne/Development/Tomcat/bin/shutdown.sh
    sh /Users/shayne/Development/Tomcat/bin/startup.sh
  ;;
  *)
    echo "Usage: start|stop|restart"
  ;;
esac
exit 0
```
2. 赋予tomcat文件执行权限   
chmod 777 tomcat   
至此就可以随便在终端通过tomcat start，tomcat stop启用tomcat了
----
参考文章:   
[1] [macOS各个文件夹的作用](https://www.jianshu.com/p/0c08f2c7748d)
[2] [mac命令行启动tomcat](https://www.jianshu.com/p/37e857c5006d)