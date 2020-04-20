FROM python:3.8-alpine

LABEL africa.encuisine.maintainer="mikamboo" \
      africa.encuisine.version="0.1.0" \
      africa.encuisine.tools="mysql-client,aws-cli"

# Optional Configuration Parameter
ARG SERVICE_USER
ARG SERVICE_HOME

# Default Settings
ENV SERVICE_USER ${SERVICE_USER:-mysql}
ENV SERVICE_HOME ${SERVICE_HOME:-/home/${SERVICE_USER}}

RUN \
    adduser -h ${SERVICE_HOME} -s /sbin/nologin -u 1001 -D ${SERVICE_USER} && \
    apk add --no-cache \
    dumb-init \
    mariadb-client && \
    pip3 --no-cache install awscli

USER    ${SERVICE_USER}
WORKDIR ${SERVICE_HOME}

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD [ "mysql" ]
