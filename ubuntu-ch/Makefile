REGISTRY?=ghcr.io/steve-fraser
IMAGE_NAME?=$(REGISTRY)/ubuntu-ch
TAG?=22.04

build:
	docker build -t $(IMAGE_NAME):$(TAG) .

push:
	docker push $(IMAGE_NAME):$(TAG)