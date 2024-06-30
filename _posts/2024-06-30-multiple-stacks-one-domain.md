1. define the upstream the stack you want to load

```config
upstream default_next_js {
    ip_hash;
    server localhost:8077;
}
```

2. define the url / path you want to make it through that stack

```config
location ~ ^/path/([^/]+)/subpath {
        add_header 'Access-Control-Allow-Origin' '*' always;
        proxy_pass http://default_next_js;
        proxy_redirect off;
        proxy_set_header Connection "";
        proxy_set_header Host $host;
        proxy_set_header Upgrade %http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $server_name;
        proxy_cache mycache;
        proxy_cache_valid any 1h;
        add_header X-Proxy-Cache $upstream_cache_status;
        proxy_connect_timeout 3600;
        proxy_read_timeout 3600;
        proxy_send_timeout 3600;
        send_timeout 3600;
    }
```

the next is assets, I recommend for asset routing to be done by the ip gateway itself rather than using nginx, but its ok if you do otherwise


sample of loading asset static in krakend

```json
 {
      "endpoint": "/_next/static/{directory}/{file}",
      "output_encoding": "no-op",
      "backend": [
        {
          "url_pattern": "_next/static/{directory}/{file}",
          "encoding": "no-op",
          "sd": "static",
          "host": [
            "40.65.169.196:8010"
          ],
          "disable_host_sanitize": false
        }
      ]
    }
```
