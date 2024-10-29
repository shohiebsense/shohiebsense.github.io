```
server {
    listen      80 default_server;
    listen      [::]:80 default_server;
    server_name _;
    return      444;
}

server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;
    server_name _;
    
    ssl_certificate /etc/xxx/livefullchain.pem; 
    ssl_certificate_key /etc/xxx/privkey.pem;

    return 444;
}
```
