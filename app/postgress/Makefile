# import .env
# You can change the default config with `make env="custom.env" build`
env ?= ../.env
include $(env)

project = postgres
containerName = $(project).kainat
imageName = $(project)
volumeName = $(project).kainat
port = 5432

# HELP
# This will output the help for each task
# thanks to https://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
.PHONY: help

help: ## This help
	- @awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-15s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

# Docker tasks
start: ## Starts a stopped container
	- docker container start $(containerName)

stop: ## Stop a running container
	- docker container stop $(containerName)

remove: stop ## Remove and stop a running container
	- docker image rm -f $(imageName)
	- docker volume rm -f $(volumeName)
	- docker container rm -f $(containerName)

build: remove ## Build a new container
	- docker build \
		--no-cache \
		-t $(imageName) \
		.

logs: ## Show logs
	- docker container logs $(containerName)

volume: ## Create volume to be use on this container
	- docker volume create $(volumeName)

run: volume ## Run container on port configured on `.env` file
	- docker run -d \
		--name $(containerName) \
		-h $(containerName) \
		-p $(port):5432 \
		-v /tpm:/tpm \
		-v $(volumeName):/var/lib/postgresql/data \
		$(imageName)

bash: ## Start bash inside container
	- docker exec -it ${containerName} bash

