# SAM Bot Autonomous Navigation & YOLOv8 Object Detection (ROS2)

## Overview

This project enables a SAM bot robot to map its environment using SLAM, autonomously navigate using Nav2, and perform real-time object detection (cans, cardboard boxes, cones) using a YOLOv8-based pipeline. All nodes run in ROS2 and integrate both navigation and detection for a true mobile robotics experiment.

---

## Repository Structure

- `sam_bot_description/`  
  Robot URDF, launch, and config files for Nav2 and SLAM

- `yolov8_ros/`  
  ROS2 Python package for YOLOv8 inference, tracking, debug, and 3D detection

- `star_navigation/`  
  Custom scripts for starting/controlling navigation missions

- `ObjectDetection.ipynb`  
  Jupyter notebook for training your own YOLOv8 model (Roboflow integration)


---

## Features

- **SLAM Mapping:** Build a map using ROS2 SLAM toolbox.
- **Autonomous Navigation:** Plan paths and navigate from any start/goal using Nav2.
- **Real-Time Object Detection:** YOLOv8 node detects target objects live during robot operation.
- **Model Training Pipeline:** Annotate and train your dataset in Roboflow/YOLOv8, then deploy in ROS2.
- **Custom Scripts:** Trigger navigation, control robot, enhance operation.

---

## Example Workflow & Commands

### 1. Map Creation with SLAM

```bash
ros2 launch slam_toolbox online_async_launch.py
```
Drive the robot to explore the environment and save the map afterward.
text

### 2. Localization

ros2 launch nav2_bringup localization_launch.py
map:=two_rooms_map2.yaml
params_file:=src/sam_bot_description/config/nav2_params.yaml


### 3. Autonomous Navigation

ros2 launch nav2_bringup navigation_launch.py
params_file:=src/sam_bot_description/config/nav2_params.yaml
use_sim_time:=true
map_subscribe_transient_local:=true

ros2 service call /start_navigation sam_bot_description/StartNavigation "{start: true}"

text

### 4. Manual Teleoperation (Optional)

ros2 run teleop_twist_keyboard teleop_twist_keyboard

text

### 5. Display Robot in RViz

ros2 launch sam_bot_description display.launch.py

text

### 6. Custom Navigation Script

ros2 run star_navigation star_nav

text

### 7. Launch YOLOv8 Object Detection

ros2 launch yolov8_bringup yolov8.launch.py

text

### 8. (Optional) Train Your Own YOLOv8 Detector

- Annotate data with Roboflow.
- Use `ObjectDetection.ipynb` for training.
- Export trained weights (.pt) and place them for YOLOv8 ROS node usage.

---

## Requirements

- ROS2 Foxy/Humble or compatible
- Python 3.8+
- Nav2, SLAM Toolbox, teleop_twist_keyboard
- YOLOv8 (Ultralytics), yolov8_ros, cv_bridge
- Jupyter notebooks (for model training)
- Roboflow account (for data annotation/export)

---

## Author

David Furtado

---

## License

See repository files for code and model licensing details (most code is under GPL-3 or MIT).
