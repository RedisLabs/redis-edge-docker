
ROOT=..
MK.pyver:=3
include $(ROOT)/deps/readies/mk/main

# OSNICK=buster|stretch|bionic
OSNICK ?= bionic # buster

REPO=redisedge

ifeq ($(JETSON),1)
DOCKER_SUFFIX=.jetson
endif

DOCKERFILE_STEM=$(ROOT)/edge/Dockerfile$(DOCKER_SUFFIX)

include ../versions

DOCKER_BUILD_ARGS += \
	REDISAI_VERSION=$(REDISAI_VERSION) \
	REDISTIMESERIES_VERSION=$(REDISTIMESERIES_VERSION) \
	REDISGEARS_VERSION=$(REDISGEARS_VERSION)

# override defines for the case
ifdef REDISGEARS_DOCKERDEP
DOCKER_BUILD_ARGS += \
	VERSION=edge \
	REDISGEARS_DOCKERDEP=$(REDISGEARS_DOCKERDEP)
endif

ifdef REDISAI_DOCKERDEP
DOCKER_BUILD_ARGS += \
	REDISAI_DOCKERDEP=$(REDISAI_DOCKERDEP)
endif

ifdef REDISTIMESERIES_DOCKERDEP
DOCKER_BUILD_ARGS += \
	REDISTIMESERIES_DOCKERDEP=$(REDISTIMESERIES_DOCKERDEP)
endif

ifdef REDIS_DOCKERDEP
DOCKER_BUILD_ARGS += \
	REDIS_DOCKERDEP=$(REDIS_DOCKERDEP)
endif

ifdef DOCKER_ORG
DOCKER_BUILD_ARGS += \
	DOCKER_ORG=$(DOCKER_ORG)
endif



include $(MK)/docker.native
