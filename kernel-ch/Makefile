REGISTRY?=ghcr.io/steve-fraser
IMAGE?=cloudhypervisor-kernel
IMAGE_NAME?=$(REGISTRY)/$(IMAGE)

build:
	docker build \
		-t $(IMAGE_NAME):6.2 \
		--build-arg KERNEL_VERSION=6.2 \
		--build-arg KERNEL_CONFIG=https://raw.githubusercontent.com/cloud-hypervisor/cloud-hypervisor/main/resources/linux-config-x86_64 \
		.

push:
	docker push $(IMAGE_NAME):6.2