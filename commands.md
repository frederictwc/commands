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

##C++##
how to run a c++ program
first use this command to compile 
```
g++ -o test filename.cpp
```
then run by
```
./test 
```

##bash general##
This will search all directories from the root for a file.
```
find / -name file
```
show hidden files(click in file manager)
```
control + h 
```

##Docker##
###How to create a docker container###
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
3. Create container. With name of container= container_name
``` 
docker run --name container_name xxxxx
```
###docker general###
Show images
```
docker images
```



