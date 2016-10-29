---
title: Hexo 源码备份与恢复
---

###一、需求：

很多情形都需要对Hexo进行管理和更新，或者进行重新部署环境。

###二、思路

创建分支，一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页。

###三、搭建的流程

1、在github上创建仓库，yourname.github.io;

2、在本地创建yourname.github.io;

3、在本地yourname.github.io文件夹下一次执行npm install hexo、hexo init、npm install 和 npm install hexo-deployer-git;

4、在本地yourname.github.io文件夹下创建文件.gitignore, 这个文件是没有后缀的，打开后写入下面两个文件夹:

/.deploy_git

/node_modules

deploy_git就是hexo d渲染并上传到github发布出去的，每次hexo d都会全部覆盖；

/node_modules就是npm install生成的插件等，没必要上传，而且也上传不了。

备注：

刚开始好多备份的教程都没有说明.gitignore文件，在恢复之后，进行hexo d之后老是报错，发在邮箱里的错误内容
github给邮箱发送的内容，说：有模块没有初始化，在这里所指的就是.deploy_git这个模块

- git初始化:
git init
- 创建hexo分支，用来存放源码:
git checkout -b hexo
- git 文件添加:
git add .
- git 提交:
git commit -m "init"
- 添加远程仓库:
git remote add origin git@github.com:yourname/yourname.github.io.git
- push到hexo分支:
git push origin hexo


5、修改_config.yml中的deploy参数，分支应为master;
6、依次执行git add .、git commit -m “…”、git push origin hexo提交网站相关的文件;
7、执行hexo g -d生成网站并部署到GitHub上
这样一来，在GitHub上的Git@github.com:yourname/yourname.github.io.git仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。

###四、恢复

当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：

1、先安装hexo

$ npm install -g hexo-cli

2、存在github上的git clone下来 

git clone git@github.com:yourname/yourname.github.io

3、项目文件夹下npm 

cd 项目名/ 

$ npm install –no-bin-links 

$ npm install hexo-deployer-git

4、重新配置github和coding的公钥


###五、更新

每次写作之后 
先执行hexo d，把要发布的内容push到github上面了，再去弄备份