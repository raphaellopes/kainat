include ../.env

project = php-fpm
containerName = $(project).wpbase
imageName = $(project)
volumeName = www-html.wpbase

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
		-t $(imageName) \
		.

volume:
	- docker create \
		--name $(volumeName) \
		-v ${LOCAL_ROOT_DIR}:/var/www/html \
		tianon/true

run: volume ## Run container
	- docker run -d --rm \
		--name $(containerName) \
		--env-file=../.env \
		-h $(containerName) \
		-v /tpm:/tpm \
		-v custom.ini:/usr/local/etc/php/conf.d/custom.ini \
		--volumes-from $(volumeName) \
		$(imageName)
