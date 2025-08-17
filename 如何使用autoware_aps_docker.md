# autoware_aps docker 的使用方法

制作autoware_apsdocker的目的是为了让UI开发者方便测试UI与autoware的通信，而不必安装复杂的autoware车给你需

## step1: 准备工作

1.安装docker 

2.下载autoware_aps docker 镜像

![alt text](<docs/Screenshot from 2025-08-17 14-33-11.png>)

## step2: 加载docker镜像

```
docker load -i autoware_aps.tar
```

![alt text](<docs/Screenshot from 2025-08-17 14-41-48.png>)

## step3: 运行docker镜像

注意docker run 的参数 --device=/dev/dri:/dev/dri 是指定机器的显卡，不同的机器可能不一样，如果要适配自己的机器请问AI。
其实不要这个参数也行，但是autoware rviz界面会很卡

```
docker run -it --rm --network=host  -e DISPLAY=$DISPLAY   -e QT_QPA_PLATFORM=xcb   -e QT_X11_NO_MITSHM=1   -v /tmp/.X11-unix:/tmp/.X11-unix:rw   --device=/dev/dri:/dev/dri   --ipc=host --shm-size=1g   autoware_aps:latest bash
```

![alt text](<docs/Screenshot from 2025-08-17 14-44-49.png>)

在主机上运行
```
xhost +
```
![alt text](<docs/Screenshot from 2025-08-17 14-49-11.png>)

## step4: 在docker容器中运行autoware_aps

```
cd autoware.APS/
source install/setup.bash
ros2 launch autoware_launch planning_simulator.launch.xml map_path:=/sample-map-planning  
```
![alt text](<docs/Screenshot from 2025-08-17 14-53-57.png>)
![alt text](<docs/Screenshot from 2025-08-17 14-54-55.png>)