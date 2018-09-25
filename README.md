# Jiri's dev box with python3, cpu-tf, vnc, etc. 
# how to build and run it:
# git clone git@github.com:ConSol/docker-headless-vnc-container.git
cd docker-headless-vnc-container/
docker build --no-cache -t jiri-tf-cpu -f ../ubuntu-desktops/Dockerfile.tf-cpu.vnc.jiri ./
docker build -t jiri-dev-box -f Dockerfile.jiri ./
docker run -d --cap-add sys_ptrace -p 5906:5901 --name jiri-dev-box -v/home/jiri/docker/home/jiri:/home/jiri -v/media/data1:/media/data1 -v/media/data5:/media/data5 -v/media/data3:/media/data3 -e VNC_PW=******** -e VNC_RESOLUTION=3384x1994 --user jiri jiri-dev-box

### GPU version
cd docker-headless-vnc-container/
docker build --no-cache -t jiri-tf-gpu -f ../ubuntu-desktops/Dockerfile.tf-gpu.vnc.jiri ./
cd ubuntu-desktops
docker build -t jiri-gpu-box -f Dockerfile.gpu.jiri ./
nvidia-docker run -d --cap-add sys_ptrace -p 5907:5901 --name jiri-gpy-box -v/home/jiri/docker/home/jiri:/home/jiri -v /nfs/mnt1/media/:/media/ -e VNC_PW=passw0rd -e VNC_RESOLUTION=3384x1994 --user jiri jiri-gpu-box
