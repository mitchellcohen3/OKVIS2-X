# Docker Installation Instructions

Clone the repo into a catkin workspace source folder using
```bash
mkdir -p catkin_ws/src
cd catkin_ws/src
git clone --recurse-submodules git@github.com:ethz-mrl/OKVIS2-X.git
cd docker
```
Build the docker image using
```bash
docker build -t okvis2x Dockerfile_ros2_22_04 .
```

Then, run the docker container by adding the following alias to your `~/.bashrc` file
```bash
export OKVIS_FOLDER="/path/to/okvis2x"
alias okvis2x_docker="docker run -it --net=host --gpus all \
    --memory="6g" --memory-swap="6g" \
    --device /dev/dri \
    --env=\"NVIDIA_DRIVER_CAPABILITIES=all\" --env=\"DISPLAY\" \
    --env=\"QT_X11_NO_MITSHM=1\" --volume=\"/tmp/.X11-unix:/tmp/.X11-unix:rw\" \
    --mount type=bind,source=$OKVIS_FOLDER,target=/okvis2x \
    --mount type=bind,source=$DOCKER_DATASETS,target=/datasets okvis2x bash"
```

The container can then be started by running
```bash
okvis2x_docker
```