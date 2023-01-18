# docker-swarm-kubernets
Material para apresentação das ferramentas

## Criação de imagens com tag e push



- Buildar imagem com node 14
`docker build -t rafaeljuliano/node-express:14 ./imagens/`
<br/>

- Rodar imagem no modo detached
  [Localhost:3000](http://localhost:3000)
`docker run -d -p 3000:3000 --name express-node-14 rafaeljuliano/node-express:14`
<br/>

- Buildar imagem com node 16
`docker build -t rafaeljuliano/node-express:16 ./imagens/`
<br/>

- Rodar no modo iterativo com remove automático
[Localhost:3001](http://localhost:3001)
`docker run -p 3001:3000 --rm --name express-node-16 rafaeljuliano/node-express:16`
<br/>

- Mostrar remoção do node 16
`docker ps -a`
<br/>

- Mostrar logs do node 14
`docker logs express-node-14`
<br/>

- Parar node
`docker stop express-node-14`
<br/>

- Retomar node 14
`docker start express-node-14`
<br/>

- Copiar arquivo
`docker cp express-node-14:src/app.js ./imagens/copia`
<br/>

- Publicar as tuas tagas da imagem
[Repositório](https://hub.docker.com/repository/docker/rafaeljuliano/node-express/general)
`docker push rafaeljuliano/node-express:dev-14 && docker push rafaeljuliano/node-express:dev-16`

## Volumes

- Deixar build pronto
`docker build -t phpmessages ./volumes/`

- Rodar dois container com o mesmo volume
[Localhost:80](http://localhost:80)
[Localhost:8080](http://localhost:8080)
`docker run -d -p 80:80 --name phpmessages1 --rm -v phpvolume:/var/www/html/messages phpmessages`
`docker run -d -p 8080:80 --name phpmessages2 --rm -v phpvolume:/var/www/html/messages phpmessages`

- Ler caminho da pasta e rodar no modo bind
`readlink -f ./volumes/messages`

- Se der erro dar permissão ao usuário do docker
`sudo chown www-data: messages`
`sudo chmod u+w messages`

# Networks

- Buildar imagems antes
`docker build -t flask_api_network ./networks/flask/`
`docker build -t mysql_api_network ./networks/mysql/`

- Criar network
`docker network create flaskNetwork`

- Subir container MYSQL na network
`docker run -d -p 3306:3306 --name mysql_api_container --rm --network flaskNetwork -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql_api_network`

- Subir container flask sem network
`docker run -d -p 5000:5000 --name flask_api_container --rm flask_api_network`

- Inserir flask na network
`docker network connect flaskNetwork flask_api_container`

- CURL
```curl
curl --request GET \
  --url http://localhost:5000/

curl --request POST \
  --url http://localhost:5000/inserthost
```

## Compose

- Subir containers
`docker-compose up ./compose`
- Destruir containers

## Docker Swarm

- Criar manager e atribuir workers
`docker swarm init --advertise-addr <ip>`

- Criar serviço
`docker  service create --name nginxswarm --replicas 3 -p 80:80 nginx`

- Mostrar workers e tentar excluir container
  
- Remover serviço
`docker service ls`
`docker service rm `

- Criarm yaml
  
- Criar deploy
`docker stack deploy -c docker-compose.yaml nginx_swarm`

- Escalar serviço
`docker service scale nginx_swarm_web=3`