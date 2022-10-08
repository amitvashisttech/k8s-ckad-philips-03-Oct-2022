```
 139  mkdir 20-ConfigMap
  140  ls
  141  kubectl  get pods
  142  kubectl  delete deploy --all
  143  ls
  144  kubectl  run hello-nginx --image=nginx:1.11 --port=80
  145  kubectl  get pods
  146  kubectl  expose pod hello-nginx --type=NodePort
  147  kubectl  get pods
  148  kubectl  get svc
  149  kubectl  delete svc python-webapp-svc
  150  ls
  151  kubectl  get svc
  152  curl 172.16.16.101:30548
  153  ls
  154  cd 20-ConfigMap/
  155  ls
  156  vim proxy.conf
  157  kubectl create configmap --help
  158  kubectl create configmap nginx-config --from-file=proxy.conf
  159  kubectl  get configmap
  160  kubectl  get secrets
  161  kubectl  describe secrets
  162  kubectl  apply -f ../13-Secrets/02-helloworld-secrets.yaml
  163  kubectl  get secrets
  164  kubectl  describe secrets my-db-secrets
  165  kubectl  edit secrets my-db-secrets
  166  kubectl  get configmap
  167  kubectl  describe configmap nginx-config
  168  ls
  169  kubectl create configmap nginx-config --from-file=proxy.conf  --dry-run -o yaml > 01-ConfigMap-Nginx.yaml
  170  ls
  171  cat 01-ConfigMap-Nginx.yaml
  172  vim 02-Nginx-Pod-Deploy.yaml
  173  kubectl  apply -f 02-Nginx-Pod-Deploy.yaml
  174  kubectl get pods
  175  kubectl get pods -w
  176  kubectl get pods
  177  kubectl get pods -o wide
  178  kubectl  get svc
  179  kubectl  expose pod helloworld-nginx --type=NodePort
  180  kubectl  get svc
  181  ls
  182  kubectl  get pods
  183  kubectl  exec -it helloworld-nginx -c nginx -- bash
  184  kubectl  exec -it helloworld-nginx  -- bash
  185  kubectl  exec -it helloworld-nginx  -- sh
  186  kubectl  get pods -o wide
  187  vim /etc/hosts
  188  kubectl  exec -it helloworld-nginx  -- bash
  189  ls
  190  cd ..
  191  ls
  192  cd ..
  193  ls
  200  ls
  201  cd k8s-ckad-philips-03-Oct-2022/
  202  ls
  203  cd 02-K8s/
  204  ls
  205  cd 20-ConfigMap/
  206  ls
  207  mkdir exp2
  208  ls
  209  mv proxy.conf exp2/
  210  ls
  211  cp -rf ../10-Services/03-app-svc-deployment.yaml .
  212  ls
  213  mv 03-app-svc-deployment.yaml exp2/
  214  ls
  215  s
  216  ls
  217  cd exp2/
  218  ls
  219  vim proxy.conf
  220  ls
  221  vim 03-app-svc-deployment.yaml
  222  ls
  223  kubectl create configmap nginx-config-py --from-file=proxy.conf  --dry-run -o yaml > 01-ConfigMap-Nginx-py.yaml
  224  kubectl  apply -f 01-ConfigMap-Nginx-py.yaml
  225  kubectl  get configmap
  226  kubectl  describe configmap nginx-config-py
  227  s
  228  ls
  229  kubectl apply -f 01-ConfigMap-Nginx-py.yaml
  230  kubectl apply -f 03-app-svc-deployment.yaml
  231  kubectl  get pods
  232  kubectl  get svc
  233  curl http://172.16.16.101:31007/info
  234  kubectl  get pods
  235  kubectl  exec -it python-webapp-deployment-77cdd99896-6vqt8 -- bash
  236  kubectl  get pods
  237  kubectl  exec -it python-webapp-deployment-77cdd99896-6vqt8 -- cat /etc/nginx/conf.d/reverseproxy.conf
  238  kubectl  exec -it python-webapp-deployment-77cdd99896-jlwsf -- cat /etc/nginx/conf.d/reverseproxy.conf
  239  kubectl  exec -it python-webapp-deployment-77cdd99896-q4llr -- cat /etc/nginx/conf.d/reverseproxy.conf
  240  ls
  241  cd ..
  242  ls
  243  cd exp2/ls
  244  cd exp2/
  245  ls
  246  mv 03-app-svc-deployment.yaml 02-app-svc-deployment.yaml
  247  ls
  248  cd ..
  249  ls
  250  cd ..
  251  ls
  252  git add . ; git commit -m "20-ConfigMap" ; git push
  253  ls
  254  kubectl  delete -f 20-ConfigMap/

```
