FROM mysql:8.0-debian
EXPOSE 3306
ARG MANGOS_DATABASE_VERSION=master

ENV MANGOS_DATABASE_REALM_NAME=MyAwesomeWowServer
ENV MANGOS_SERVER_VERSION=3
ENV MANGOS_DB_RELEASE=Rel21
ENV MYSQL_USER=mangos
ENV MYSQL_PASSWORD=mangos

ADD launch_mysql.sh .

RUN apt update && \
    apt install git -y
RUN git clone https://github.com/mangosthree/database.git -b ${MANGOS_DATABASE_VERSION} --recursive
RUN chmod a+x launch_mysql.sh
RUN apt-get remove --purge --force-yes -y git wget && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["./launch_mysql.sh"]
CMD ["mysqld"]