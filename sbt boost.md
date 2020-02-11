### 问题标签
* sbt慢
* 国内maven仓库
* sbt 302
* sbt http redirect

### 背景
sbt操作时需要从网络下载众多jar包，会导致其响应很慢。
网上流传一个曾经可行的方案：[配置国内aliyun maven仓库](https://blog.csdn.net/liu3237/article/details/58149934)，来加快jar包下载速度。
但是，由于aliyun仓库利用CDN，对jar包访问进行了302跳转，由于sbt launcher的一个[bug](https://github.com/sbt/sbt/issues/5059)，这个方案目前并不一定好使。

最直接的解决方法，是升级sbt代码来支持http redirect。但是sbt源码编译有些复杂，本人曾经尝试编译sbt 1.3.x分支代码，并没有编译成本。针对aliyun 302跳转，这里给出一个基于http proxy的补充方案。

测试环境为Mac。
步骤如下：

1. 安装nginx，作为http代理。
```bash
brew install nginx
```

2. 配置nginx.conf (位置 /usr/local/etc/nginx/nginx.conf)，添加如下配置：
```
    server {
        listen      8081;
        charset     utf-8;

        location / {
            proxy_pass https://maven.aliyun.com/nexus/content/groups/public/;
            proxy_intercept_errors on;
            error_page 301 302 307 = @handle_redirects;
        }

        location @handle_redirects {
            set $orig_loc $upstream_http_location;
            proxy_pass $orig_loc;
            resolver 8.8.8.8;
        }
    }
```

3. 配置~/.sbt/repositories，如下：
```
[repositories]
#使用ivy本地缓存
local
#使用maven本地缓存
maven-local
#使用本地的http proxy，可以处理302 http redirect
aliyun: http://127.0.0.1:8081/
typesafe: https://repo.typesafe.com/typesafe/ivy-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
sonatype-oss-releases
maven-central
sonatype-oss-snapshots
```

4. 启动 & 关闭Nginx
```bash
launchctl load /usr/local/Cellar/nginx/1.17.8/homebrew.mxcl.nginx.plist
launchctl unload /usr/local/Cellar/nginx/1.17.8/homebrew.mxcl.nginx.plist
```

### 参考
[https://gist.github.com/sirsquidness/710bc76d7bbc734c7a3ff69c6b8ff591]
[https://gist.github.com/JonasGao/89370dc9cf84f4bbc1131fce2e700635]
