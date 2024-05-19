FROM debian:12
EXPOSE 8085
ENV LOGIN_DATABASE_INFO=127.0.0.1;3306;root;mangos;realmd
ENV WORLD_DATABASE_INFO=127.0.0.1;3306;root;mangos;mangos1
ENV CHARACTER_DATABASE_INFO=127.0.0.1;3306;root;mangos;character1
WORKDIR /etc/mangos/
COPY --from=mangosthree/builder /server/bin .
RUN apt-get update && \
    apt-get install wget libstdc++6 libmariadbclient-dev libmariadbd19 libmariadb3 libssl-dev -y && \
    ln -s /usr/lib/x86_64-linux-gnu/libmariadbclient.so /usr/lib/x86_64-linux-gnu/libmariadbclient.so.18 && \
    useradd -ms /bin/bash mangos && \
    chmod -R a+x . && \
    mv conf/mangosd.conf.dist conf/mangosd.conf && \
    sed -i 's/^LoginDatabaseInfo            =.*$/LoginDatabaseInfo            = LOGIN_DATABASE_INFO/' conf/mangosd.conf && \
    sed -i 's/^WorldDatabaseInfo            =.*$/WorldDatabaseInfo            = WORLD_DATABASE_INFO/' conf/mangosd.conf && \
    sed -i 's/^CharacterDatabaseInfo        =.*$/CharacterDatabaseInfo        = CHARACTER_DATABASE_INFO/' conf/mangosd.conf && \
    chown -R mangos:mangos . && \
    rm -rf /var/lib/apt/lists/*
USER mangos
CMD ["./launch_mangosd.sh"]