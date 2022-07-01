FROM amazoncorretto:17

# Based on https://github.com/oscarfonts/docker-h2/blob/master/alpine/Dockerfile

ENV DOWNLOAD https://github.com/h2database/h2database/releases/download/version-2.1.214/h2-2022-06-13.zip
ENV DATA_DIR /home/h2-data

RUN yum -y install curl unzip && yum -y clean all  && rm -rf /var/cache

RUN mkdir -p ${DATA_DIR} \
    && curl -L ${DOWNLOAD} -o h2.zip \
    && unzip h2.zip -d /home/ \
    && rm h2.zip

EXPOSE 81 1521

WORKDIR /home/h2-data

# Databases shouldn't be created on first access on production (remove -ifNotExists and create them e.g. via console)
CMD java -cp /home/h2/bin/h2*.jar org.h2.tools.Server \
  -ifNotExists \
 	-web -webAllowOthers -webPort 81 \
 	-tcp -tcpAllowOthers -tcpPort 1521 \
 	-baseDir ${DATA_DIR} ${H2_OPTIONS}