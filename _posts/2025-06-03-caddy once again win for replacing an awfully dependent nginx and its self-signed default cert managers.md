Literally,

In this case, the server operates in clustering system so no need to care the nameserver anymore, do this.  


```Caddyfile
:80, :443 {
    reverse_proxy 192.168.150.99:32412
}
```

that is ip addr of own machine that belongs to one of the nodes. And we involve the Kubernetes NodePort for this.  

Here we go, I don't need to care about ssl renewal anymore, whether the cert is third party using let's encrypt, not self signed.  

With just those 3 beautiful lines. Look at that, so sexy isn't it?
