# docker-aspnet-angular-weather-app
Containerized ASP.NET Angular Weather App

![2023-11-26 00-37-46](https://github.com/codewithelmor/docker-aspnet-angular-weather-app/assets/44918452/8f73f4e9-3108-47ef-835a-63ab5395f556)

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
