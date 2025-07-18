# localization+planner=controller 调试日志，从零开始

```
ros2 topic pub --rate 10 /vehicle/status/steering_status autoware_vehicle_msgs/msg/SteeringReport '{
  "stamp": {
    "sec": '"$(date +%s)"',
    "nanosec": 0
  },
  "steering_tire_angle": 0.0
}'
```
```
ros2 topic pub --rate 10 /vehicle/status/velocity_status autoware_vehicle_msgs/msg/VelocityReport '{
  "header": {
    "stamp": {
      "sec": '"$(date +%s)"',
      "nanosec": 0
    },
    "frame_id": "base_link"
  },
  "longitudinal_velocity": 0.0,
  "lateral_velocity": 0.0,
  "heading_rate": 0.0
}'
```
```
ros2 launch autoware_launch planning_simulator.launch.xml map_path:=/home/libpet/autoware_map/sample-map-planning vehicle_model:=aps_vehicle sensor_model:=aps_sensor_kit
```