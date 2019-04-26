# import .env
# You can change the default config with `make env="custom.env" build`
env ?= ../.env
include $(env)

project = redis
containerName = $(project).kainat
imageName = $(project):alpine
volumeName = $(project).kainat
port = 6379

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
	- docker container rm -f $(containerName)

logs: ## Show logs
	- docker container logs $(containerName)

run: ## Run container on port configured on `.env` file
	- docker run -d -t \
		--name $(containerName) \
		-h $(containerName) \
		-p $(port):6379 \
		-v /tpm:/tpm \
		$(imageName)

bash: ## Start bash inside container
	- docker exec -it ${containerName} bash

