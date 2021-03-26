#
# Dockerfile
#

FROM alpine:latest
MAINTAINER Yann Verry <docker@verry.org>


RUN apk add --no-cache pgbouncer

USER nobody

CMD /usr/bin/pgbouncer /etc/pgbouncer/pgbouncer.ini
