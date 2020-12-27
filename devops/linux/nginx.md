# Nginx 配置指南
## 启动和管理
```
#启动命令
nginx

#控制
nginx -s [stop|reload]
```

## 配置
nginx安装目录一般在/etc/nginx/中
配置文件为nginx.conf,而该会配置文件可以通过命令导入其它路径下的配置.参考nginx.conf配置如下:
```
http {
        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}
```


### 缓存内容配置
```
# 在http标签下,添加proxy_cache_path配置项, 修改[path] 为缓存路径,[key] 一个标识.
    http {
    ...
    proxy_cache_path [path] keys_zone=[key]:10m;
```
通过在server标签指定 proxy_cache 启用缓存,配置示例
```
http {
    ...
    proxy_cache_path /data/nginx/cache keys_zone=mycache:10m;
    server {
        proxy_cache mycache;
        location / {
            proxy_pass http://localhost:8000;
        }
    }
}
```

参考
* [Nginx Content Caching](https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/)