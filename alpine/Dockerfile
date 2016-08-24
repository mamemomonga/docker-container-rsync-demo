FROM alpine:latest

RUN set -xe && \
	apk update && \
	apk add rsync

# ダミーサーバ
CMD ["/bin/sh","-c","while true; do sleep 1; done"]

