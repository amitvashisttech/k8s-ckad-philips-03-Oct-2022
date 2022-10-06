```
  853  systemctl status kubelet
  854  cat /var/lib/kubelet/config.yaml
  855  grep -i "staticPodPath"  /var/lib/kubelet/config.yaml
  856  cat /etc/kubernetes/manifests/myapp.yaml
```

```
NAME                READY   STATUS    RESTARTS   AGE     IP                NODE      NOMINATED NODE   READINESS GATES
busybox-2-worker2   1/1     Running   1          7m43s   192.168.189.118   worker2   <none>           <none>
myapp-master        1/1     Running   0          3m38s   192.168.219.72    master    <none>           <none>
myapp-worker1       1/1     Running   0          5m57s   192.168.235.155   worker1   <none>           <none>
myapp-worker2       1/1     Running   0          6m59s   192.168.189.114   worker2   <none>           <none>
```
