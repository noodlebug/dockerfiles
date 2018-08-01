FROM ubuntu:18.04

RUN apt-get update
RUN apt-get -y install python wget 

ENV IDRIVE_VERSION 1.1.8

# ADD https://www.idrive.com/ldb/downloads/idrive-datacenteredition/IDrive-DataCenterEdition-${IDRIVE_VERSION}.tar.gz /IDrive-DataCenterEdition.tar.gz
COPY IDrive-DataCenterEdition-${IDRIVE_VERSION}.tar.gz /IDrive-DataCenterEdition.tar.gz

RUN tar xvf /IDrive-DataCenterEdition.tar.gz \
    && rm -f /IDrive-DataCenterEdition.tar.gz \
    && cd IDrive-DataCenterEdition-${IDRIVE_VERSION} \
    && ./ez_install.sh

RUN export IDRIVE_USER="idrive" \
    && export IDRIVE_UID="1100" \
    && export IDRIVE_GROUP="idrive" \
    && export IDRIVE_GID="1100" \
    && export IDRIVE_PASSWORD="idrive" \
    && groupadd ${IDRIVE_GROUP} --gid ${IDRIVE_GID} \
    && useradd --gid ${IDRIVE_GROUP} --uid ${IDRIVE_UID} ${IDRIVE_USER} \
    && echo "${IDRIVE_USER}:${IDRIVE_PASSWORD}" | chpasswd \
    && mkdir -p /home/idrive/.idrive && chown ${IDRIVE_USER}:${IDRIVE_GROUP} /home/idrive/.idrive


EXPOSE 5001
VOLUME ["/etc/idrive", "/home/idrive/.idrive", "/data"]
ENTRYPOINT ["python", "idrive_admin.py", "start"]