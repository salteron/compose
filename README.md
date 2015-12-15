# blizko
docker compose up

OR

docker run -d -p 6379:6379 --restart=always redis
docker run -d -p 5432:5432 --restart=always --name blizko_db blizko_db
docker run -d -p 11211:11211 --restart=always memcached
docker run -d -p 9306:9306 --restart=always -v ~/rails_applications/blizko/config:/sphinx/conf:ro --link blizko_db:db sphinx

# удалить все контейнеры
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)

# how to change Docker's storage base directory
https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169

# gracefully stopping docker containers
http://www.techbar.me/stopping-docker-containers-gracefully/
