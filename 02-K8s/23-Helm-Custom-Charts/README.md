```
412  wget https://get.helm.sh/helm-v3.4.2-linux-amd64.tar.gz
  413  tar -zxvf helm-v3.4.2-linux-amd64.tar.gz
  414  sudo mv linux-amd64/helm /usr/local/bin/helm
  415  helm list
  416  helm search repo nginx
  417  helm repo add azure-marketplace https://marketplace.azurecr.io/helm/v1/repo
  418  helm search repo nginx
  419  helm install first-nginx azure-marketplace/nginx-test
  420  helm list
  421  kubectl get pods
  422  ls
  423  cd k8s-ckad-philips-03-Oct-2022/
  424  ls
  425  cd 02-K8s/
  426  ls
  427  cd 22-Helm/
  428  ls
  429  vim helm-rbac.yaml
  430  kubectl  apply -f helm-rbac.yaml
  431  helm list
  432  kubectl  get pods
  433  kubectl  get deploy
  434  kubectl  get svc
  435  curl 172.16.16.101:30642
  436  helm install second-nginx azure-marketplace/nginx-test
  437* helm install third-nginx azure-marketplace/nginx-ttes
  438  kubectl get deploy,pod,svc
  439  cat /root/.kube/config
  440  ls
  441  cd ..
  442  ls
  443  git add . ; git commit -m "22-Helm" ; git push
  444* helm
  445  helm install second-nginx-2 azure-marketplace/nginx-test --debug
  446  helm install second-nginx-2 azure-marketplace/nginx-test
  447  helm list
  448  helm uninstall second-nginx-2
  449  helm --help
  450  helm install second-nginx-2
  451  helm install second-nginx-2 azure-marketplace/nginx-test
  452  helm install second-nginx-3 azure-marketplace/nginx-test --debug
  453  ls
  454  mkdir 23-Helm-Custom-Charts
  455  cd 23-Helm-Custom-Charts/
  456  ls
  457  helm create my-tiny-web
  458  ls
  459  cd my-tiny-web/
  460  ls
  461  cat Chart.yaml
  462  ls
  463  cat values.yaml
  464  ls
  465  cd templates/
  466  ls
  467  vim service.yaml
  468  ls
  469  cat deployment.yaml
  470  ls
  471  cd .
  472  cd ..
  473  ls
  474  vim values.yaml
  475  ls
  476  cd ..
  477  ls
  478  helm install mywebapp my-tiny-web --dry-run
  479  helm install mywebapp my-tiny-web
  480  helm list
  481  kubectl  get pods
  482  ls
  483  cd ..
  484  ls
  485  cd 23-Helm-Custom-Charts/
  486  ls
  487  helm create my-py-webapp
  488  ls
  489  cd my-py-webapp/
  490  ls
  491  vim values.yaml
  492  ls
  493  vim templates/deployment.yaml
  494  ls
  495  vim values.yaml
  496  ls
  497  cd ..
  498  ls
  499  helm install web-app-py my-py-webapp --dry-run
  500  helm install web-app-py my-py-webapp
  501  kubectl  get pods

```
