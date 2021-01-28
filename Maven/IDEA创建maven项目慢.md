# IDEA创建maven项目慢

在maven的VM Options加上-DarchetypeCatalog=internal参数，步骤如下：

打开idea的启动界面，进入全局设置
![img](https://img2018.cnblogs.com/blog/1478697/201901/1478697-20190124142735864-1061899915.png)

搜索maven，点击Runner一栏，在VM Options输入框里写上 “-DarchetypeCatalog=local”，

![img](https://img2018.cnblogs.com/blog/1478697/201901/1478697-20190124142814319-1910702367.png)

确定后，再新建maven项目，就能发现项目很快就创建完成。