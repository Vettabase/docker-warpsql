# WarpSQL
# WarpSQL is a MySQL fork by Justin Swanhart.
# https://github.com/greenlion/warp

# Build and create a container:
# docker build --no-cache --tag vettadock/warpsql:8.0-1.0 .
# docker rm -f warp1
# docker run --detach --name warp1 vettadock/warpsql:8.0-1.0
# docker start warp1
#
# Connect to WarpSQL:
# docker exec -ti warp1 mysql


ARG ubuntu_version=20.04
FROM ubuntu:$ubuntu_version

ARG tarball=https://github.com/greenlion/warp/releases/download/v8.0.21-1.0.2-beta/mysql-8.0.21-1.0.2-beta.tar.gz

RUN  \
    groupadd mysql \
    && useradd -r -g mysql -s /bin/false mysql

ADD $tarball /usr/local/warpsql.tar.gz
WORKDIR /usr/local

ADD ./my.cnf /etc/mysql/

RUN \
    apt-get update \
    && apt-get install -y \
        libssl1.1 \
    && TARBALL=$(ls -t1 | head -1) \
    && tar zxovf $TARBALL \
    && DIRNAME=$( tar --list -f $TARBALL | head -1 ) \
    && rm $TARBALL \
    && mv $DIRNAME mysql \
    && echo "/usr/local/mysql/lib/plugin" > /etc/ld.so.conf.d/warp.conf \
    && ldconfig
RUN cd /usr/local/mysql \
    && /usr/local/mysql/bin/mysqld --initialize-insecure

EXPOSE 3306
ENV PATH="/usr/local/mysql/bin:${PATH}"
CMD ["mysqld"]
USER root:root

# metadata
LABEL \
    com.vettabase.vendor="Vettabase" \
    maintainer="federico.razzoli@vettabase.com" \
	com.vettabase.license="GNU GPL 2.0" \
    description="WarpSQL by Justin Swanhart" \
	com.vettabase.maturity="alpha"


