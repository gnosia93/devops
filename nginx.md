```
$ sudo systemctl enable nginx
Created symlink from /etc/systemd/system/multi-user.target.wants/nginx.service to /usr/lib/systemd/system/nginx.service.
$ sudo service nginx start
$ service nginx status
Redirecting to /bin/systemctl status nginx.service
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
   Active: active (running) since 수 2019-02-06 20:39:22 KST; 3s ago
  Process: 3300 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
  Process: 3297 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
  Process: 3294 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
 Main PID: 3301 (nginx)
    Tasks: 9
   Memory: 10.6M
   CGroup: /system.slice/nginx.service
           ├─3301 nginx: master process /usr/sbin/nginx
           ├─3302 nginx: worker process
           ├─3303 nginx: worker process
           ├─3304 nginx: worker process
           ├─3305 nginx: worker process
           ├─3306 nginx: worker process
           ├─3307 nginx: worker process
           ├─3308 nginx: worker process
           └─3309 nginx: worker process
           
$ sudo firewall-cmd --permanent --zone=public --add-service=http 
$ sudo firewall-cmd --permanent --zone=public --add-service=https
$ sudo firewall-cmd --reload        
```
