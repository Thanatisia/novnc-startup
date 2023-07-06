# Dockerfile for NodeJS Web server

## Pull Base Image
FROM debian:latest

## Arguments/Variables
ARG PYTHON_DEPENDENCIES=./dependencies/python/requirements.txt

## Set Environment Variables
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

### Project
# ENV VNC_WEB_CLIENT="/usr/share/novnc"
# ENV VNC_WEB_PORT="6080"
# ENV VNC_SERVER_HOST_IP="localhost"
# ENV VNC_SERVER_HOST_PORT="5901"
# ENV OTHER_OPTIONS="-D"
ENV VNC_WEB_CLIENT=
ENV VNC_WEB_PORT=
ENV VNC_SERVER_HOST_IP=
ENV VNC_SERVER_HOST_PORT=
ENV OTHER_OPTIONS=

## Set Current Working Directory
WORKDIR /usr/src/app

## Copy dependencies and required files
### Python pip package requirements
# COPY ${PYTHON_DEPENDENCIES} ${PYTHON_DEPENDENCIES}
COPY ./docker/dependencies/python/requirements.txt ./dependencies/python/requirements.txt

## Update package manager and packages
RUN DEBIAN_FRONTEND=noninteractive \
    apt update -y && \
    apt upgrade -y && \
    ## Install other dependencies \
    apt install -y vim git nodejs npm python3 python3-pip python3-venv novnc

## Install python packages into a virtual environment using requirements.txt
RUN python3 -m venv $VIRTUAL_ENV && \
    $VIRTUAL_ENV/bin/pip install --upgrade pip && \
    $VIRTUAL_ENV/bin/pip install -Ur ${PYTHON_DEPENDENCIES}

## Install Manual Repositories
### NoVNC - If using a non-apt base image
# RUN git clone https://github.com/novnc/novnc /usr/share/novnc

## Run additional commands

## Set defaults

## Expose Ports
# EXPOSE 6080

## Run command

## Set Entry Point 
# Default: websockify -D --web=/usr/share/novnc 6080 localhost:5901
# ENTRYPOINT websockify ${OTHER_OPTIONS} --web=${VNC_WEB_CLIENT} ${VNC_WEB_PORT} ${VNC_SERVER_HOST_IP}:${VNC_SERVER_HOST_PORT}
# ENTRYPOINT /usr/bin/websockify ${OTHER_OPTIONS} --web=${VNC_WEB_CLIENT} ${VNC_WEB_PORT} ${VNC_SERVER_HOST_IP}:${VNC_SERVER_HOST_PORT}
ENTRYPOINT ["/bin/bash"]


