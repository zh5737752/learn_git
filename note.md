# 主题：Git 学习

## 创建版本库

1. 创建新文件夹，在文件夹空白处右键点击Open git bash here
2. 通过`git init`命令把这个目录变成Git可以管理的仓库:`$ git init`

## 把文件添加到版本库

1. 用命令`git add`告诉Git，把文件添加到仓库：  

   `$ git add readme.txt`

2. 用命令`git commit`告诉Git，把文件提交到仓库：  

   `$ git commit -m "wrote a readme file`

## 时光机穿梭

### 基础查看

1. 查看工作区状态（能看到文件是否被修改）：`git status`  

   `$ git status`

2. 查看文件具体修改了什么内容：`git diff`  

   `$ git diff readme.txt`

### 版本回退

1. 用`git log`查看历史记录  

   `$ git log`  

   如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：  

   `$ git log --pretty=oneline`

2. 版本回退，用`git reset`.  

   在Git中，用HEAD表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，然往上100个版本写成`HEAD~100`  

   `$ git reset --hard HEAD^`

   `--hard`会回退到上个版本的已提交状态，而`--soft`会回退到上个版本的未提交状态，`--mixed`会回退到上个版本已添加但未提交的状态  
   退回后，新版本[^消失]  

3. 用版本号指定[^回到新版本]

   `$ git reset --hard 1094a`  
  
4. 查看文件内容`cat`  

   `$ cat readme.txt`

5. 找不到版本的commit id,用git reflog用来记录你的每一次命令：

   `$ git reflog`

- **总结**：
  - HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
  - 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
  - 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。



[^消失]: 好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了  
[^回到新版本]: 指定回到21世纪

### 工作区和缓存区

### 管理修改

每次修改，如果不用git add到暂存区，那就不会加入到commit中

### 撤销修改

- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命`git restore --staged <file>`，就回到了场景1，第二步按场景1操作。

- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库