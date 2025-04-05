I have tried crowdsec [crowdsec](https://github.com/crowdsecurity/crowdsec) . It is tough as ubuntu repos not maintaining Lua modules anymore, you have to add it manually.  

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
