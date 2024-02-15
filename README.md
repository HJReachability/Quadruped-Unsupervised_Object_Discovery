# Unsupervised Object Discovery via Interaction

Developed an LLM-aware computer vision algorithm - dependent on physically probing the built environment - equipping a quadruped unmanned ground vehicle (UGV) for unsupervised object detection.

<div align="center">
  <img src="media/read_me.gif" alt="Description">
</div>


</br>

To view final results:
- [Project Website](https://sites.google.com/berkeley.edu/unsupervised-object-discovery/unsupervised-object-discovery-via-interaction)
- [Presenatation Deck](https://docs.google.com/presentation/d/1bJXGHLaNxGCH2Xnr3C20kdvZxDNgF2fkvTv9KjHSBMs/edit?usp=sharing)


---
### Dependencies

This repo contains the forked versions of the following repos:
- https://github.com/alonrot/unitree_ros_to_real.git
- https://github.com/alonrot/unitree_legged_sdk_from_inside_robot.git

Specficially the public branch of both.
This code would not be possible without the amazing work of alonrot, and his [documentation](https://catkin-denim-4f0.notion.site/Go1-Setup-Simple-Walking-Test-0e0e9ae4ed074a53b2bb31e62ac6f73e)


Since both repos have to be in the same ROS workspace to move the robot, our team found it easier to combine into a single repo

---

Before running the experiment, make sure to:
- copy the files from src/pi_files to the Raspberry Pi
- copy the files from src/nano_files to the main Jetson Nano (192.168.123.13)

---

### Running on Go1

1. Connect to the unitree Wi-Fi

```
ssh pi@192.168.12.1	<pwd: 123>
```

2. Connect to the Raspberry Pi and launch the Relay Node

```
python camera1node.py
```

3. On an external computer, launch the object and goal detection nodes (this assumes the camera used for AR tag tracking is already running)

Note: depending on the camera used for AR tag tracking, parameters in src/perception/launch/ar_track.launch might need to be ajusted

```
# Object detection
rosrun perception object_detector_pc.py

# Goal detection
roslaunch perception ar_track.launch

rosrun perception get_goal1_transform.py ar_tag_1

rosrun perception get_goal1_transform.py ar_tag_2

rosrun perception goal_detector.py

```

4. Still on the external computer, run the main ROS node

```
rosrun plannedctrl main_node.py
```

