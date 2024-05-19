FROM debian:12
EXPOSE 3724
ENV LOGIN_DATABASE_INFO=127.0.0.1;3306;root;mangos;realmd
WORKDIR /etc/mangos/
COPY --from=mangosthree/builder /server/bin/ .

ADD launch_realmd.sh .

RUN apt-get update && \
    apt-get install wget libmariadbclient-dev libmariadbd19 libmariadb3 libssl-dev -y
RUN ln -s /usr/lib/x86_64-linux-gnu/libmariadbclient.so /usr/lib/x86_64-linux-gnu/libmariadbclient.so.18
RUN useradd -ms /bin/bash realm && \
    chmod -R a+x . && \
    mv conf/realmd.conf.dist conf/realmd.conf
RUN sed -i 's/^LoginDatabaseInfo      =.*$/LoginDatabaseInfo      = LOGIN_DATABASE_INFO/' conf/realmd.conf && \
    chown -R realm:realm .
RUN rm -rf /var/lib/apt/lists/*
USER realm
CMD ["./launch_realmd.sh"]