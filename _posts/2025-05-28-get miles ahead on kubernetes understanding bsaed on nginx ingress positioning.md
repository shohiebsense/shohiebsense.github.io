[![Watch the video](https://img.youtube.com/vi/RQbc_Yjb9ls/hqdefault.jpg)](https://youtu.be/RQbc_Yjb9ls)  

you can, but also it will eventually let the kubernetes exposed the node port, to make it accessible from the public, but as you know it will use around 30000 ports.  

Just mind you every approach/positioning will have the pros and cons.

After you can understand the difference in behaviour between them.  

You can read to solidify your understanding here.  

[https://kubernetes.github.io/ingress-nginx/deploy/baremetal/#over-a-nodeport-service](https://kubernetes.github.io/ingress-nginx/deploy/baremetal/#over-a-nodeport-service)  

so that you can achieve what you want

```bash
shohiebsense@k8s-master:~/kube-configs$ sudo ss -tlnp | grep -E ':(80|443) '
LISTEN 0      4096          0.0.0.0:80         0.0.0.0:*    users:(("nginx",pid=520240,fd=15),("nginx",pid=520234,fd=15))                           
LISTEN 0      4096          0.0.0.0:80         0.0.0.0:*    users:(("nginx",pid=520239,fd=7),("nginx",pid=520234,fd=7))                             
LISTEN 0      4096          0.0.0.0:443        0.0.0.0:*    users:(("nginx",pid=520240,fd=17),("nginx",pid=520234,fd=17))                           
LISTEN 0      4096          0.0.0.0:443        0.0.0.0:*    users:(("nginx",pid=520239,fd=9),("nginx",pid=520234,fd=9))                             
LISTEN 0      4096             [::]:80            [::]:*    users:(("nginx",pid=520239,fd=8),("nginx",pid=520234,fd=8))                             
LISTEN 0      4096             [::]:80            [::]:*    users:(("nginx",pid=520240,fd=16),("nginx",pid=520234,fd=16))                           
LISTEN 0      4096             [::]:443           [::]:*    users:(("nginx",pid=520239,fd=10),("nginx",pid=520234,fd=10))                           
LISTEN 0      4096             [::]:443           [::]:*    users:(("nginx",pid=520240,fd=18),("nginx",pid=520234,fd=18))                           
```

