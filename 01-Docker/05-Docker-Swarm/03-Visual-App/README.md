```
567  mkdir 03-Visual-App
  568  ls
  569  cd 03-Visual-App/
  570  ls
  571  vim docker-compose.yaml
  572  docker stack deploy -c docker-compose.yaml visual
  573  docker stack ls
  574  docker stack ps visual
  575  docker service ls
  576  curl ifconfig.me
  577  docker services ls
  578  docker service ls
  579  docker service scale visual_web=5
  580  docker service scale visual_web=1
  581  docker service create --replicas 1 --name hello-swarm nginx
  582  docker service scale visual_web=3
  583  docker service scale hello-swarm=3
  584  docker stack ls
  585  docker stack rm visual
  586  docker service ls
  587  docker service rm hello-swarm
```
