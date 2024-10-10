REGISTRY?=ghcr.io/steve-fraser
IMAGE_NAME?=$(REGISTRY)/node-rke2-airgapped
TAG?=dev

build:
	docker build -t $(IMAGE_NAME):$(TAG) .

push:
	docker push $(IMAGE_NAME):$(TAG)