# EFK
**EFK on kubernetes**

由于fluentd-daemonset.yaml使用了nodeSelector，所以需要为使用fluentd收集日志的节点需要添加label.
```
# kubectl label nodes nodename beta.kubernetes.io/fluentd-ds-ready=true
```
---
```
# kubectl get node --show-labels  
NAME   STATUS   ROLES    AGE   VERSION   LABELS
k8s1   Ready    master   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true**,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s1,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s2   Ready    master   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s2,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s3   Ready    master   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s3,kubernetes.io/os=linux,node-role.kubernetes.io/master=
k8s4   Ready    <none>   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s4,kubernetes.io/os=linux
k8s5   Ready    <none>   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s5,kubernetes.io/os=linux
k8s6   Ready    <none>   24h   v1.14.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/fluentd-ds-ready=true,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=k8s6,kubernetes.io/os=linux
```
---
```
# kubectl get pod -n logging  
NAME                     READY   STATUS    RESTARTS   AGE
es-cluster-0             1/1     Running   0          23h
es-cluster-1             1/1     Running   0          23h
es-cluster-2             1/1     Running   0          23h
fluentd-es-7nsmc         1/1     Running   0          23h
fluentd-es-9tcfz         1/1     Running   0          23h
fluentd-es-b5252         1/1     Running   0          23h
fluentd-es-q9f44         1/1     Running   0          23h
fluentd-es-v89xc         1/1     Running   0          23h
fluentd-es-wlf2q         1/1     Running   0          23h
kibana-bd6f49775-52xs9   1/1     Running   0          23h
```
---
```
# kubectl get svc -n logging  
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
elasticsearch   ClusterIP   None            <none>        9200/TCP,9300/TCP   23h
kibana          NodePort    10.110.82.151   <none>        5601:30524/TCP      23h
```
