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
# ./build-taskwarrior
```

Ideally you'll run ./build-taskwarrior to do the necessary build - assuming you've built this before and have those steps documented in that script. 

If this is the first time you've packaged this, you'll need to do a couple of things first:

1. Edit make-[app name]-pacakges to provide values used when packaging
1. Fill in build-[app name] with the commands necessary to build the app
⋅⋅1. If you need to install build pre-requisites, put those in a bash script in the scripts directory called 'docker-preinstalls' which should take the default docker to the state you need to build the package.  At the very least, change any place with "EDIT" as the value.
⋅⋅1. You can call your docker-preinstalls script from build-[app name] to remove the need to call it directly before you do your build.  There is value in having it separate so that difference betweeen Linux releases like library names can be isolated into only that file.
1. chmod u+x those scripts
1. Fire up the build docker with $ ../../scripts/launch-docker build
1. Run the build-[app name] script and make sure it runs cleanly

When you're done to CTRL+p and CTRL+q to exit the Docker image and...

```
Exited Build Docker 

Do you want to clean up (delete) the docker build image? [y/n]: y

Stopping the build-taskwarrior docker
build-taskwarrior
Deleting the build-taskwarrior docker
build-taskwarrior
```

NOTE:  You can not delete the build image and return to it later if you need to pause packaging work for some reason.

Next, you'll need to create the Debian and RPM packages after building the app.  To do that, rerun the launch-docker script but for FPM:

```
$ ../../scripts/launch-docker FPM
```

PUT OUTPUT OF THE COMMANDS ABOVE