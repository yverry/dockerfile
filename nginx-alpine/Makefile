all: pull build


pull:
	docker pull alpine:latest

build:
	docker build --network yann_default --no-cache=true -t nginx-alpine .
