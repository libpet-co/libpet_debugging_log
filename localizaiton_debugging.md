# localization 调试日志，从零开始

```
ros2 service call /localization/pose_twist_fusion_filter/trigger_node std_srvs/srv/SetBool "{data: true}"
ros2 topic pub --once /initialpose3d geometry_msgs/msg/PoseWithCovarianceStamped "{header: {frame_id: 'map'}, pose: {pose: {position: {x: 0.0, y: 0.0, z: 0.0}, orientation: {x: 0.0, y: 0.0, z: 0.0, w: 1.0}}, covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]}}"

ros2 topic pub --once /initialpose3d geometry_msgs/msg/PoseWithCovarianceStamped "{
  header: {
    stamp: { sec: 0, nanosec: 0 },
    frame_id: 'map'
  },
  pose: {
    pose: {
      position: { x: 0.0, y: 0.0, z: 0.0 },
      orientation: { x: 0.0, y: 0.0, z: 0.0, w: 1.0 }
    },
    covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
                 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
                 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
                 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
                 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
                 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
  }
}"
ros2 service call /localization/pose_estimator/trigger_node std_srvs/srv/SetBool "{data: true}"
```