# Commands

##nvidia
watch -n 1 nvidia-smi

## virtualenv, virtualenvwrapper

```
virtualenv my_name                                   # create virtualenv
virtualenv -p /usr/bin/python2.7 virtualenv_name     # create python2.7 virtualenv
source Documents/virtualenvs/realsense/bin/activate  # activate virtualenv in my directory
deactivate
```
virtualenv files are located in home directory but hidden
for python3
```
python3 -m venv <venv_name>
source <venv_name/bin/activate>
```


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
find . -name file                                  # search current directory for a file
control + h                                        # show hidden files in GUI
echo 'Hello world'                                 # print
ssh robotdata@192.168.50.163                       # ssh
ssh -p <port> <computer_name>@<public_ip>          # ssh from outside network
scp /path/to/file username@a:/path/to/destination  # to copy a file from B to A while logged into B, a= IP
scp username@b:/path/to/file /path/to/destination  # To copy a file from B to A while logged into A
scp -r robotdata@192.168.1.127:~/Documents/jetson_inference /home/fred/Documents/jetson-nano-backup

lscpu                                              # check cpu hardware, architecture
hostnamectl                                        # check OS 
df                                                 # check disk space
du -h --max-depth=1                                # size of directories
hostname -I                                        # get IP address
startx                                             # start GUI
ps -aux                                            # check processes
sudo du -sh <dir>                                  # check file size in <dir>
for filename in ./*; do mv "./$filename" "./$(echo "$filename" | sed -e 's/test.extra//g')";  done # remove part of filename of all files in directory
arp -a                                             # scan IP addresses on network
sshpass -p robot-data3388 scp start.sh rd-dev@192.168.50.101:~/Desktop/HKPCFacialRecognition  # scp with a password
sudo lsof -i -P -n | grep LISTEN                   # check all ports in use
pkill -f "Process name"                            # kill process by name

```
## OSX
```
ipconfig getifaddr en0                             # get ip address
```
### How to run a GUI docker in OSX
run xquartz
```
open -a XQuartz
```
make sure preferences/security is allowing connections from network clients
```
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```
open a new terminal and run docker container
```
docker run -d -e DISPLAY=<ip address of computer>:0 <docker image>
```
alternatively, run with interactive mode then go into container
```
docker run -it -d -e DISPLAY=<ip address of computer>:0 <docker image>
```
then open a terminal in container 
```
docker exec -it <container name> /bin/bash
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
docker run -it -v <path outside container>:<path inside container> test_1 bash # pass a directory into container.
docker run -it -v ~/frederictwc/tracking/test-gui:/frederictwc/tracking/test-gui -e DISPLAY=10.0.202.26:0    test # tried running cv2.imshow, opens window then immediately closes. but even in that quick second the image is all black
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
## git

```
git init                                      #create local git repository in the project folder, add files to this folder
git status                                    # check for files that git has identified
git add <filename>                            # add a file to staging envir
git commit -m "Your message about the commit" # then package files into a commit
git checkout -b <my branch name>              # create new branch and go into it
git branch                                    # check branches
git push origin <branch_name>                 # push to existing branch
git branch -d localBranchName                 # delete branch locally
git push origin --delete remoteBranchName     # delete branch remotely
git push -u origin <branch_name>              # push local branch to remote
git mv <source> <destination>                 # move folder, remember to push 
git clone --single-branch --branch <branchname> <remote-repo> #clone single branch
git submodule add <repo> <dir>                # add submodule, still need to commit
git submodule foreach git pull                # git pull for all submodules
git remote | xargs -n1 git remote remove      # remove all remotes
```
push an existing local repo onto github
```
git remote add origin https://github.com/frederictwc/<repo>.git
git push -u origin master
```
merge steps: first push changes in <branch_name>
```
git checkout master
git merge <new_branch>
git push
```
add a local branch <local branch> in repo1 to a new remote branch <new remote branch> in repo2
```
git remote add origin2 https://github.com/frederictwc/<repo2>.git
git push origin2 <local branch>:<new remote branch>
```
update local master with origin
```
git fetch --all
git reset --hard origin/master
```
clone a repo with submodules, after cloning
```
git submodule init
git submodule update
```
remove a commited submodule
```
git submodule deinit <path_to_submodule>
git rm <path_to_submodule>
git commit-m "Removed submodule "
rm -rf .git/modules/<path_to_submodule>
```
## DIGITS
start container with DIGITS
```
docker run --gpus all -d -p 8888:5000 <image>
```
open following link in browser 
```
<digits computer ip>:8888 
```
