ARG REDIS_VERSION
FROM redis:${REDIS_VERSION}

ARG REIDS_DOCKER_DATA_DIR
RUN mkdir -p ${REIDS_DOCKER_DATA_DIR}

CMD [ "redis-server", "/etc/redis.conf" ]