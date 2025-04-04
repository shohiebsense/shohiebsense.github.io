I have tried crowdsec [crowdsec](https://github.com/crowdsecurity/crowdsec) . It is tough as ubuntu repos not maintaining Lua modules anymore, you have to add it manually.  

Or using LuaRocks.  

I `upgrade` from plain nginx to OpenResty.  

if you find some errors when starting the nginx. See the `status`  

```
Apr 05 17:31:13 xxx.xxx.net nginx[1674599]:         no file '/usr/lib/x86_64-linux-gnu/lua/5.1/cjson.so'
Apr 05 17:31:13 xxx.xxx.net nginx[1674599]:         no file '/usr/local/lib/lua/5.1/loadall.so'
Apr 05 17:31:13 xxx.xxx.net nginx[1674599]: stack traceback:
```

i install them according to the version then copy it.

`xxx:/etc/nginx# sudo cp /usr/local/lib/lua/5.1/cjson.so /usr/lib/x86_64-linux-gnu/lua/5.1/`



It works well with other modules like let's encrypt.  

this is sample in action.  

`sudo cscli decisions list`

```
╭───────┬──────────┬───────────────────┬───────────────────────────────────┬────────┬─────────┬───────────────────────────────────────┬────────┬────────────┬──────────╮
│   ID  │  Source  │    Scope:Value    │               Reason              │ Action │ Country │                   AS                  │ Events │ expiration │ Alert ID │
├───────┼──────────┼───────────────────┼───────────────────────────────────┼────────┼─────────┼───────────────────────────────────────┼────────┼────────────┼──────────┤
│ 61781 │ crowdsec │ Ip:172.71.148.23  │ crowdsecurity/jira_cve-2021-26086 │ ban    │ DE      │ 13335 CLOUDFLARENET                   │ 1      │ 3h57m13s   │ 12       │
│ 61780 │ crowdsec │ Ip:167.86.89.21   │ crowdsecurity/ssh-slow-bf         │ ban    │ DE      │ 51167 Contabo GmbH                    │ 11     │ 3h56m56s   │ 11       │
│ 61778 │ crowdsec │ Ip:143.198.57.211 │ crowdsecurity/ssh-slow-bf         │ ban    │ US      │ 14061 DIGITALOCEAN-ASN                │ 11     │ 3h35m18s   │ 9        │
│ 61776 │ crowdsec │ Ip:14.103.172.199 │ crowdsecurity/ssh-slow-bf         │ ban    │ CN      │ 4811 China Telecom Group              │ 11     │ 3h35m9s    │ 7        │
│ 4     │ crowdsec │ Ip:160.19.78.242  │ crowdsecurity/ssh-slow-bf         │ ban    │ VN      │ 45899 VNPT Corp                       │ 11     │ 2h47m53s   │ 4        │
│ 2     │ crowdsec │ Ip:164.52.24.188  │ crowdsecurity/http-probing        │ ban    │ JP      │ 63199 CDSC-AS1                        │ 12     │ 2h21m4s    │ 2        │
│ 1     │ crowdsec │ Ip:47.245.86.231  │ crowdsecurity/ssh-bf              │ ban    │ SG      │ 45102 Alibaba US Technology Co., Ltd. │ 7      │ 2h18m37s   │ 1        │
╰───────┴──────────┴───────────────────┴───────────────────────────────────┴────────┴─────────┴───────────────────────────────────────┴────────┴────────────┴──────────╯
```

It integrates into your existing Nginx config.  

It intercepts requests before they reach your backend.  

It checks the client IP against CrowdSec’s decisions (blocklist/allowlist).  

If the IP is banned, it returns a response (like 403 or CAPTCHA) directly — no need to proxy the request further.  

So don't worry, it doesn't add another reverse proxy.  
