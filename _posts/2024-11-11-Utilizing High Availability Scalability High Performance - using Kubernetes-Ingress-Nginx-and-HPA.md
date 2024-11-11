the steps:

```bash
#i use docker desktop that acts as a cluster: to act as a handler for public domain of the app)
load balancer (cluster) -> ingress <-> hpa <-> the application in pods
# hpa: horizontal pod autoscaling
```

1. Install the app you want to scale
2. Make the Dockerfile
3. Build it, for example:  
`docker build -t shohiebsense/network-traffic-monitor-8085:latest .`
4. Push it to harbor/registry or whatever, you can build private harbor/registry tho but i use docker hub https://hub.docker.com/  
`docker push shohiebsense/network-traffic-monitor-8085:latest`
5. Install the metrics, tools to monitor the hpa.  
`kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`
6. Check if metrics installed  
`kubectl get deployment metrics-server -n kube-system`  
6a. log if it's running  
`kubectl logs -n kube-system deployment/metrics-server`
8. Apply the deployment, load_balancer, and ingress (`.yaml` file).
`kubectl apply -f deployment.yaml`  
`kubectl apply -f ingress.yaml`
`kubectl apply -f load_balancer.yaml`  
9. You can use bash script or yaml file to do autoscaling
`kubectl autoscale deployment network-traffic-monitor-deployment-8085 --cpu-percent=3 --min=2 --max=5`
10. using `.yaml`  
```.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: network-traffic-monitor-hpa-8085
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: network-traffic-monitor-deployment-8085
  minReplicas: 2
  maxReplicas: 7
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 3  # Lower the CPU target to 3%, it's small i know, to see the scaling by generating new pods in action
```
10. Test your app, I use locust
11. Monitor your pods, can use `watch` or `k9s`
```
watch kubectl get pods -o wide
```
12. [https://k9scli.io/](https://k9scli.io/)  


Repo:  
[https://github.com/shohiebsense/kubernetes_8085-autoscaler-hpa-ingress-nginx](https://github.com/shohiebsense/kubernetes_8085-autoscaler-hpa-ingress-nginx)


