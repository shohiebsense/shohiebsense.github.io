I have installed OpenResty, it makes the cpanel (whm) didn't detect the Nginx from Nginx Manager.  

Thankfully it goes smoothly, it can mingle with OpenResty.  

So just install again via Cpanel (Nginx Manager), then look for the error.log again if it happens in errror.log

`cat /var/log/nginx/error.log`  

usually about permissions.

```
chown -R www-data:www-data /var/cache/ea-nginx/proxy
chmod -R 700 /var/cache/ea-nginx/proxy
sudo chown -R www-data:www-data /var/cache/nginx
chown -R nobody:nobody /var/cache/ea-nginx/proxy
chmod -R 700 /var/cache/ea-nginx/proxy
sudo chmod -R 700 /var/cache/nginx
```

