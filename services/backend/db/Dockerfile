FROM postgres:13-alpine as dumper

COPY restore/restore.sql /docker-entrypoint-initdb.d/

RUN ["sed", "-i", "s/exec \"$@\"/echo \"skipping...\"/", "/usr/local/bin/docker-entrypoint.sh"]

ENV POSTGRES_USER=postgres
ENV POSTGRES_PASSWORD=postgres
ENV PGDATA=/data

RUN ["/usr/local/bin/docker-entrypoint.sh", "postgres"]

FROM postgres:13-alpine
COPY --from=dumper /data $PGDATA

# credits
# https://cadu.dev/creating-a-docker-image-with-database-preloaded/
