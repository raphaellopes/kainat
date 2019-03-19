include ../.env

project = httpd
containerName = $(project).wpbase
imageName = $(project):2.4

stop:
	- docker container stop $(containerName)

remove: stop
	- docker image rm -f $(imageName)

build: remove
	- docker build \
		-t $(imageName) \
		.

logs:
	- docker container logs $(containerName)

run:
	- @echo $(APACHE_EXPOSED_PORT) 
	- docker run -dit \
		--name $(containerName) \
		-p $(APACHE_EXPOSED_PORT):80 \
		-v ~/Workspaces/manaca.dev/web:$(APACHE_ROOT_DIR)/htdocs/ \
		$(imageName)
