# Docker PHP-FPM For WordPress
从[dnmp](https://github.com/yeszao/dnmp/)拆出来的 PHP-FPM 容器，适用于 WordPress，与 Nginx Docker 容器配合使用。
## 介绍
PHP-FPM 容器，目前版本 PHP 7.4.7，添加了 WordPress 可能用到的扩展。
## 使用

### 修改目录映射

按需修改 docker-compose.yml 中的目录映射。
> 某些情况下 Nginx 中的 www 目录可能需要与 PHP-FPM 容器中的路径保持一致（容器内路径）。

### 编译镜像并拉起容器
```
docker-compose up -d
```
### 连通 Nginx 网络
将 PHP-FPM 容器加入 Nginx 所在的网络；

在 Nginx 容器中使用 ping 命令检查是否连通：
```
# ping php service
ping php74
```
### 修改 Nginx PHP 反代地址
将 Nginx 配置文件中对应网站的 PHP 反代地址改成 `[service name]:9000`，例如`php74:9000`。
```bash
location ~ \.php$ {
    fastcgi_pass   php74:9000; #本行
    # [省略其他内容]
}
```
### 重启 Nginx
重启 Nginx 容器。