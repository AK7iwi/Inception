FROM	debian:bullseye

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y mariadb-server
RUN apt-get install -y mariadb-client
RUN apt-get install -y procps

COPY ./conf/50-server.cnf /etc/mysql/mariadb.conf.d/50-server.cnf

RUN mkdir -p /var/run/mysqld

RUN mkdir -p /var/lib/mysql

RUN chown mysql:mysql /var/run/mysqld/
RUN chmod --recursive 755 /var/run/mysqld/
RUN chown mysql:mysql /var/lib/mysql/
RUN chmod --recursive 755 /var/lib/mysql/

EXPOSE 3306

COPY ./tools/autoconfig.sh ./
RUN chmod 755 ./autoconfig.sh

ENTRYPOINT ["bash", "./autoconfig.sh"]
