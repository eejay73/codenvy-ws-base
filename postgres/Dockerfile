FROM eclipse/stack-base:ubuntu

USER root
RUN set -ex; \
    key='B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8'; \
    export GNUPGHOME="$(mktemp -d)"; \
    sudo gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    sudo gpg --export "$key" > /etc/apt/trusted.gpg.d/postgres.gpg; \
    rm -r "$GNUPGHOME"; \
    sudo apt-key list
ENV PG_MAJOR 9.6
ENV PG_VERSION 9.6.2-1.pgdg80+1
RUN sudo echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' $PG_MAJOR > /etc/apt/sources.list.d/pgdg.list
USER user
RUN sudo apt-get update \
    && sudo apt-get install -y postgresql-common \
    && sudo sed -ri 's/#(create_main_cluster) .*$/\1 = false/' /etc/postgresql-common/createcluster.conf \
    && sudo apt-get install -y \
	postgresql-$PG_MAJOR=$PG_VERSION \
	postgresql-contrib-$PG_MAJOR=$PG_VERSION \
    && sudo rm -rf /var/lib/apt/lists/*
RUN sudo mv -v /usr/share/postgresql/$PG_MAJOR/postgresql.conf.sample /usr/share/postgresql/ \
    && sudo ln -sv ../postgresql.conf.sample /usr/share/postgresql/$PG_MAJOR/ \
    && sudo sed -ri "s!^#?(listen_addresses)\s*=\s*\S+.*!\1 = '*'!" /usr/share/postgresql/postgresql.conf.sample
RUN sudo mkdir -p /var/run/postgresql && sudo chown -R postgres:postgres /var/run/postgresql && sudo chmod g+s /var/run/postgresql
ENV PATH /usr/lib/postgresql/$PG_MAJOR/bin:$PATH
ENV PGDATA /var/lib/postgresql/data
RUN sudo mkdir -p "$PGDATA" && sudo chown -R postgres:postgres "$PGDATA" && sudo chmod 777 "$PGDATA"
VOLUME /var/lib/postgresql/data
CMD sudo pg_createcluster 9.6 main --start && sudo service postgresql start & tail -f /dev/null
