
SLURM_VERSION = 20.11.9
IMAGE = scidas/slurm.base

DIR := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

.PHONY: all build clean test

all: build

build:
	cp -r "$(DIR)/../packages/almalinux-8.7/rpms" .
	docker build -t $(IMAGE):$(SLURM_VERSION) .

clean:
	@[ -z $(docker images -q $(IMAGE):$(SLURM_VERSION)) ] || docker rmi $(IMAGE):$(SLURM_VERSION)
	rm -rf rpms
