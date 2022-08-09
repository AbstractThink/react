# react
优质文章收集

# hooks
[React Hooks工程实践总结](https://juejin.cn/post/6844904009220931598)

[React Hooks - 组件重新渲染原理](https://www.agora.io/cn/community/blog/best/22203)

[React Hooks源码解析，原来这么简单～](https://juejin.cn/post/6844904080758800392)

[React Hooks 原理与最佳实践](https://blog.csdn.net/howgod/article/details/107053862)

[React Hooks工程实践总结](https://juejin.cn/post/6844904009220931598#heading-5)

先简单说一下常见的git 分支管理策略

集中式工作流：类似于SVN管理方式，只有一个master分支，每个人将自己的代码提交到master上。

feature工作流：有一个主分支默认为master分支。每个人开发的时候基于master分支新建feature分支，然后提交到中央仓库，供大家code-review，通过之后merge进master分支

gitflow工作流：长期存在两个分支，一个master分支，一个develop分支，develop分支为日常开发分支，所有功能开发都基于develop分支，测试也基于develop，测试通过之后合并到master分支。

forking 工作流：这个工作流和其他工作流有本质不同，其他工作流都是有一个服务端仓库，forking工作流允许每个开发者有一个自己的服务端仓库。每个开发者可以将修改push到自己的服务端仓库，然后发起一个pull request 项目拥有者将修改更新到本地，测试通过之后，合并到自己本地的master分支，然后推送到公共仓库。

以上四种工作方式除了第一种不能使用pull request其他都可以。pull request 就是提交代码之后发起给团队其他人发起code review请求。

下面来具体说说gitflow 工作流，也是很多团队都在使用的工作流。
优点：就是打包上线，测试，开发，都很清晰。
gitflow工作流是由Vincent Driessen 提出的。其主要思想可以用如下图表示。
gitflow
在Gitflow 工作流中主要体现两个分支：
一个master分支，所有上线的版本全部由该分支打包。
一个develop分支，日常开发基于该分支。
gitFlow 日常工作流程图如下
gitflow-branch
下面介绍一下使用gitflow 工作流的常规操作。

将设我们开发一个新的feature-1
操作如下：
```
git checkout develop #切换到develop分支，保证最新。
git checkout -b feature-1 #新建feature-1分支，并切换到该分支做一堆修改，然后加入暂存区
```
```
git commit -m "compelete feature-1" #一次commit操作
git checkout develop #切回到develop分支
git pull --rebase #检查更新，并以rebase方式更新到本地
git checkout feature-1 #切回feature-1
git rebase develop #将develop rebase到feature-1
git push -u origin feature-1 #推送到服务端进行code review
```
code review #团队 code review，顺利通过。
```
git checkout develop #切回develop
git merge feature-1 #将feature-1 合并进develop
git push origin develop #将develop 推送到服务端
git push origin --delete feature-1 #删除分支
git branch -d feature-1 #删除本地分支
git checkout master #切回master分支
git merge --no-ff develop #将 develop 合并进master分支
```
以上是一次完整的功能开发。


