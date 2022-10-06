```
130  cd 12-Affinity/
  131  ls
  132  vim 01-helloworld.yaml
  133  kubectl  apply -f 01-helloworld.yaml
  134  cat 01-helloworld.yaml
  135  kubectl  label node worker1 env=prod
  136  kubectl  delete -f 01-helloworld.yaml
  137  cp -rf 01-helloworld.yaml 02-hellowrld-multi-dev-prod.yaml
  138  vim 02-hellowrld-multi-dev-prod.yaml
  139  kubectl  label node worker1 env-
  140  kubectl  apply -f 02-hellowrld-multi-dev-prod.yaml
  141  kubectl  label node worker1 env=dev
  142  kubectl  label node worker2 env=prod
  143  kubectl  get nodes --show-labels
  144  kubectl  scale --replicas=5 -f 02-hellowrld-multi-dev-prod.yaml
  145  kubectl  delete -f 02-hellowrld-multi-dev-prod.yaml
  146  ls
  147*
  148  kubectl  label node worker2 env=dev
  149  kubectl  label node worker2 env=dev --overwrite
  150  kubectl  get nodes --show-labels
  151  s
  152  ls
  153  cp -rf 02-hellowrld-multi-dev-prod.yaml 03-hellowrld-dev.yaml
  154  ls
  155  vim 03-hellowrld-dev.yaml
  156  kubectl  apply -f 03-hellowrld-dev.yaml
  157  kubectl  delete -f 03-hellowrld-dev.yaml
  158  ls
  159  cp -rf 03-hellowrld-dev.yaml 04-hellowrld-dev-preff.yaml
  160  ls
  161  vim 04-hellowrld-dev-preff.yaml
  162  kubectl  apply -f 04-hellowrld-dev-preff.yaml --dry-run
  163  vim 04-hellowrld-dev-preff.yaml
  164  kubectl  apply -f 04-hellowrld-dev-preff.yaml --dry-run
  165  kubectl  label node worker2 team=devops
  166  kubectl  get nodes --show-labels
  167  kubectl  apply -f 04-hellowrld-dev-preff.yaml
  168  kubectl  scale --replicas=10 -f 04-hellowrld-dev-preff.yaml
```
