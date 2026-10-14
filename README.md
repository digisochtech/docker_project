# Docker Project with MySQL and Grafana docker-images to setup monitoring dashboard
---

## Pre-requisite
Docker installed in your system.

## Steps

There are two methods to run mysql and garfana and connect togather:
### 1. Using docker command
Open command prompt/Terminal and run the following commands to setup mysql and grafana docker images.


- List availabe docker images
  
```bash
docker images
```
-pull mysql and grafana docker images

```bash
docker pull mysql:8.0
docker pull grafana/grafana:latest
```
-Create a network to connect mysql and grafana containers

```bash
docker network create mysql-grafana-network
```
- Run mysql container

```bash
docker run -d --name demo_mysql --network mysql-grafana-network -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=grafana_demo -e MYSQL_USER=grafana_user -e MYSQL_PASSWORD=grafana123 mysql:8.0
```

- Run grafana container

```bash
docker run -d --name demo_grafana --network mysql-grafana-network -p 3000:3000 -e GF_SECURITY_ADMIN_USER=admin -e GF_SECURITY_ADMIN_PASSWORD=admin grafana/grafana:latest
```
- Now you can access grafana dashboard in your browser using the following URL: http://localhost:3000
- Try to login with username: admin and password: admin
- To test mysql connection, you can use the following command to connect to mysql container:

```bash
docker exec -it demo_mysql mysql -u grafana_user -p
```


### 2. Using Docker compose file
