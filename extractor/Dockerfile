FROM debian:12
EXPOSE 3724
ENV LOGIN_DATABASE_INFO=127.0.0.1;3306;root;mangos;realmd
WORKDIR /etc/mangos/
COPY --from=mangosthree/builder /tools/ ./tools/
RUN cp ./tools/*-extractor ~/etc/mangos/cata_client  \
    cp ./tools/*.sh ~/etc/mangos/cata_client         \
    cp ./tools/offmesh.txt ~/etc/mangos/cata_client  \
    cd ~/etc/mangos/cata_client                      \
    chmod -R a+w ~/mangos/zero/gamedata              \
    chmod a+x ExtractResources.sh                    \
    sh ExtractResources.sh -a                        \
    