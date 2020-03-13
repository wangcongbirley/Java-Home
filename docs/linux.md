

![](/images/常用linux命令.png)

## 基于CentOS7内核
- yum install：安装
- sudo：root权限 输入用户密码
- curl：综合传输工具/http命令行工具
- rpm：管理套件  -qa 使用询问模式，查询所有套件 -e删除指定的套件
- wget:下载文件
- tar:解压文件
- pwd:查看当前所在路径
- useradd：创建一个用户
- userdel:删除用户 userdel -rf name
- su：切换用户
- cp：拷贝
- chmod:更改权限
- PS：查看进程     ps -aux | grep ela
- mv：移动文件 mv oldfilename newfilename 重命名文件/文件夹
- mkdir:创建文件夹
- ls -l /home:查看用户是否成功建立
- systemctl stop firewalld.service：关闭防火墙
- chown -R 用户名 路径 ：给用户授权
- unzip：解压zip文件
- tar zxJf 解压包：解压tar.xz文件
- netstat：查看进程
- kill -9：杀死进程
- cd: ../../../ 多级父目录跳转

工具：SecureCRT的SSH远程登录。
命令：
ps
kill -9 端口号 强制杀死进程
cd
mv
pwd
systemctl get-default 查看默认启动方式
