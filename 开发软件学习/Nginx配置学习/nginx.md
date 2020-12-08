# nginx同个域名部署多个工程

## conf配置文件如下：

```
server {
    listen 8080;
    server_name ****.*****.com;
    root /home/work/***/static/client;
    index index.html;
    autoindex on;
    charset   utf-8;

    location ~ /(system|car)/ {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://192.168.1.1:8851;
    }

    #配置Nginx动静分离，定义的静态页面直接从Nginx发布目录读取。
    location /admin {
        alias /home/work/****/static/admin/;
        #expires定义用户浏览器缓存的时间为7天，如果静态页面不常更新，可以设置更长，这样可以节省带宽和缓解服务器的压力
        expires  1d;
        index index.html;
	autoindex on;
    }

    access_log /home/work/****/logs/static_admin_ng_access.log;

    location /api/ {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://192.168.1.1:8851;
    }
    #配置Nginx动静分离，定义的静态页面直接从Nginx发布目录读取。
    location /client {
        alias /home/work/****/static/client/;
        #expires定义用户浏览器缓存的时间为7天，如果静态页面不常更新，可以设置更长，这样可以节省带宽和缓解服>务器的压力
        expires  1d;
        index index.html;
	autoindex on;
    }
    access_log /home/work/****/logs/static_client_ng_access.log;

}
```



## 出现问题

### 访问一直404



## 问题解决：

### alias 和 root 的区别； root 的话；location 中的地址会拼接到root后面；alias就直接代替后面的东西

```
如：
location /admin {
root  /admin/res/;
index html.html;
autoindex no;
}


location /admin {
alias /admin/res/;
index html.html;
autoindex no;
}

访问地址：localhost:8080/admin/res/app.js;

root实际访问的地址就是： localhost:8080/admin/res/admin/res/app.js

也就是说这个实际访问的地址 ./admin/res/admin/res/app.js ；这样根本找不到文件；

alias 实际的访问地址就是： localhost:8080/admin/res/app.js;

访问的地址是  ./admin/res/app.js

```

