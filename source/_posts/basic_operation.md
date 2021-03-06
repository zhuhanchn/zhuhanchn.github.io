---
title: Hexo博客基本操作
date: 2019-08-18 14:59:58
tags: 
	- Hexo

cover: https://i.loli.net/2019/08/18/bWKhYjdJ6iRVDTv.png

---

## 参考的教程与主题模板，感谢各位大大~

- 博客搭建教程：https://www.lixint.me/hexo-blog.html
- 使用的主题（hexo-theme-butterfly）的文档：https://jerryc.me/posts/21cfbf15/#%E5%BF%AB%E9%80%9F%E9%96%8B%E5%A7%8B

## Hexo重要的命令和操作

### 基本流程（修改、更新和发布）
- 搭建电脑：
```bash
hexo clean #清除缓存
hexo g  #保存修改，生成文件
hexo s  #启动本地服务
hexo d  #发布到远程
```
- 非搭建电脑：
```bash
git add .
git commit -m "..."
git push
hexo d -g
hexo s
```

**注意： 每次换电脑进行博客更新时，不管上次在其他电脑有没有更新，**
      **最好先在username.github.io文件夹下 git bash 中进行 git pull**

> 使用git clone出现 fatal: unable to access 'https://github.com/...'的解决办法:
取消代理：
git config --global --unset http.proxy 
git config --global --unset https.proxy 

- 修改之后-> 在username文件夹下 -> hexo g -> hexo s -> 打开http://localhost:4000 查看 -> hexo d -> 打开https://username.github.io/ 查看

- 修改站点配置文件、主题配置文件（Butterfly的主题配置文件在G:\username\source\_data\butterfly.yml）、修改文章等操作之后，按照上诉步骤执行就可以~

- **如果是在非搭建的电脑上进行更新：**
  - localhost查看更新内容：修改之后 -> 在username.github.io文件夹下（目录中git branch的结果是*hexo）-> hexo s -> 打开http://localhost:4000 查看 即可！ 超方便的~
  - 上传更新：修改之后 -> 在username.github.io文件夹下（目录中git branch的结果是*hexo）-> git add . -> git commit -m 'back up hexo files'（引号内容可改）-> git push (保证hexo分支版本最新) -> hexo clean (可选) -> hexo d -g (将最新改动更新到master分支) -> hexo s -> 打开https://username.github.io/ 查看
  - 参考资料：https://www.jianshu.com/p/0b1fccce74e0

- **多台电脑同步使用时，对于搭建电脑的操作：**
    - 多台电脑同时更新之后，搭建电脑的操作（修改博文、发布到远端）也都应该在username.github.io文件夹下，而非原本的username文件夹下了~ 不过再搭建电脑上的提交操作，只需要hexo g -> hexo d -> hexo s 三个步骤即可

### git pull 有冲突

注意看git pull之后提示的信息，如果有**CONFLICT**，请先解决冲突问题，然后commit和push
```bash
（git add .）
git commit -m "..."
git push
hexo d -g
hexo s
```

若是不允许git pull操作：
- 保留本地的修改的做法：

    ```bash
    git stash # 先将本地修改存储起来
    （git stash list # 可以查看保存的信息，显示Git栈内的所有备份）
    git pull
    git stash pop # 还原暂存的内容
    （git stash clear # 清空Git栈）
    ```

- 放弃本地修改的做法:
    
    ```bash
    git reset --hard # 将本地的冲突文件冲掉，回到先前的那一个提交，后面可加版本号
    git pull
    ```

    （好好看CONFLICT的内容，打开冲突的文件选定需要的版本，保存，然后 （git add .） -> git commit -m "xxx" -> git push， 将选定的版本推上去）
    commit和push完了之后，应该不会在hexo-merge下面，如果在这个下面，可以尝试git reset --hard / git merge --abort(当没有文件需要合并,中止)等操作（应该是不用的）。
    
    
### 新建文章
- 在G:\username\source\_posts 路径下面，新建md文件，编辑md文件，编辑好之后采用上面的基本流程就可以发布
- 注意在md文件的开始处添加下列配置内容，可以在其中设置标签、分类等

```md
---
title: Hexo博客基本操作
date: 2019-08-18 14:59:58
tags: 
	- Hexo
	- markdown

cover: https://i.loli.net/2019/08/18/3q2WiZL9N7IdoC1.png

---
```
- 注意有网址的地方的空行操作，不然可能会识别错误。
- 配置文件一样会被pull更新，可以更改开头的内容，但注意，更新完一篇文章之后务必保存并关闭文件，下次请打开pull之后的最新文件进行修改！不要在之前的版本上反复修改！！

### 主题配置文件更改 butterfly.yaml

<div style='display: none'>
哈哈我是注释，不会在浏览器中显示:
- 在搭建的电脑上，对G:\username.github.io\source\_data\butterfly.yaml 进行修改，然后只需要hexo g -> hexo d -> hexo s，就可以更新到远端。但是很神奇的一点是，github上面，无论是hexo分支下面还是master分支下面，找不到更新的yaml的内容，应该是直接写成了html的内容更新到了master中。
- 所以在其他电脑上git pull之后，都不能更新localhost中显示的主题样式，但是https://username.github.io/ 中显示的是最新的主题。
- 如果想要改变其他分支电脑上的localhost的主题显示，可以直接更改分支电脑上的../username.github.io/source/_data/butterfly.yaml 文件，可改变localhost的主题显示。
- 所以，主题请在搭建电脑上更新，并发布到远端，G:\username.github.io\source\_data\butterfly.yaml下的文件始终是最新文件，git pull也不会改变它。更改该文件，并hexo g -> hexo d -> hexo s，即可写入master的html文件中，体现在https://username.github.io/ 的显示中。
</div>

- **在任意一台电脑上的\username.github.io\source\_data\butterfly.yaml 进行修改，**
    - 对于搭建电脑，只需要hexo g -> hexo d -> hexo s，就可以更新到远端。
    - 对于非搭建电脑，git add . -> git commit -m 'back up hexo files'（引号内容可改）-> git push (保证hexo分支版本最新) -> hexo clean (可选) -> hexo d -g (将最新改动更新到master分支) -> hexo s （此步骤一定不能省） -> 打开https://username.github.io/ 查看 即可
    - 将Butterfly的yaml配置文件拷到source文件夹下面的好处就是用git push就可以在不同电脑上同步更新，github上面的仓库会更新，注意每台电脑git pull没有报错就可以啦。
    - github.io刷新出的内容显示有延迟，localhost的实时显示
    - 注意看git pull之后提示的信息，如果有**CONFLICT**，请先解决冲突问题，然后commit和push
--------------------

```bash
hexo init #生成站点
hexo new page "xxx" #生成页面
hexo new "" #生成文章
npm install --save xxx  #安装插件
npm unstall xxx #卸载插件

```

## 主题修改
### 下载
git clone https://github.com/iissnan/hexo-theme-next themes/next

### 建议： 
若想多端同步修改博客，最好先将此主题fork到自己github仓库，再下载。否则，无法对主题进行push，此处有坑，若无此需求，无视

### 启用
主题文件拷贝到themes目录下

- 站点配置文件 
  theme：next 
  hexo generate 保存

- 主题配置文件 
  打开任意一项

```yaml
    # Schemes
    scheme: Muse
    #scheme: Mist
    #scheme: Pisces
    #scheme: Gemini
```

主题建议部分的原文链接：https://blog.csdn.net/tianbo_zhang/article/details/79137103

