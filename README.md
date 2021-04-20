# filebroswer
使用File Browser 搭建远程文件管理器  

1、安装filebrowser

tar -xvf linux-amd64-filebrowser.tar.gz  
mkdir -p /filebrowser  
mv filebrowser /filebrowser  

2、配置

（1）创建配置数据库

./filebrowser -d /filebrowser/filebrowser.db config init


（2）设置监听地址

./filebrowser -d /filebrowser/filebrowser.db config set --address 192.168.0.101



（3）设置监听端口

./filebrowser -d /filebrowser/filebrowser.db config set --port 80



（4）设置中文语言环境

./filebrowser -d /filebrowser/filebrowser.db config set --locale zh-cn



（5）设置日志文件位置

./filebrowser -d /filebrowser/filebrowser.db config set --log /filebrowser/filebrowser.log



（6）添加用户

./filebrowser -d /filebrowser/filebrowser.db users add test 123456 --perm.admin



3、启动

（1）编写service文件

vim /etc/systemd/system/filebrowser.service



ExecStart根据自己的实际目录修改
```  
[Unit]
Description=File Browser
After=network.target

[Service]
ExecStart=/filebrowser/filebrowser -d /filebrowser/filebrowser.db

[Install]
WantedBy=multi-user.target
```  


（2）启动及开机自启
```  
systemctl daemon-reload
systemctl start filebrowser
systemctl enable filebrowser
```  


4、浏览器访问

浏览器直接访问地址加我们设置的端口即可打开filebrowser的首页，然后可以使用上面我们创建的管理员账户添加普通账户设置账户访问目录访问权限等等操作


Ref: https://blog.csdn.net/ywd1992/article/details/93030495  

