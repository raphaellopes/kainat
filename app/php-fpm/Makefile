project = php-fpm
containerName = $(project).wpbase
imageName = $(project)
volumeName = www-html.wpbase

stop:
	- docker container stop $(containerName)

remove: stop
	- docker image rm -f $(imageName)

build: remove
	- docker build \
		-t $(imageName) \
		.

volume:
	- docker create \
		--name $(volumeName) \
		-v ~/Workspaces/manaca.dev/web:/var/www/html \
		tianon/true

run: volume
	- docker run -d --rm \
		--name $(containerName) \
		-h $(containerName) \
		-v /tpm:/tpm \
		-v custom.ini:/usr/local/etc/php/conf.d/custom.ini \
		--volumes-from $(volumeName) \
		$(imageName)
