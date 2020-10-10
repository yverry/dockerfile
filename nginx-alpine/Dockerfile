#
# Dockerfile
#

FROM alpine:edge
MAINTAINER Yann Verry <docker@verry.org>


RUN apk add --no-cache nginx-mod-http-headers-more nginx-mod-http-echo nginx-mod-http-lua nginx-mod-http-geoip2 nginx-mod-http-brotli  && \
	mkdir /var/www/html && \
	touch /var/www/html/index.html

# GeoIP
RUN apk add --no-cache wget && \
	mkdir /usr/share/geoip && \
	wget -O GeoLite2-City.tar.gz 'https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-City&license_key=${MMDB_APIKEY}&suffix=tar.gz' && \
	wget -O GeoLite2-Country.tar.gz 'https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-Country&license_key=${MMDB_APIKEY}&suffix=tar.gz' && \
	wget -O GeoLite2-ASN.tar.gz 'https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-ASN&license_key=${MMDB_APIKEY}&suffix=tar.gz' && \
	tar xf GeoLite2-City.tar.gz && \
	tar xf GeoLite2-Country.tar.gz && \
	tar xf GeoLite2-ASN.tar.gz && \
	mv GeoLite2-City*/GeoLite2-City.mmdb /usr/share/geoip/ && \
	mv GeoLite2-Country*/GeoLite2-Country.mmdb /usr/share/geoip/ && \
	mv GeoLite2-ASN*/GeoLite2-ASN.mmdb /usr/share/geoip/ && \
	rm -rf Geo*

EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
