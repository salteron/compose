FROM scratchy

# postgres
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update
RUN apt-get -y -q install postgresql-9.2 postgresql-client-9.2 postgresql-plperl-9.2 postgresql-contrib-9.2 skytools-modules-9.2
RUN pg_dropcluster --stop 9.2 main
RUN pg_createcluster --locale $LC_ALL --start 9.2 main
RUN echo "host all all 0.0.0.0/0 trust" > /etc/postgresql/9.2/main/pg_hba.conf
RUN echo "host all all ::1/128 trust" >> /etc/postgresql/9.2/main/pg_hba.conf
RUN echo "local all all trust" >> /etc/postgresql/9.2/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.2/main/postgresql.conf
RUN echo "ssl=false" >> /etc/postgresql/9.2/main/postgresql.conf
RUN echo "plperl.on_init = 'use utf8; use re; package utf8; require \"utf8_heavy.pl\";'" >> /etc/postgresql/9.2/main/postgresql.conf

ADD dump.sql /root/db/structure/

# project db
RUN /etc/init.d/postgresql start &&\
    while ps aux | grep "postgres: [s]tartup process" > /dev/null; do sleep 1;done &&\
    sudo -u postgres psql -c "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" &&\
    sudo -u postgres psql template1 -c "CREATE EXTENSION hstore;" &&\
    sudo -u postgres createdb -O docker docker &&\
    cat /root/db/structure/dump.sql | psql -U docker docker &&\
    /etc/init.d/postgresql stop

# entrypoint
RUN echo "exec sudo -u postgres /usr/lib/postgresql/9.2/bin/postgres --config-file=/etc/postgresql/9.2/main/postgresql.conf" >> /root/init.sh

ENTRYPOINT ["/root/init.sh"]

# run script: docker run -d -p 5432:5432 --restart=always db
# check script: psql -h localhost -U docker docker -c 'select count(*) from products'
