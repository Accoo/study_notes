# IntelliJ IDEA解决创建maven web项目慢的问题

使用idea创建maven web项目的时候，出现：

```
Executing external Maven 
Running C:\Users\user\AppData\Local\Temp\archetypetmp
```

导致创建项目特别慢。

解决办法： 
创建项目时候添加`archetypeCatalog=internal`参数即可，如下图所示、

![img](https://img-blog.csdn.net/20180226194204494?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYl94X3A=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)