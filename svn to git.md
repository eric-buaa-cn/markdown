本文档以demo项目为例，说明svn迁移git的过程。

## 一个完整的迁移过程如下：

1. 新建一个空目录
```bash
mkdir svnrepo
cd svnrepo
```

2. 制作作者映射文件。

svn作者格式与git作者格式有差异，这一步骤用于制作两者的映射文件。
```bash
svn log --quiet http://SVN_HOST/demo/ | grep -E "r[0-9]+ \| .+ \|" | cut -d'|' -f2 | sed 's/ //g' | sort | uniq | awk '{print $0" = "$0" <"$0".yy.com>"}' > authors.txt
```

3. 迁出svn库
```bash
git svn clone http://SVN_HOST/demo/ --authors-file=authors.txt --no-metadata build
```

4. 标签和分支的转换（如果有）
```bash
cd build
cp -Rf .git/refs/remotes/origin/tags/* .git/refs/tags/
rm -Rf .git/refs/remotes/origin/tags
cp -Rf .git/refs/remotes/* .git/refs/heads/
rm -Rf .git/refs/remotes
```

5. 指定远程仓库

远程仓库需要提前在Git上创建完成。
```bash
git remote add origin https://github.com/eric/demo.git
```

6. 推送到远程仓库
```bash
git push origin --all
```

7. 说明
> * 迁移过程中，原来svn库的空目录不再保留。
> * 迁移过程中，如果不幸遇到了git svn异常退出，请参考[这里](https://www.endpoint.com/blog/2010/05/13/continuing-interrupted-git-svn-clone)。
> * 当使用Gitlab时，legacy代码存在一个庞大的库中，如何像svn一样，仅下载一个子目录来查看（注意，这个子目录不能作为工作目录）呢？ 这依赖于GitLab的版本，[11.11](https://docs.gitlab.com/ee/user/project/repository/#download-source-code)支持了。
