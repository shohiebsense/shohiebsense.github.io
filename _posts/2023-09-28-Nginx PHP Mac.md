Just Affirming that this works:  

https://kevdees.com/install-nginx-multiple-php-versions-on-macos-13-ventura/  

Just make sure that the php-fpm config `usr/local/etc/php/7.3/php-fpm.d/www.conf`  

the listen port  

`listen = 127.0.0.1:9000` as same as  

in `usr/local/etc/nginx`  

```
  location ~ \.php$ {
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           include        fastcgi_params;
           fastcgi_pass   127.0.0.1:9000;
           fastcgi_index index.php;
           fastcgi_split_path_info ^(.+\.php)(/.+)$;
        }
```  
