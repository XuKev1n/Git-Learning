### 第一阶段

git版本控制分几步走（git管理文件夹）

1.进入要管理的文件夹（进入）

2.初始化（提名）

3.管理

4.生成版本

*****************************************

使用到的命令

1、进入要管理的目录

2、git init 初始化，即：让git帮助我们管理当前文件夹

3、git status 检测当前目录下文件的状态

4、三种状态的变化

@1红色：新增的文件、修改了的文件——》git add 文件名

git add .

@2绿色：git已经管理起来—— 》git commit -m’描述信息’

@3生成版本

***************************************************************************************************************************

笔记整理

想要让git对一个目录进行版本控制需要以下步骤：

进入要管理的文件夹

执行初始化命令

```
git init
```

管理目录下的文件状态

```
git status
注：新增的文件和修改过后的文件都是红色
```

管理指定文件（红变绿）

```
git add 文件名
git add .
```

个人信息配置：用户名、邮箱【一次即可】

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

生成版本

```git
git commit -m '描述信息
```

查看版本记录

```
git log
```

********************

三大区域：工作区、缓存区、版本库

*******************

### 第二阶段

```
git add
git commit -m '新功能'
```

### 第三阶段

回滚至之前版本

```
git log
git reset --hard + 版本号
```

******

回滚至之后版本

```
git reflog
git reset --hard + 版本号
```

小总结

```
git init 
git add
git commit
git log
git reflog
git reset --hard 版本号

git checkout对修改的文件有效
git reset HEAD暂存区回到工作区 绿变红
其他见截图
```

***

补充：分支的思想

****************

###  第四阶段

开发商城功能

bug紧急修复：创建一个新的分支 然后合并到主分支去

默认主干线：master

*基于分支修复线上bug的具体过程

*************

命令总结和工作流

查看分支

 - 查看分支

   ```
   git branch
   ```

- 创建分支

  ```
  git branch + 分支名称
  ```

- 切换分支

  ```
  git checkout 分支名称
  ```

- 分支合并（可能产生冲突）

  ```
  git merge 要合并的分支
  注意：切换分支再合并
  ```

- 删除分支

  ```
  git branch -d 分支名称
  ```

#### 工作流

master（正式）

dev（开发）

***********

### 第五阶段

```
1、给远程仓库起别名
	git remote add origin 远程仓库地址
2、向远程推送代码
	git push -u origin 分支名
3、克隆远程仓库的代码
	git clone 远程仓库地址（内部已实现git remote add origin 远程仓库地址）
4、切换分支
	git checkout 分支名
```

*******

   在家里上传代码

```
1.给远程仓库起别名
	git remote add origin 远程仓库地址
2.向远程推送代码
	git push -u origin 分支
```

到公司新电脑上第一次获取代码

```
1.克隆远程仓库代码
	git clone 远程仓库地址（内部已实现git remote add origin 远程仓库地址）
2.切换分支
	git checkout 分支
```

在公司进行开发

```
1.切换到dev分支进行开发
	git checkout dev
2.把master分支合并到dev【仅一次】
	git merge master 
3.修改代码
4.提交代码
	git add .
	git commit -m 'xx'
	git push origin dev
```

回到家中继续写代码

```
1.切换到dev分支进行开发
	git checkout dev
2.拉代码
	git pull origin dev
3.继续开发
4.提交代码
	git add 
	git commit -m 'xx'
	git push origin dev
```

在公司继续开发

```
1.切换到dev分支进行开发
	git checkout dev
2.拉代码
	git pull origin dev
3.继续开发
4.提交代码
	git add
	git commit -m 'xx'
	git push origin dev
```

开发完毕，要上线

```
1.将dev分支合并到master，进行上线
	git checkout master
	git merge dev
	git push origin mater
2.把dev分支也推送到远程
	git checkout dev
	git merge master
	git push origin dev
```

```
git pull origin dev
等同于
git fetch origin dev
git merge origin/dev
```

**********

##### rebase(变基)

使git记录变简洁 

- 第一种应用场景
  - 多个记录——>一个记录
    
    ```
    git rebase -i HEAD~3
    git rebase -i 版本号
    ```
    
    - 注意：合并纪录时不要和已push到仓库的合并，合并的是那些没有提交到仓库的提交记录
- 第二种应用场景
- 第三种应用场景

***

####  快速解决冲突

1.安装Beyond Compare

2.在git中配置

```
git config --local merge.tool bc3
git config --local mergetool.path 'xxx/xxx/xxx'
git config --local mergetool.keepBackup false
```

3.应用Beyond Compare 解决冲突

```
git mergetool
```

****

#### 总结

- 添加远程连接

  ```
  git remote add origin 地址
  ```

- 推送代码

  ```
  git push origin dev(推送到的分支)
  ```

- 下载代码

  ```
  git clone 地址 （所有分支都下载了）
  ```

- 拉去代码（更新本地代码）

  ```
  git pull origin dev
  等价于
  git fetch origin dev
  git merge origin/dev
  ```

- 保持代码提交整洁（变基）

  ```
  git rebase 分支
  ```

- 记录的图形展示

  ```
  git log --graph --pretty=format:"%h %s"
  ```

  