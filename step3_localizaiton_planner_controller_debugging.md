# localization+planner+controller 调试日志

complete step1_autoware_dependency_install_and_initial_run and step2_localizaiton_debugging

## step 1 download source code 

download code 

```
git clone https://github.com/libpet-co/autoware.APS.git
```
![alt text](docs/image.png)

## step 2 download testing ros2 bag data and map data

ros2 bag data include imu data vehicle interface data
```
mkdir ros2_bag_data
gdown -O ros2_bag_data/rosbag2_2025_07_21-14_12_57.zip https://drive.google.com/uc?id=1gdhUmAzXyBWIGrEAqnjXgw9N4H-alEqG
unzip -d ros2_bag_data rosbag2_2025_07_21-14_12_57.zip
```
download sample map data

```
mkdir test_map
gdown -O test_map/sample-map-planning-APS.zip https://drive.google.com/uc?id=19PaxactEaybAZfU5lb4TlHDOIGFgKzBc
unzip -d test_map/ test_map/sample-map-planning-APS.zip
```
download vehicle model data 
```
gdown -O src/launcher/autoware_launch_APS/vehicle/aps_vehicle_launch/aps_vehicle_description/mesh/aps2.dae  'https://drive.google.com/uc?id=1JFPvC
hA3dt0KyEM8-l4DqiAY18JekRlM'
```
## step 3 compile

compile after complete step2 because some data tranfer nedd to install directory

```
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release
```
## step 4 change params 

1.change use_sim_time

need to change params "use_sim_time = true" , if you want to use ros2 bag data , if run online on real car "use_sim_time = false"  

![alt text](<docs/Screenshot from 2025-07-22 20-38-17.png>)

2.change imu topic name 

find and replace imu topic name 

![alt text](docs/change_imu_topic.png)

3.change twist frome vehicle interface topic name 

![alt text](docs/change_twist_name.png)

4.change gnss enabled = false

![alt text](docs/change_gnss_enabled.png)

## step 5 source and launch

you need change the path of the map data acorrding your path

```
source install/setup.bash
ros2 launch autoware_launch autoware.launch.xml map_path:=/home/frank/test_map/sample-map-planning-APS vehicle_model:=aps_vehicle sensor_model:=ap
s_sensor_kit
```