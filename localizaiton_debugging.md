# localization 调试日志，从零开始

## Step 1 安装依赖 

请参考 README.md ,先把README中的内容能运行，就说明环境配置好了

## Step 2 下载autoware库

```
git clone https://github.com/libpet-co/autoware.APS.git

```

## Step 3 Setup workspace
```
cd autoware.APS
mkdir src
vcs import src < autoware.repos
```

## Step 4 下载数据

1） APS车的模型 aps2.dae，注意路径

```
gdown -O src/launcher/autoware_launch_APS/vehicle/aps_vehicle_launch/aps_vehicle_description/mesh/aps2.dae  'https://drive.google.com/uc?id=1JFPvChA3dt0KyEM8-l4DqiAY18JekRlM'
```
2） ros2 bag 数据
```
mkdir data
gdown -O data/ros2_bag_data.zip  'https://drive.google.com/uc?id=1ugzhulnHvblLenjpAMu5oOVOPWNH1xkB'
unzip -d data data/ros2_bag_data.zip
```
## Step 5 编译

```
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release
```

## Step 6 启动 autoware localization 测试
```
source install/setup.bash
ros2 launch autoware_launch test_localization.launch.xml map_path:=/home/libpet/autoware_map/sample-map-planning-APS vehicle_model:=aps_vehicle sensor_model:=aps_sensor_kit
``` 

## Step 7 播放ros2 bag 数据
```
cd data/ros2_bag_data/ 
ros2 bag play rosbag2_2025_07_14-20_23_11_move/ --clock
```

## Step 8 初始化位置

回放数据并初始化位置的方法请见视频，遇到报错请按照最下面的描述解决。一旦开始播放数据，请快速在rviz上初始化，不然因为数据播放，车辆位置移动，可能导致初始化失败。

[![autoware使用ros2 bag数据定位的操作流程](https://bb-embed.zjffun.com/embed?v=BV1qMuHzfEEa)](https://player.bilibili.com/player.html?bvid=BV1qMuHzfEEa&page=1)

报错解决方法

1）报错“[autoware_ndt_scan_matcher_node-6] [INFO] [1752573537.226621404] [localization.pose_estimator.ndt_scan_matcher]: Mismatch between pose timestamp and current timestamp”  时间戳相关问题，下面三个问题，通过在三个文件中增加 use_sim_time 解决，报错和修改程序如下图。
![alt text](<docs/Screenshot from 2025-07-15 18-03-03.png>)
![alt text](<docs/Screenshot from 2025-07-15 19-41-11.png>) 
![alt text](<docs/Screenshot from 2025-07-15 19-41-52.png>) 
![alt text](<docs/Screenshot from 2025-07-15 19-42-21.png>) 
![alt text](<docs/Screenshot from 2025-07-15 19-42-31.png>) 
![alt text](<docs/Screenshot from 2025-07-15 19-42-51.png>)