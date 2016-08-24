FROM alpine:latest

RUN set -xe && \
	apk update && \
	apk add rsync

CMD ["/bin/sh","-c","while true; do sleep 1; done"]
