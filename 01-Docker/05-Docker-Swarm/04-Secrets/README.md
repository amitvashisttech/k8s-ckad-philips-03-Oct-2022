```
1  echo "Welcome to Docker Secrets" | docker secret create my_secret -
    2  docker secret ls
    3  docker secret rm my_external_secret
    4  ls
    5  docker secret ls
    6  echo "My Second Secrets is Here" > my_file_secret.txt
    7  ls
    8  cat my_file_secret.txt
    9  ls
   10  vim docker-compose.yaml
   11  docker stack deploy -c docker-compose.yaml test-secrets-1
   12  docker secrets
   13  docker secret ls
   14  vim docker-compose.yaml
   15  docker stack deploy -c docker-compose.yaml test-secrets-1
   16  docker stack ls
   17  docker stack rm test-secrets-1
   18  docker stack deploy -c docker-compose.yaml test-secrets-1
   19  docker stack ls
   20  docker services ls
   21  docker service ls
   22  docker service ps test-secrets-1_web
   23  docker ps
   24  docker exec -it test-secrets-1_web.1.7dfapvxhbbn1y38gnuisqbhsz -- bash
   25  docker exec -it test-secrets-1_web.1.7dfapvxhbbn1y38gnuisqbhsz bash
   26  history
```
