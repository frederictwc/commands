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
find / -name file    # search all directories from the root for a file. 
control + h          # show hidden files in GUI
echo 'Hello world'   # print
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
docker build -t container_name:container_tag .
```
Create and start container. With name of container= container_name
``` 
docker run --name container_name xxxxx
```
### docker general
```
docker images                       # Show images
docker info                         # Check info 
docker ps                           # List all running Docker containers
docker ps -a                        # List all containers both running and stopped
docker start [options] container_id # Start an existing container[-it: interactive]
docker system prune                 # Delete all stopped containers, images and unused networks
docker container rm container_id    # Delete docker container
docker image rm image_id            # Delete docker image
docker run -it container_id bash    # SSH into a container
exit                                # exit SSHS
```
