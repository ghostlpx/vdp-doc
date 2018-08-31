# 服务器部署

### 1.首次部署
首次部署需要下载完整代码，返回到应用列表中。  
``1）点击下载链接，下载代码。``    
``2) 解压压缩包。``    
``3）将压缩包中的文件全部拷贝到目标服务器根（java项目对应的目录是webapp）目录，将站点默认页面指向index.html。``    
``4) 如果出现资源无法访问的情况，请检查系统全局设置中静态资源目录和站点目录结构是否匹配。``  

### 2.页面新增，修改后部署
  首次需要拷贝完整包，以后页面的任意修改，在不需要升级核心代码的情况下做如下操作：  
``1）应用列表中查看代码，全部复制``  
``2）替换目标服务器下index.html中的内容``

### 3.nginx下BrowserRouter路由方式配置

#### 参考配置如下：{docsify-ignore}

```js
server {
  listen 80;
  server_name localhost;
  location / {
    root /usr/local/nginx/html/vdp/dist;
    index index.html index.htm;
    proxy_set_header Host $host;
    proxy_set_header X - Real - Ip $remote_addr;
    proxy_set_header X - Forwarded - For $remote_addr;
    try_files $uri $uri / /index.html;
    location~ * \.(eot | ttf | woff | svg | otf) $ {
      add_header Access - Control - Allow - Origin * ;
      add_header Access - Control - Allow - Headers X - Requested - With;
      add_header Access - Control - Allow - Methods GET, POST, OPTIONS;
    }
  }
}
```

