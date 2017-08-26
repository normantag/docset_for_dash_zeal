# docset for dash/zeal



## docset 简介

Dash/Zeal 本身只支持 docsets 格式的文档，也就是由 [appledoc](http://gentlebytes.com/appledoc/) 生成的文档格式，打开看一下会发现，docset其实是一个文件包，可以分为几个部分

- Documents 文件夹，里面存放着API文档的实际内容，可能会很大
- 配置文件有 meta.json Info.plist 和 docSet.dsidx，
  - meta.json Info.plist 这两个文件里记录了一些配置信息，无非是该docset的名字 发布者等，使用文本编辑器打开，按照其他docset的形式改一下就可以了，
  - docSet.dsidx这个文件比较重要，它是一个记录着查找索引的SQLite数据库，无法简单的修改得到，但目前针对各种语言，都有工具生成这个数据库文件

目前有多种工具，可以把常见语言的文档格式转成 docsets 格式。下面以python为例，我们为 scikit learn 生成可供 Dash/Zeal 查看的文档



## python文档转换成 docsets

大部分python文档都是Sphinx格式的，使用python Sphinx库就可以将其转换成各种常见格式的文档，比如html ps等，scikit learn也使用Sphinx格式

开源工具 doc2dash 可以将sphinx生成的html格式文档转换成docsets格式，所以我们只需要先生成html格式的文档，然后使用doc2dash转换成docsets即可

步骤很简单，如下：

###  安装依赖库

```
$ pip install sphinx
$ pip install doc2dash
```

### 生成html格式的文档

到 scikit learn 的github仓库下载源码，最好下载release的代码，master分支下代码可能有bug，导致编译失败，下载完成后，执行命令生成文档

```shell
$ cd scikit-learn-0.18.1\doc
$ make.bat html
```

### 使用 doc2dash 将html文档转换成docsets格式

 ```shell
$ doc2dash --name sklearn --icon flask-logo.png -d path/to/output scikit-learn-0.18.1/doc/_build/html
 ```

### 拷贝docset

最后将生成的docset拷贝到Dash/Zeal对应的文档目录即可（通过配置可以看到文档存储目录）



## 编译好的docset

我已经编译好了部分docset，存放在本仓库中，目前收录的有：

- scikit learn v0.18.1 http://scikit-learn.org
- scikit learn cn v0.17 中文翻译版 基于 https://github.com/lzjqsdd/scikit-learn-doc-cn



欢迎大家共享自己的docset



### 参考

https://kapeli.com/docsets#python

https://doc2dash.readthedocs.io/en/stable/usage.html