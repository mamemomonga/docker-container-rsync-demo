FROM debian:jessie

# 日本のミラーに変更し、rsyncを導入
RUN set -xe && \
	mv /etc/apt/sources.list /etc/apt/sources.list.orig && \
	sed -e 's/httpredir\.debian\.org/ftp.jp.debian.org/g' /etc/apt/sources.list.orig > /etc/apt/sources.list && \
	apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y rsync

# ダミーサーバ
CMD ["/bin/sh","-c","while true; do sleep 1; done"]

