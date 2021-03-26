all: pull build


pull:
	docker pull alpine:latest

build:
	docker build --no-cache=true -t pgbouncer-alpine .
