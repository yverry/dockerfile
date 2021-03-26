all: pull build


pull:
	docker pull php:8-fpm-alpine

build:
	docker build --network yann_default -t php-alpine .
