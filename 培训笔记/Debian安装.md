# Debian安装
连接别人的虚拟机ssh root@ip地址
1.首先更改成国内源（debian 9 源），改为中科大源。
2.将sudoers配置文件修改，将自己的账户添加进去（添加一行后将root改为wumengfei）：
sudo nano /etc/sudoers（yy复制，p将复制的粘贴带下一行）,sh命令切换到root目录
（Ctrl+d退出）。
3.ssh安装：sudo apt-get install ssh
4.在xshell上连接上直接的账户，进入 sudo nano /etc/apt/sources.list 将内面的链接修改为中科大的源。
5.将源更新一下：sudo apt-get update
5.vim 安装：sudo apt-get install vim

---
#基本命令
- rm 删除（加上-r之后就是对文件进行操作） 
- cd 切换目录
- mkdir -p 递归新建目录
- find 查找（慢，消耗资源大）
- locate 查找（快，消耗资源少）
- echo 输出（相当于print）
- ln 创建链接
- wget 下载文件 -c断点下载
- ls - lh 
- pwd 查看当前目录
- cat 查看文件内容
- | 通道符 将前面的结果作为参数传入后面
- cp 复制文件
- mv 移动文件
- grep 文本搜索工具
2.添加环境
- export PATH=$PATH:/.../...
- alias
3.vim的基本操作
- a i o 插入模式
- 正常模式
- 命令模式
    - :进入命令模式
    - :w 保存
    - :w! 强制保存
    - :q 退出
    - :q! 强制退出不保存
    - :wq 保存后退出
    - :wq! 强制保存后退出
    - :w [filename] 将文件另存为另一个文件
    - :r [filename] 在编辑的文件后面读入另一个文件的数据
- 查找与替换
    - /word 在光标后查找一个名为word的字符串
    - ?word 在光标后查找一个名为word的字符串

---
#xshell远程连接debian的root用户
- 首先修改配置文件 vim /etc/ssh/sshd_config
- 将PermitRootLogin 后面的东西改为yes，将注释去掉
- 重启sshd：systemctl restart sshd 
- 在Xshell上输入ip进入连接

#Note.js环境搭建
- 首先安装 git sudo apt install git
- 然后进行克隆 git clone httpd://github.com/cnpm/nvm.git
- 进入nvm：cd nvm
- 查看nvm.sh所在目录：pwd
- 修改配置文件：vim ~/.bashrc
- 在最后面（G）加上nvm.sh的目录地址并保存退出：source /home/nvm/nvm.sh
- 然后写source ~/.bashrc
- 最后敲nvm
- 然后就直接可以进行安装了：nvm install 10.5.0
    
---
#mongodb数据库的安装
1.安装mongodb：sudo apt-get install mongodb
2.创建一个目录来放置数据库：mkdir -p /wmf/mongodb/db
3.安装tmux：sudo apt-get install tmux
4.停止mongodb服务：systemctl stop mongodb
5.关闭开机自启动：systemctl disable mongodb
6.进入tmux：tmux
7.进入之后敲 mongodb --dbpath /root/wmf/mongondb/db
8.然后退出tmux：Ctrl+B  松手后敲D
9.进入mongodb：mongo

---
#mongodb的使用（增删改查）
1.新建一个数据库：use 名称（mydb）
2.show dbs  查看已经有的数据库
3.db 查看当前的数据库
4.显示当前集合：show collections
5.增加：db.students.insert({"名称":"内容"})
7.查看表格内容：db.students.find()
7.删除数据库：db.dropDatabase()
8.删除表格：db.students.drop()
9.删除数据：db.students.remove({"名称":"内容"})
10.修改：db.students.update({"名称":"内容"},{"名称":"修改后的内容"})
