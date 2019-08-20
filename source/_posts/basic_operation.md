---
title: Hexo博客基本操作xxx
date: 2019-08-18 14:59:58
tags: 
	- Hexo

cover: https://i.loli.net/2019/08/18/bWKhYjdJ6iRVDTv.png

---

## 参考的教程与主题模板，感谢各位大大~

- 博客搭建教程：https://www.lixint.me/hexo-blog.html
- 使用的主题（hexo-theme-butterfly）的文档：https://jerryc.me/posts/21cfbf15/#%E5%BF%AB%E9%80%9F%E9%96%8B%E5%A7%8B

## Hexo重要的命令和操作

### 基本流程
```yaml
hexo clean #清除缓存
hexo g  #保存修改，生成文件
hexo s  #启动本地服务
hexo d  #发布到远程
```
- 修改之后-> 在username文件夹下 -> hexo g -> hexo s -> 打开http://localhost:4000 查看 -> hexo d -> 打开https://username.github.io/ 查看

- 修改站点配置文件、主题配置文件（Butterfly的主题配置文件在G:\username\source\_data\butterfly.yml）、修改文章等操作之后，按照上诉步骤执行就可以~

- **如果是在非搭建的电脑上进行更新：**
  - localhost查看更新内容：修改之后 -> 在username.github.io文件夹下（目录中git branch的结果是*hexo）-> hexo s -> 打开http://localhost:4000 查看 即可！ 超方便的~
  - 上传更新：修改之后 -> 在username.github.io文件夹下（目录中git branch的结果是*hexo）-> git add . -> git commit -m 'back up hexo files'（引号内容可改）-> git push (保证hexo分支版本最新) -> hexo clean (可选) -> hexo d -g (将最新改动更新到master分支) -> 打开https://username.github.io/ 查看
  - 参考资料：https://www.jianshu.com/p/0b1fccce74e0

**注意： 每次换电脑进行博客更新时，不管上次在其他电脑有没有更新，最好先git pull**

### 新建文章
- 在G:\zhuhanchn\source\_posts 路径下面，新建md文件，编辑md文件，编辑好之后采用上面的基本流程就可以发布
- 注意在md文件的开始处添加下列配置内容，可以在其中设置标签、分类等

```
---
title: Hexo博客基本操作
date: 2019-08-18 14:59:58
tags: 
	- Hexo
	- markdown

cover: https://i.loli.net/2019/08/18/3q2WiZL9N7IdoC1.png

---
```
注意有网址的地方的空行操作，不然可能会识别错误。

--------------------

```yaml
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

