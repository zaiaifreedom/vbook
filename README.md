# 前言

本书使用 [gitbook](https://www.gitbook.com/) 来记录学习的过程，使用方法见 [文档](https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md) 

# gitbook 的使用

- 安装

```
npm i -g gitbook-cli
```

- 新建

提前把父目录和 github 中的 gitpage-master分支进行关联
```
mkdir mybook
cd mybook
gitbook init
```

- 热预览

```
gitbook serve --port 4000
```

- 打包

```
gitbook build [书籍目录] [打包目录]
```

- 提交

.gitignore 中忽略一些文件
```
git add .
git commit -m '提交信息'
git push
```

- 其他生成格式

```
生成 PDF 格式的电子书：

$ gitbook pdf ./ ./mybook.pdf

生成 epub 格式的电子书：

$ gitbook epub ./ ./mybook.epub

生成 mobi 格式的电子书：

$ gitbook mobi ./ ./mybook.mobi

``` 

- [插件](https://plugins.gitbook.com/)

参考官方 （https://toolchain.gitbook.com/plugins/）
参考示例 （https://blankj.com/gitbook/gitbook/）

```
gitbook install ./
```


