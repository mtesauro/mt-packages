Steps to build a new packge in mt-packages

1. cd to apps
1. run the new-packages script
1. cd into your new directory
1. Run launch-docker build to get a build environment


Example run:

```
$ cd apps/
$ ../scripts/new-package taskwarrior

You want to create a package for taskwarrior.  Is this correct? [y/n]: y

Creating directory structure for taskwarrior...

The app taskwarrior is ready for packaging at /home/mtesauro/Dropbox/projects/mtesauro-packages/apps/taskwarrior

Go forth and conquer
$ cd taskwarrior
$ ../../scripts/launch-docker build

Entering Build Docker ubuntu:16.04
  [in the launched docker]
# cd /opt/taskwarrior
# ls
README.md  build-taskwarrior  make-taskwarrior-packages  packages  pkg-root  references  scripts  source
# ./scripts/docker-preinstalls
# cd source
# wget https://taskwarrior.org/download/task-2.5.1.tar.gz
```

Ideally you'll run ./build-taskwarrior to do the necessary build - assuming you've built this before and have those steps documented in that script. 

When you're done to CTRL+p and CTRL+q to exit the Docker image and...

```
Exited Build Docker 

Do you want to clean up (delete) the docker build image? [y/n]: y

Stopping the build-taskwarrior docker
build-taskwarrior
Deleting the build-taskwarrior docker
build-taskwarrior
```