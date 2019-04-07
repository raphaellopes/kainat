# import .env
# You can change the default config with `make env="custom.env" build`
env ?= ../.env
include $(env)

project = mysql
containerName = $(project).kainat
imageName = $(project):5.7
volumeName = $(project).kainat

# HELP
# This will output the help for each task
# thanks to https://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
.PHONY: help

help: ## This help
	- @awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-15s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

# Docker tasks
stop: ## Stop a running container
	- docker container stop $(containerName)

remove: stop ## Remove and stop a running container
	- docker image rm -f $(imageName)
	- docker volume rm -f $(volumeName)

logs: ## Show logs
	- docker container logs $(containerName)

volume: ## Create volume to be use on this container
	- docker volume create $(volumeName)

run: volume ## Run container on port configured on `.env` file
	- docker run -d --rm \
		--name $(containerName) \
		-p 3307:3306 \
		-h $(containerName) \
		-v ~/Workspace/manaca-site/dumps/2019-04-05.sql:/docker-entrypoint-initdb.d/dump.sql \
		-v /tpm:/tpm \
		-v $(volumeName):/var/lib/mysql \
		-e MYSQL_ROOT_PASSWORD=$(MYSQL_ROOT_PASSWORD) \
		-e MYSQL_DATABASE=$(MYSQL_DATABASE) \
		-e MYSQL_USER=$(MYSQL_USER) \
		-e MYSQL_PASSWORD=$(MYSQL_PASSWORD) \
		$(imageName)

bash: ## Start bash inside container
	- docker exec -it ${containerName} bash

