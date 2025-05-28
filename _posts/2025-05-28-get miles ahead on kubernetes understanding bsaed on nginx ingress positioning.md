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



shohiebsense@k8s-master:~/kube-configs$ kubectl get pods --all-namespaces -l app.kubernetes.io/name=ingress-nginx
NAMESPACE       NAME                                                     READY   STATUS    RESTARTS   AGE
ingress-nginx   nginx-ingress-ingress-nginx-controller-f5b78bf4c-7xhbg   1/1     Running   0          16h
shohiebsense@k8s-master:~/kube-configs$ kubectl get svc -n ingress-nginx
NAME                                               TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                      AGE
nginx-ingress-ingress-nginx-controller             LoadBalancer   10.108.242.29   x.x.x.x   80:30080/TCP,443:30443/TCP   44h
nginx-ingress-ingress-nginx-controller-admission   ClusterIP      10.103.107.28   <none>           443/TCP                      44h
shohiebsense@k8s-master:~/kube-configs$ kubectl get svc
NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
cm-acme-http-solver-964fn   NodePort    10.103.150.114   <none>        8089:32605/TCP   17h
kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP          2d6h
my-web-app-service          ClusterIP   10.105.126.204   <none>        80/TCP           43h
test-nginx-nodeport         NodePort    10.110.42.164    <none>        80:30366/TCP     46h
web-server-service          ClusterIP   10.107.232.187   <none>        80/TCP           16h
shohiebsense@k8s-master:~/kube-configs$ kubectl get deploy -A | grep test-nginx
default          test-nginx                               1/1     1            1           46h
shohiebsense@k8s-master:~/kube-configs$ kubectl scale deployment test-nginx --replicas=0 
deployment.apps/test-nginx scaled
shohiebsense@k8s-master:~/kube-configs$


```

