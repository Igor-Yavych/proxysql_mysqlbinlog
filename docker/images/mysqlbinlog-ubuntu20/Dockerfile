FROM ubuntu:20.04

LABEL authors="Miro Stauder <miro@proxysql.com>"

# dependencies
RUN apt-get -y update && \
	apt-get -y install \
	libssl1.1

# copy package from context
COPY proxysql-mysqlbinlog_*.deb ./
RUN bash -c "yes | dpkg -i proxysql-mysqlbinlog_*$(dpkg --print-architecture).deb" && \
	rm -f proxysql-mysqlbinlog_*.deb

CMD ["sh", "-c", "proxysql_binlog_reader -h \"${MYSQL_HOST:-127.0.0.1}\" -u \"${MYSQL_USER:=root}\" -p \"${MYSQL_PASSWORD:-root}\" -P \"${MYSQL_PORT:-3306}\" -l \"${LISTEN_PORT:-6020}\" -f"]
