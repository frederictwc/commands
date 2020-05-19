# Commands

## virtualenv, virtualenvwrapper

```
virtualenv my_name                                   # create virtualenv
virtualenv -p /usr/bin/python2.7 virtualenv_name     # create python2.7 virtualenv
source Documents/virtualenvs/realsense/bin/activate  # activate virtualenv in my directory
deactivate
```
virtualenv files are located in home directory but hidden

## C++
how to run a c++ program
first use this command to compile 
```
g++ -o test filename.cpp
```
then run by
```
./test 
```

## bash general
```
find / -name file                                  # search all directories from the root for a file. 
control + h                                        # show hidden files in GUI
echo 'Hello world'                                 # print
ssh robotdata@192.168.50.163                       # ssh
scp /path/to/file username@a:/path/to/destination  # to copy a file from B to A while logged into B, a= IP
scp username@b:/path/to/file /path/to/destination  # To copy a file from B to A while logged into A
lscpu                                              # check cpu hardware, architecture
hostnamectl                                        # check OS 
df                                                 # check disk space
```

## Docker

### How to run a python script inside a container 
Create a Dockerfile as follows:
```
FROM python:3.7
WORKDIR /usr/src/app                               # This is where everything will be run
COPY requirements.txt ./                           # copy this file to current dir
RUN pip install --no-cache-dir -r requirements.txt
RUN apt-get update
RUN apt-get install libgtk2.0-dev
COPY . .                                           # copy everything in cur dir to workdir
CMD ["python","./python-script.py"]
```
A "." simply means current working dir. 
Create a requirements.txt file 
```
numpy
pandas
```
Then build 
```
docker build -t image_name:image_tag .
```
Create and start container. With name of container= container_name
``` 
docker run --name container_name image_tag
```
### docker general
```
docker images                                 # Show images
docker info                                   # Check info 
docker ps                                     # List all running Docker containers
docker ps -a                                  # List all containers both running and stopped
docker start [options] container_id           # Start an existing container[-it: interactive]
docker system prune                           # Delete all stopped containers, images and unused networks
docker container rm container_id              # Delete docker container
docker image rm image_id                      # Delete docker image
docker run -it image_id bash                  # SSH into a container
exit                                          # exit SSH
x11docker image_id                            #run docker container with GUI output
docker rm $(docker ps -a -f status=exited -q) #delete all inactive containers
docker run --device=/dev/video3 image_id      # pass a device and run container(doesnt seem to work,use next one below)
docker run --privileged image_id              # pass all devices to container
x11docker --share /dev/usb2 realsense         #pass a device and run GUI container
x11docker --webcam image_id                   # pass any webcam into GUI container
```

## matplotlib
Plot in loop
```python
from matplotlib import pyplot as plt
try:
    plt.ion()
    while True:
        plt.plot(array)
        plt.draw()
        plt.pause(0.1)
        plt.clf()
```
