#
# BUILD		docker build -t svendowideit/apt-cacher .
# RUN		docker run -d -p 3142:3142 -name apt-cacher-run apt-cacher
#
# and then you can run containers with:
# 		docker run -t -i -rm -e http_proxy http://192.168.1.2:3142/ debian bash
#
FROM		ubuntu
MAINTAINER	SvenDowideit@home.org.au


VOLUME		["/var/cache/apt-cacher-ng"]
RUN		apt-get update ; apt-get install -yq apt-cacher-ng
RUN		sed -i "s/USER=apt-cacher-ng/USER=root/g" /etc/init.d/apt-cacher-ng \
   		&& sed -i "s/GROUP=apt-cacher-ng/GROUP=root/g" /etc/init.d/apt-cacher-ng
RUN		echo 'Acquire::http { Proxy "http://127.0.0.1:3142"; };' >> /etc/apt/apt.conf.d/01proxy

EXPOSE 		3142
CMD		chmod 777 /var/cache/apt-cacher-ng ; /etc/init.d/apt-cacher-ng start ; tail -f /var/log/apt-cacher-ng/*
