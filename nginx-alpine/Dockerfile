#
# Dockerfile
#

FROM alpine
MAINTAINER Yann Verry <docker@verry.org>


RUN apk add --no-cache nginx-mod-http-headers-more nginx-mod-http-geoip nginx-mod-http-echo nginx-mod-http-lua
RUN /etc/periodic/monthly/geoip
