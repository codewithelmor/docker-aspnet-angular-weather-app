# docker-aspnet-angular-weather-app
Containerized ASP.NET Angular Weather App

## Web App

Client

* http://localhost:4200/
  
API

* http://localhost:5032/swagger/index.html

## Commands

```bash
sudo -s
docker rm -vf $(sudo docker ps -aq)
docker rm -f $(sudo docker ps -aq)
docker rmi -f $(sudo docker images -aq)
docker system prune

docker-compose build
docker network create app_network
docker images -a
docker ps -a
docker create --network=app_network --name api --hostname api -p 5032:8080 [image_id]
docker start api
docker create --network=app_network --name client --hostname client -p 4200:80 [image_id]
docker start client
```
