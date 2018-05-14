### 有网的时候：

**1、建立一个远程仓库**

**2、将远程仓库克隆到本地（git clone 网址）//shift+insert 复制**

3、git config --list //查看配置

4、git config --(加入自己的邮箱和名字)

**5、在本地仓库中增添内容**

**6、git status //查看状态**
   //git config --global core.quotepath false 解决中文问题

**7、将工作区的内容添加到到暂存区**
  （1、git add .//将全部文件添加到暂存区 2、git add 文件名//将指定的文件添加到暂存区）

8、git status //查看状态

**9、将暂存区的内容提交到远程仓库（git commit -m "提交说明"）**

10、git log  查看状态
或者 git log --oneline 将查看的状态显示在一行

11、git remote -v 查看远程信息

**12、将本地仓库的内容推送到远程仓库 （git push origin master）** 

---

### 没网的时候：	

**1、在本地初始化仓库（git init）**

2、参考上面的步骤（2—10步）

**3、有网的时候在GitHub上建立一个远程仓库**

**4、本地仓库和远程仓库建立联系（git remote add origin 网址）**

5、git remote -v 查看远程信息
**6、将本地仓库的内容推送到远程仓库 （git push origin master）**