FROM --platform=linux/x86_64 mysql:8.0 

ENV TZ=UTC

COPY ./Docker/mysql/my.cnf /etc/my.cnf
RUN chmod 777 /etc/my.cnf