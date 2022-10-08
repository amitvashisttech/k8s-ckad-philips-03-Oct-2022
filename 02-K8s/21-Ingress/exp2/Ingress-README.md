```
 kubectl create ingress catch-all --class=otheringress --rule="/backend=backend-app-v1:80"  --rule="/info=python-webapp-svc:31007" --rule="/frontend=frontend-app-v1:80"```
