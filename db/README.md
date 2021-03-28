docker run --name mariadb \
    -v /home/selab-server/docker/mariadb-test/datadir:/var/lib/mysql \
    -p 13306:3306 \
    -e MYSQL_ROOT_PASSWORD=test \
    -d mariadb