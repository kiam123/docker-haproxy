docker network create --subnet=172.18.0.0/24 test-network

cd base
docker build -t server_base .
cd ..
cd haproxy
docker build -t haproxy_base .
cd ..
cd web
docker build -t nginx_web .
cd ..

docker run -d \
    -p 8880:80 -p 8022:22 -p 9000:9000 \
    --name haproxy \
    --privileged \
    --net test-network \
    haproxy_base

docker run -d \
    -p 8881:80 -p 8023:22 \
    --privileged \
    --name web1 \
    --net test-network \
    -e "name=WEB1" \
    nginx_web

docker run -d \
    -p 8882:80 -p 8024:22 \
    --privileged \
    --name web2 \
    --net test-network \
    -e "name=WEB2" \
    nginx_web




## DB with WordPress
docker run --name mariadb \
    -v /home/selab-server/docker/mariadb-test/datadir:/var/lib/mysql \
    -p 13306:3306 \
    -e MYSQL_ROOT_PASSWORD=test \
    --net test-network \
    -d mariadb


docker run --name wordpress -p 8888:80 \
    -e WORDPRESS_DB_HOST=172.18.0.2:3306 \
    -e WORDPRESS_DB_USER=root \
    -e WORDPRESS_DB_PASSWORD=test \
    -e WORDPRESS_DB_NAME=wordpress \
    --net test-network \
    -d wordpress

docker rm -f mariadb wordpress && sudo rm -rf ~/docker/mariadb-test/datadir/*

