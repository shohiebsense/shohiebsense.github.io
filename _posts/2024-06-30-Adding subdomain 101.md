1. Add the sub domain in your web server configuration, for example nginx
```
server {
    listen 80;
    server_name sub.example.com;

    root /var/www/sub.example.com; # Change this to the directory where your site files are located
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    # Additional configurations can go here
}
```

2. Add "A" type dns records to your dns provider, for example nginx
