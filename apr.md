# Docker

docker run <imagem> - executa imagem
-it - iteration - roda com terminal
-d - detached - roda em background
-p <porta maquina>:<porta container>
--name <node do container>
--rm remove após o stop
-v <diretorio>

docker start <id | nome>
docker stop <id | nome>

docker rm <id>
-f - force - para container

docker logs <id / nome>
-f - follow

docker build <diretorio>
-t - tag - define nome e tag

docker tag <ID> <nome>:<tag> nomeia iamgem

docker system prune

docker network create <nome da rede>
-d driver

docker cp <nome container>:workdir/<path/file> <path-file>

docker run -d -p 80:80 --name phpmessages_cont --rm -v phpvolume:/var/www/html/messages phpmessages

docker run -d -p 80:80 --name phpmessages_cont --rm -v phpvolume:/var/www/html/messages:ro phpmessages
sudo chown www-data: messages

sudo chmod u+w messages
docker run -d -p 80:80 --name phpmessages_cont --rm -v \/home/rafael/workspace/curso-docker/curso_docker/2_volumes/messages:/var/www/html/messages phpmessages

docker build -t mysql_api_network .networks/mysql/
docker build -t flask_api_network .networks/flask/
docker network create flaskNetwork
docker run -d -p 3306:3306 --name mysql_api_container --rm --network flaskNetwork -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql_api_network
docker run -d -p 5000:5000 --name flask_api_container --rm --network flaskNetwork flask_api_network

docker run -d -p 5000:5000 --name flask_api_container --rm flask_api_network
docker network connect flaskNetwork flask_api_container

curl --request GET \
  --url http://localhost:5000/

curl --request POST \
  --url http://localhost:5000/inserthost


  SWARM 
  docker swarm init --advertise-adr ip
  docker  service create --name nginxswarm --replicas 3 -p 80:80 nginx
  docker stack deploy -c docker-compose.yaml nginx_swarm
  docker service scale nginx_swarm_web=3

  kubectl create deployment flask-deployment --image=rafaeljuliano/flask-hub-project
  kubectl expose deployment flask-deployment --type=LoadBalancer --port=5000
  minikube service flask-deployment
  kubectl scale deployment/flask-deployment --replicas=5
  kubectl set image deployment/flask-deployment flask-hub-project=rafaeljuliano/flask-hub-project:2
  kubectl rollout undo deployment/flask-deployment

  kubectl apply -f path
