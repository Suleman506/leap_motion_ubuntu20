# leap_motion_ubuntu20
Run Leap motion controller 2 on Ubuntu 20 via docker
Step 1: Install docker on ubuntu 20.04.
Step 2: Clone this repository to get the docker file.
Step 3: Build the docker file
```
cd leap_motion_ubuntu20
git clone https://github.com/ultraleap/leapc-python-bindings.git
sudo docker build -t leapmotion -f leap.Dockerfile .
```
Step 4: Connect the leap motion conroller 2 with PC via USB cable. Open three terminals and execute the commands below one by one 
```
export DISPLAY=:0
xhost +local:docker
sudo docker run -it   --privileged   --net=host --mount type=bind,source=/dev/bus/usb,target=/dev/bus/usb   -e DISPLAY=$DISPLAY   -v $HOME/.Xauthority:/root/.Xauthority:ro   -v /run/user/$(id -u):/run/user/$(id -u)   --name leapmotion_$(uuidgen)   leapmotion leapd
```
```
sudo docker run -it --privileged --net=host --mount type=bind,source=/dev/bus/usb,target=/dev/bus/usb -e DISPLAY=$DISPLAY -v $HOME/.Xauthority:/root/.Xauthority:ro -v /run/user/$(id -u):/run/user/$(id -u) --name leapmotion_$(uuidgen) --entrypoint "/bin/bash" leapmotion -c "yes | leapctl eula; bash"
```
```
sudo docker run -it   --privileged   --net=host --mount type=bind,source=/dev/bus/usb,target=/dev/bus/usb   -e DISPLAY=$DISPLAY   -v $HOME/.Xauthority:/root/.Xauthority:ro   -v /run/user/$(id -u):/run/user/$(id -u)   --name leapmotion_$(uuidgen)   leapmotion ultraleap-hand-tracking-control-panel
```
