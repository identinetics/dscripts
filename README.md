# Docker project template 

A docker image for running a XYZ instance. Has a few scripts around the docker commend that
is becoming unwiedly when one needs many arguments. Tries to be a thin wrapper around the
docerk CLI.

Features:
- By default, containers do not run as root, but have unique users mapped to the docker host
- The image produces immutable containers, i.e. a container can be removed and re-created
  any time without loss of data, because data is stored on mounted volumes.
- Configuration from a config file, building and running containers with the same script in
  different projects
- Consistent image, container, user and network mapping for multiple containers
- Data and config directories are mapped to the docker host, with consistent userids

## Configuration

1. Add this project to your docker project as a subdirectory or git submodule, e.g.

    git submodule add git@github.com:identinetics/dscripts.git
    git commit -m 'add submodule dscripts'
    # when you clone your project, you need to execute:    
    git submodule init
    git submodule update
    
2. From your project root copy default files:

    cp dscript/Dockerfile.default Dockerfile
    cp dscript/conf.sh.default confXX.sh  # set XX to a unique 2-digit number on your host
    cp dscript/build_prepare.sh.default build_prepare.sh  # optional
    
    
3. adapt Dockerfile, conf.sh and build_prepare.sh

## Usage

    build.sh [-h] [-i] [-n] [-p] [-r]
    run-sh [-h] [-i] [-n container-nr] [-p] [-r] -[R] [cmd]
    exec.sh [-h] [-i] [-n] [-p] [-r] [cmd]
    
   To run multiple XYZ containers on the same system you need to create separate 
   conf.sh files and build separate images:
   E.g. to create XYZ container instance 3:
   a) create a file conf3.sh, and set the IMGID=3; and
   b) build the container with the -n option, e.g. `build.sh -n 3`
   c) run the container with the -n option, e.g. `run.sh -n 3`
