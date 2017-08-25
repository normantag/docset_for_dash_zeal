# docset for dash/zeal



## 生成docset

Dash/Zeal 本身只支持 docsets 格式的文档，也就是由 [appledoc](http://gentlebytes.com/appledoc/) 生成的，但是目前有多种工具，可以把常见语言的文档格式转成 docsets 格式

以python为例，下面我们为 scikit learn 生成可供 Dash/Zeal 查看的文档

大部分python文档都是Sphinx格式的，使用python Sphinx库就可以将其转换成各种常见格式的文档，比如html ps等，scikit learn也使用Sphinx格式

开源工具 doc2dash 可以将sphinx生成的html格式文档转换成docsets格式，所以我们只需要先生成html格式的文档，然后使用doc2dash转换成



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



### 参考

https://kapeli.com/docsets#python

https://doc2dash.readthedocs.io/en/stable/usage.html