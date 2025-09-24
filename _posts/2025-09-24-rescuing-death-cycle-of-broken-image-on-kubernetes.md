1. check the pods of deployment

    `kubectl get pods -l app=authsvc -n namespace-svc-dev`

    you will get the list of the pods

    ```
    NAME                       READY   STATUS              RESTARTS   AGE
    authsvc-58b68667dc-bhrlc   0/1     ContainerCreating   0          68s
    authsvc-58b68667dc-gvn4m   0/1     ContainerCreating   0          65s
    authsvc-6997b54ddc-6g44c   1/1     Running             0          22h
    ```

2. get the last logs if possible

   `kubectl logs authsvc-5d54b55c9b-62tdp -n namespace-svc-dev -f`

3. If it's not possible due to in never ending `ContainerCreating` or `Terminating` state, look for the events 

   `kubectl describe pod authsvc-58b68667dc-bhrlc -n namespace-svc-dev`

    example

    ```
      node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
    Events:
      Type     Reason       Age                   From               Message
      ----     ------       ----                  ----               -------
      Normal   Scheduled    4m47s                 default-scheduler  Successfully assigned dev-app-svc/authsvc-d9b8d9cb-blqs4 to node5
      Warning  FailedMount  38s (x10 over 4m47s)  kubelet            MountVolume.SetUp failed for volume "kube-api-access-vg4zq" : failed to fetch token: pod "authsvc-d9b8d9cb-blqs4" not found
      Warning  FailedMount  29s (x2 over 2m45s)   kubelet            Unable to attach or mount volumes: unmounted volumes=[kube-api-access-vg4zq], unattached volumes=[env kube-api-access-vg4zq]: timed out waiting for the condition
    ```

4. If you need some more information, look for the pod json 

      `kubectl get pod authsvc-58b68667dc-bhrlc -n namespace-svc-dev -o json`

5. In my case, check the image that the pod deployed, you see it's different signature `58b68667dc` and `6997b54ddc`  

6. Try to delete the unwanted pod

    `kubectl get pods -n dev-app-svc | grep Terminating | awk '{print $1}' \
      | xargs -I{} kubectl delete pod {} -n namespace-svc-dev --force --grace-period=0`  

7. If it kees recreating, set the replicas to 2 only, forcing, for example.

      `kubectl scale deployment authsvc -n namespace-svc-dev --replicas=2`  

8.  It should keep creating, see the list of replicasets

    `kubectl get rs -n namespace-svc-dev | grep authsvc`

    ```
    jpailabs@node1:~$ kubectl get rs -n namespace-svc-dev | grep authsvc
    authsvc-6997b54ddc              2         2         2       29m
    authsvc-858f96c65b              0         0         0       65m
    authsvc-58b68667dc              1         1         0       21m
    jpailabs@node1:~$
    ```

9. Supposed that this guy is different and has the issue `authsvc-58b68667dc  `, set it to 0
      `kubectl scale rs authsvc-58b68667dc -n namespace-svc-dev --replicas=0`

10. Check again

    ```
    kubectl get rs -n namespace-svc-dev | grep authsvc
    kubectl get pods -l app=authsvc -n nameespace-svc-dev
    ```

11. If still creating, Rollout to previous deployment  

    ```
    kubectl rollout undo deployment authsvc -n namespace-svc-dev
    ```


12. Then delete it again

    ```
    kubectl get pods -n namespace-svc-dev | grep authsvc-d9b8d9cb | awk '{print $1}' \
    >   | xargs -I{} kubectl delete pod {} -n namespace-svc-dev --force --grace-period=0
    ```

Bonus, or just look for the previous stable ones, 

    ```
    kubectl set image deployment/authsvc authsvc=registry-pg-1.app.co.id/superapps-app/authsvc:development-479 -n namespace-svc-dev
    ```
