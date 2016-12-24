# docker image version
VERSION := latest
# The name of the docker image.
IMAGE_NAME := clue/apt-cacher:$(VERSION)
# docker container name
NAME := apt_cacher
# Set the option PORTS='-p 53:53/udp' to use the DNS server on localhost.
PORTS := -p 3142:3142
# Cache directory.
CACHE_DIR := /var/cache/apt-cacher

define DOCKER_CMD :=
docker run \
--name $(NAME) \
$(PORTS) \
-v "$(CACHE_DIR):/var/cache/apt-cacher" \
-d \
$(IMAGE_NAME)
endef

include ../docker_make_utils/Makefile.help
include ../docker_make_utils/Makefile.functions
include ../docker_make_utils/Makefile.container

.PHONY +: run rerun rm clean test restart bash

run: $(CACHE_DIR) _run ##@default Starts the container.

rerun: _rerun ##@targets Stops and starts the container.

rm: _rm ##@targets Stops and removes the container.

clean: _clean _rm_dataContainer ##@targets Stops and removes the container and removes all created files.
	sudo rm -rf $(CACHE_DIR)

test: _testDataContainer _test ##@targets Tests if the container is running.
	
restart: _restart ##@targets Restarts the container.

bash: test _bash ##@targets Executes the bash inside the running container.

$(CACHE_DIR):
	sudo mkdir -p "$(CACHE_DIR)"
