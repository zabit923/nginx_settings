# nginx_settings



# для 80

    server {
        listen 80;
        server_name 127.0.0.1:8000;
        access_log  /var/log/nginx/example.log;
    
    
        location /static/ {
              root /home/user/project/project;
              expires 30d;
        } 
    
        location /media/ {
      	    root /home/user/project/project;
      	    expires 30d;
        }
    
        location / {
      	    proxy_pass http://127.0.0.1:8000;
      	    proxy_set_header Host $server_name;
      	    proxy_set_header X-Real-IP $remote_addr;
      	    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      	    proxy_set_header Referer $http_referer;
      	    proxy_set_header Origin $scheme://$host; 
        }
    }





# для 443

    server {
        listen 80;
        server_name 127.0.0.1:8000;
        return 301 https://$project.ru$request_uri;
    }
    
    server {
        listen 443 ssl;
        ssl on;
        ssl_certificate /etc/nginx/ssl/crt.crt;
        ssl_certificate_key /etc/nginx/key.key;
        server_name 127.0.0.1:8000;
        access_log  /var/log/nginx/example.log;
    
        location /static/ {
            root /home/user/project/project;
            expires 30d;
        }
    
        location /media/ {
          	root /home/user/project/project;
          	expires 30d;
        }
    
    
        location / {
            proxy_pass http://127.0.0.1:8000;
            proxy_set_header Host $server_name;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Referer $http_referer;
            proxy_set_header Origin $scheme://$host;
        }
    }


