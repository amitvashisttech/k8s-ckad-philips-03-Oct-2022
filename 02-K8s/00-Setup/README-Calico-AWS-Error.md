# Delete the existing Calico Deployment

```
kubectl delete -f calico.yaml
```


# Apply the Tigera Calio
```
kubectl create -f https://projectcalico.docs.tigera.io/manifests/tigera-operator.yaml
kubectl create -f https://projectcalico.docs.tigera.io/manifests/custom-resources.yaml
```
