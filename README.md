# Steps to reproduce:
## With move_base
1. Clone in workspace
2. `roslaunch teb_local_planner_tutorials robot_diff_drive_in_stage.launch`
3. Call the `move_base` action (or the simple goal, or use Rviz tool) with a target_pose of (0,0,0) and it crashes. To call the action, I use `rosrun actionlib axclient.py /move_base` with:
```
target_pose: 
  header: 
    seq: 0
    stamp: 
      secs: 0
      nsecs:         0
    frame_id: 'map'
  pose: 
    position: 
      x: 0.0
      y: 0.0
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
```

## With move_base_flex
1. Clone in workspace
2. `roslaunch teb_local_planner_tutorials robot_diff_drive_mbf_in_stage.launch`
3. Call the `get_path` action with a target_pose of (0,0,0) and it crashes. To call the action, I use `rosrun actionlib axclient.py /move_base/get_path` with:
```
use_start_pose: False
start_pose: 
  header: 
    seq: 0
    stamp: 
      secs: 0
      nsecs:         0
    frame_id: ''
  pose: 
    position: 
      x: 0.0
      y: 0.0
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 0.0
target_pose: 
  header: 
    seq: 0
    stamp: 
      secs: 0
      nsecs:         0
    frame_id: 'map'
  pose: 
    position: 
      x: 0.0
      y: 0.0
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
tolerance: 0.0
planner: ''
concurrency_slot: 0
```
 
I had to remove the border of the map as the issue seems to happen only with empty cells. Also I suspected the outlineMap parameter recently merged, see https://github.com/ros-planning/navigation/pull/926,  to play a role (as the costmap is not outlined at initialization), so I disabled it ( `<param name="GlobalPlanner/outline_map" value="false" />`). But the crash happens also without the outline.

