# VMWare16Pro



## 安装VMWare16Pro

VMWare16pro 

- 下载：https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html

- 激活码

  ```
  ZF3R0-FHED2-M80TY-8QYGC-NPKYF
  ```

  

## 安装Ubuntu

Ubuntu20.04

- http://releases.ubuntu.com/20.04/





参考：https://blog.csdn.net/maxg1206/article/details/105919344/







```
        #websocket代理配置如下
        location /ws/ {
            proxy_redirect    off;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;	
            proxy_pass http://127.0.0.1:8000/;  

            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
```



```
location ^~ /ws {	
	       proxy_pass http://127.0.0.1:8000/ws;  
	
	       proxy_http_version 1.1;
	       proxy_set_header Upgrade $http_upgrade;
	       proxy_set_header Connection "upgrade";
	   }
```





```
uWSGI+nginx启动项目,http请求可用,websocket请求错误
```





- Django使用uWSGI采用部署时，Websocket在本地可以用，使用Nginx+uWSGI部署时不能运行
