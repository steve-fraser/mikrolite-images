REGISTRY?=ghcr.io/mikrolite
IMAGE?=firecracker-kernel
IMAGE_NAME?=$(REGISTRY)/$(IMAGE)
TAG?=6.1

build:
	docker build -t $(IMAGE_NAME):$(TAG) .

push:
	docker push $(IMAGE_NAME):$(TAG)