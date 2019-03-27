# import .env
# You can change the default config with `make env="custom.env" build`
env ?= ../.env
include $(env)

project = httpd
containerName = $(project).kainat
imageName = $(project):2.4
volumeName = www-html.kainat

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

logs: ## Show logs
	- docker container logs $(containerName)

build: remove ## Build a new container
	- docker build \
		--no-cache \
		-t $(imageName) \
		.

volume:
	- docker create \
		--name $(volumeName) \
		-v ${LOCAL_ROOT_DIR}:${APACHE_ROOT_DIR}/htdocs \
		tianon/true

run: volume ## Run container on port configured on `.env` file
	- docker run -dit --rm \
		-p $(APACHE_EXPOSED_PORT):80 \
		--name $(containerName) \
		--env-file=$(env) \
		--link php-fpm.kainat:php-fpm.kainat \
		--volumes-from $(volumeName) \
		$(imageName)

bash: ## Start bash inside container
	- docker exec -it ${containerName} bash

up: build run ## Run container on port configured in `.env` file (Alias to run)
