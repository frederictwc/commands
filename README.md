# Commands

## virtualenv, virtualenvwrapper
you can create a virtualenv using the following command:
```
virtualenv my_name
```
To create a Python 2.7 virtual environment, use the following command:
```
virtualenv -p /usr/bin/python2.7 virtualenv_name
```
to activate virtual environment
```
source virtualenv_name/bin/activate
```
activate virtualenv in my directory
```
source Documents/virtualenvs/realsense/bin/activate
```
to deactivate virtualenv
```
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
This will search all directories from the root for a file.
```
find / -name file
```
show hidden files(click in file manager)
```
control + h 
```
print a message
```
echo 'Hello world'
```

## Docker
### How to create a docker container
1. Create a dockerfile named Dockerfile. Then add these lines into it
```
FROM alpine
CMD ['echo','hi']
```
2. Build image: In dockerfile directory type
```
docker build . 
```
It should output successfully built xxxxx
3. Create and start container. With name of container= container_name
``` 
docker run --name container_name xxxxx
```
### How to run a python script inside a container 
Create a Dockerfile as follows:
```
FROM python:3.7
WORKDIR /usr/src/app     #This is where everything will be run
COPY requirements.txt ./ #copy this file to current dir
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["python","./python-script.py"]
```
Create a requirements.txt file 
```
numpy
pandas
```
Then do the rest build image run container

### docker general
Show images
```
docker images
```
Check info 
```
docker info
```
List all running Docker containers
```
docker ps
```
List all containers both running and stopped
```
docker ps -a
```
Start an existing container[-it: interactive]
```
docker start [options] container_id 
```
Delete all stopped containers, images and unused networks
```
docker system prune
```
Delete docker container
```
docker container rm container_id
```
Delete docker image
```
docker image rm image_id
```
SSH into a container
```
docker run -it container_id bash
```

