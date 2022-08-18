# my_first_helm

Helm figures out what is to be run first (unless forced to). For example, when I gave namespace as 04-xx and deployment in that namespace as 01-xx , then helm still applied them in correct order. The out of “helm template” , or “helm get manifest” shows the right order as well. 
But to force helm to execute something first, or last, use the hooks defined here:https://helm.sh/docs/topics/charts_hooks/#helm 
Note that use these hooks with care. For example: If the hook with pre-install is creating a job in a namespace, and the namespace is being created by something other file…then this will fail. Because the pre-install hook will bypass helm’s logic and run first …even before namespace is created. 

```
[mano@bastion ~]$ oc get all -n helm-test-1 
NAME                              READY   STATUS    RESTARTS   AGE
pod/argotesting-79675587f-9hpgb   1/1     Running   0          14m
pod/argotesting-79675587f-f8wq2   1/1     Running   0          14m
pod/argotesting-79675587f-rvvgc   1/1     Running   0          14m
pod/argotesting-79675587f-vtt6b   1/1     Running   0          14m

NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
service/argo-test-service   ClusterIP   172.30.66.164   <none>        80/TCP    14m

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/argotesting   4/4     4            4           14m

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/argotesting-79675587f   4         4         4       14m
[mano@bastion ~]$ 
```
