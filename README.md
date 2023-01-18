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
```