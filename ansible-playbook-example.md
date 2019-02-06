## Nginx Playbook ##
```

- hosts: localhost
  tasks:
     - name: installs nginx web server
       yum: name=nginx state=installed update_cache=true
       notify:
         - start nginx

  handlers:
     - name: start nginx
       service: name=nginx state=started
     
```
> ansible-playbook nginx.yml --user root -vvv
> service nginx status

