FROM pg92

ADD blizko.sql /root/db/structure/
RUN /etc/init.d/postgresql start &&\
    cat /root/db/structure/blizko.sql | psql -U docker docker &&\
    /etc/init.d/postgresql stop

# run script: docker run -d -p 5432:5432 --restart=always blizko_db
# check script: psql -h localhost -U docker docker -c 'select count(*) from products'