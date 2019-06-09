# TAG raffapen/redisedgevision-${ARCH}-${OSNICK}:latest

ARG OSNICK=bionic
# ARG ARCH=x64|arm64|arm7l

#----------------------------------------------------------------------------------------------
FROM raffapen/redisai-${OSNICK}:latest as ai
FROM raffapen/redistimeseries-${OSNICK}:latest as timeseries 
FROM raffapen/redisgears-${OSNICK}:latest as gears
FROM raffapen/redisedgevisionlibs-${OSNICK}:latest as visionlibs

#----------------------------------------------------------------------------------------------
FROM raffapen/redis-${OSNICK}:5.0.5

RUN apt-get update; apt-get install -y libgomp1

WORKDIR /data

ENV REDISMODULES_LIBS /usr/lib/redis/modules
ENV LD_LIBRARY_PATH ${REDISMODULES_LIBS}:${LD_LIBRARY_PATH}
RUN mkdir -p ${REDISMODULES_LIBS}

COPY --from=timeseries ${REDISMODULES_LIBS}/*.so ${REDISMODULES_LIBS}/
COPY --from=ai         ${REDISMODULES_LIBS}/*.so* ${REDISMODULES_LIBS}/
COPY --from=gears      /opt/redislabs/lib/modules/redisgears.so ${REDISMODULES_LIBS}/
COPY --from=gears      /opt/redislabs/ /opt/redislabs/
COPY --from=visionlibs /usr/local/ /usr/local/

CMD ["--loadmodule", "/usr/lib/redis/modules/redistimeseries.so", \
     "--loadmodule", "/usr/lib/redis/modules/redisai.so", \
     "--loadmodule", "/usr/lib/redis/modules/redisgears.so", \
     "PythonHomeDir", "/opt/redislabs/lib/modules/python3/"]