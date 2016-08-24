FROM debian:jessie

RUN set -xe && \
	apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y rsync

CMD ["/bin/sh","-c","while true; do sleep 1; done"]

