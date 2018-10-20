
## Various docker images of Jiri's

Please note that docker-headless-vnc-container is a snapshot of git@github.com:ConSol/docker-headless-vnc-container.git 
and you may want to see if that repo got some significant updates, separately.

### TF-CPU dev-box with all kinds of tooling
`cd docker-headless-vnc-container/`
`docker build --no-cache -t jiri-tf-cpu -f ./Dockerfile.tf-cpu.vnc.jiri ./`
`docker build -t jiri-dev-box -f Dockerfile.ecl.jiri ./`
`docker run -d --cap-add sys_ptrace -p 5906:5901 --name jiri-dev-box -v/home/jiri/docker/home/jiri:/home/jiri -v/media/data1:/media/data1 -v/media/data5:/media/data5 -v/media/data3:/media/data3 -e VNC_PW=******** -e VNC_RESOLUTION=3384x1994 --user jiri jiri-dev-box`

### GPU version of the dev-box
`cd docker-headless-vnc-container/`
`docker build --no-cache -t jiri-tf-gpu -f ../ubuntu-desktops/Dockerfile.tf-gpu.vnc.jiri ./`
`cd ubuntu-desktops`
`docker build -t jiri-gpu-box -f Dockerfile.gpu.ecl.jiri ./`
`nvidia-docker run -it -d --cap-add sys_ptrace -p 5906:5901 --name jiri-gpu-box -v/home/jiri/docker/home/jiri:/home/jiri -v/raid:/media -e VNC_PW=********* -e VNC_RESOLUTION=3384x1994 --user jiri jiri-gpu-box /bin/bash`
