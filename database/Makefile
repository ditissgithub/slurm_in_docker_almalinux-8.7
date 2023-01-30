
SLURM_VERSION = 20.11.9
IMAGE = cdac_slurm.database

.PHONY: all build clean test


all: build

build:
	docker build -t $(IMAGE):$(SLURM_VERSION) .

clean:
	@[ -z $(docker images -q $(IMAGE):$(SLURM_VERSION)) ] || docker rmi $(IMAGE):$(SLURM_VERSION)
