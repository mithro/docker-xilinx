
Dockerize Xilinx tools to allow "throw away" environment for doing CI style builds.

# Running the container

```bash
docker run -t \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=$DISPLAY \
  \
  -v /home/tansell/.Xilinx:/home/xilinx/.Xilinx \
  \
  -i mithro/xilinx-ise:14.7-1015-base \
  /bin/bash
```

# Larger Docker Containers

Add "--storage-opt dm.basesize=30G" to your /etc/default/docker file. Then stop
docker, **remove all your docker images** and start docker again.

This option **won't** take effect until you remove all your images and start
again, sorry about that :(.

```bash
DOCKER_OPTS="${DOCKER_OPTS} --storage-driver=devicemapper --storage-opt dm.basesize=30G"
```

# Getting the GUI tools working

Allow X connections from anywhere with `xhost +` on container.

Run docker container with the following extra arguments;
 * `-v /tmp/.X11-unix:/tmp/.X11-unix` - Maps the X11 sockets into the docker container. 
 * `-e DISPLAY=$DISPLAY` - Set up the $DISPLAY environment variable.

See http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/

# License stuff
`-v /home/$USER/.Xilinx:/home/xilinx/.Xilinx` - Maps the Xilinx license files into the docker container.

 - [ ] FIXME: How to deal with docker MAC address stuff?

# Mapping USB into docker

`--device=/dev/bus/usb/001/001`


