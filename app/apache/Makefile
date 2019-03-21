include ../.env

project = httpd
containerName = $(project).wpbase
imageName = $(project):2.4

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

run: ## Run container on port configured on `.env`
	- @echo $(APACHE_EXPOSED_PORT) 
	- docker run -dit --rm \
		--env-file=../.env \
		--dns 172.17.0.1 \
		--name $(containerName) \
		--link php-fpm.wpbase:php-fpm.wpbase \
		-p $(APACHE_EXPOSED_PORT):80 \
		-v ${LOCAL_ROOT_DIR}:$(APACHE_ROOT_DIR)/htdocs/ \
		$(imageName)

bash: ## Start bash inside container
	- docker exec -it ${containerName} bash
