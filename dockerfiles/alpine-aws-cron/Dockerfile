# Cron docker image with :
# - Supersonic to run crontab file (https://github.com/aptible/supercronic)
# - AWS cli to send content to s3
# - Timezone setup (UTC)
# - Service user uid 1001

FROM python:3.8-alpine

LABEL africa.encuisine.maintainer="mikamboo" \
      africa.encuisine.version="0.1.0" \
      africa.encuisine.tools="aws-cli,supersonic"

# Optional Configuration Parameter
ARG SERVICE_USER
ARG SERVICE_HOME

# Default Settings
ENV SERVICE_USER=${SERVICE_USER:-cronworker}
ENV SERVICE_HOME=${SERVICE_HOME:-/home/${SERVICE_USER}}

ENV SUPERCRONIC_URL=https://github.com/aptible/supercronic/releases/download/v0.1.9/supercronic-linux-amd64 \
    SUPERCRONIC=supercronic-linux-amd64 \
    SUPERCRONIC_SHA1SUM=5ddf8ea26b56d4a7ff6faecdd8966610d5cb9d85

RUN \
    adduser -h ${SERVICE_HOME} -s /sbin/nologin -u 1001 -D ${SERVICE_USER} \
    && apk add --no-cache dumb-init curl tzdata \
    && pip3 --no-cache install awscli \
    && cp /usr/share/zoneinfo/UTC /etc/localtime \
    && echo "UTC" >  /etc/timezone \
    && apk del tzdata 

RUN \
    curl -fsSLO "$SUPERCRONIC_URL" \
    && echo "${SUPERCRONIC_SHA1SUM}  ${SUPERCRONIC}" | sha1sum -c - \
    && chmod +x "$SUPERCRONIC" \
    && mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" \
    && ln -s "/usr/local/bin/${SUPERCRONIC}" /usr/local/bin/supercronic

USER    ${SERVICE_USER}
WORKDIR ${SERVICE_HOME}

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD [ "supercronic" ]
