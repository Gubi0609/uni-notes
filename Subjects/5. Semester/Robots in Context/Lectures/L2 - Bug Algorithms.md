
---
**Date:** 2026-09-08

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[weekly2_E26.pdf]]
[[RIC_2_Bug_E26.pdf]]

# Topics


# Notes
# ROS2 Workflow Guide: From Zero to a Custom Node

## 1. Core Concepts (read this first)

- **Workspace**: a folder (e.g. `~/ros2_ws`) that holds all your ROS2 packages. Just a folder, name doesn't matter, but convention is `something_ws`.
- **Package**: a folder inside `workspace/src/` containing one unit of ROS2 code (your Python files, config, metadata).
- **Node**: a running program that talks to other nodes via topics/services. One Python script = usually one node.
- **Build (`colcon build`)**: compiles/copies your package from `src/` into `install/`, and registers any commands you defined.
- **Source (`source install/setup.bash`)**: tells your *current terminal* where to find the newly built stuff. This does NOT persist across terminals — every new terminal needs to source both:
  1. ROS2 itself: `source /opt/ros/<distro>/setup.bash`
  2. Your workspace: `source ~/ros2_ws/install/setup.bash`

> [!warning] Golden rule: **rebuild → re-source**. If you change code inside `src/`, you must `colcon build` again and re-source before `ros2 run` will see the changes (for pure Python packages, sometimes edits to already-installed files take effect without rebuilding, but don't rely on it — just rebuild).

---

## 2. Creating a Workspace + Package

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python my_pkg_name --dependencies rclpy nav_msgs
````

This generates:

```
my_pkg_name/
├── my_pkg_name/          ← your actual Python code goes in here
│   └── __init__.py
├── package.xml           ← metadata (name, deps) — usually don't need to touch
├── setup.py               ← IMPORTANT: this is where you register runnable nodes
├── setup.cfg
└── resource/
    └── my_pkg_name        ← empty marker file, required, don't delete
```

Note: the outer folder and inner folder have the _same name_ — that's normal, not a mistake.

You can safely add extra folders inside the inner Python folder for your own files, e.g. a `maps/` folder for data files.

---

## 3. Writing a Node and Registering It

1. Put your script inside the **inner** package folder: `~/ros2_ws/src/my_pkg_name/my_pkg_name/my_node.py`
    
2. Your script needs a `main()` function and the standard rclpy boilerplate:
    

```python
import rclpy
from rclpy.node import Node

class MyNode(Node):
    def __init__(self):
        super().__init__('my_node')
        # subscriptions, publishers, timers go here

def main():
    rclpy.init()
    node = MyNode()
    rclpy.spin(node)

if __name__ == '__main__':
    main()
```

3. Open `setup.py` (the **outer** one, package root) and register the node under `entry_points`:

```python
entry_points={
    'console_scripts': [
        'my_node = my_pkg_name.my_node:main',
    ],
},
```

How to read that line: `command_name = python_module_path:function_to_call`

- `my_node` → what you'll type after `ros2 run my_pkg_name`
- `my_pkg_name.my_node` → the file `my_node.py` inside the `my_pkg_name` folder
- `:main` → the function inside that file to call when the node starts

---

## 4. Build and Run

```bash
cd ~/ros2_ws
colcon build --packages-select my_pkg_name
source ~/ros2_ws/install/setup.bash
ros2 run my_pkg_name my_node
```

- `colcon build` with `--packages-select` only rebuilds that one package (faster than rebuilding everything).
	- Can be used to rebuild if chances are made.
- No terminal output after `ros2 run` is often _good_ — it means the node is idle/waiting, not crashed. Check with `ros2 topic list` / `ros2 topic echo` in a second terminal.
- Common errors:
    - `Package 'my_pkg_name' not found` → forgot to source, or sourced the wrong terminal.
    - Python traceback → actual bug in your script, read it top to bottom, the last line is usually the real error.

> [!warning] Remember to always source ros when running ros commands in a new terminal window
> ```bash
> source /opt/ros/jazzy/setup.bash
> ```

---

## 5. Debugging / Verifying a Running Node

In a **second terminal** (source both ROS2 and workspace again — every terminal needs it fresh):

```bash
ros2 topic list                 # see all active topics
ros2 topic echo /topic_name --once   # see one message
ros2 topic echo /topic_name --once --field data | tr -d '[],' | tr ' ' '\n' | sort | uniq -c
                                 # ^ quick way to sanity-check a big numeric array
                                 #   (e.g. confirming a map has both 0s and 100s, not all one value)
```

---

## 6. Turning an Image into a Map (`OccupancyGrid`) — Without `nav2_map_server`

**Why:** RViz2 doesn't display images directly — it visualizes a `nav_msgs/OccupancyGrid` message on a topic (conventionally `/map`). The standard tool for this is `nav2_map_server`, but if that's off-limits for your exercise, you can publish the same message type yourself from a small custom node.

### 6.1 Prepare the image

- Keep it simple black/white: **white = free space, black = obstacle** (this is the standard convention, `negate: 0`).
- Any format PIL can open works (`.png`, `.pgm`, etc).

### 6.2 Write a `map.yaml` describing it

```yaml
image: map.png
resolution: 0.05          # meters per pixel — YOU choose this based on desired real-world scale
origin: [0.0, 0.0, 0.0]    # [x, y, yaw] of the image's bottom-left pixel, in map coordinates
negate: 0                  # 0 = white is free, black is occupied (matches most hand-made maps)
occupied_thresh: 0.65      # grayscale fraction above which a pixel counts as occupied
free_thresh: 0.25          # grayscale fraction below which a pixel counts as free
```

Keep `map.yaml` and the image file in the same folder.

### 6.3 Custom publisher node (in place of `map_server`)

```python
import rclpy
from rclpy.node import Node
from nav_msgs.msg import OccupancyGrid
from PIL import Image
import numpy as np
import yaml
import os

class MapPublisher(Node):
    def __init__(self):
        super().__init__('map_publisher')
        self.pub = self.create_publisher(OccupancyGrid, '/map', 10)

        yaml_path = '/absolute/path/to/map.yaml'
        with open(yaml_path, 'r') as f:
            meta = yaml.safe_load(f)

        image_path = os.path.join(os.path.dirname(yaml_path), meta['image'])
        img = Image.open(image_path).convert('L')  # grayscale
        arr = np.array(img)

        resolution = meta['resolution']
        origin = meta['origin']
        negate = meta.get('negate', 0)
        occ_thresh = meta.get('occupied_thresh', 0.65)

        grid = OccupancyGrid()
        grid.header.frame_id = 'map'
        grid.info.resolution = resolution
        grid.info.width = arr.shape[1]
        grid.info.height = arr.shape[0]
        grid.info.origin.position.x = origin[0]
        grid.info.origin.position.y = origin[1]

        # image row 0 is the TOP in image coords, but map row 0 should be the BOTTOM
        flipped = np.flipud(arr)
        normalized = flipped / 255.0
        if negate:
            normalized = 1.0 - normalized
        occ = np.where(normalized < (1.0 - occ_thresh), 100, 0).astype(np.int8)
        grid.data = occ.flatten().tolist()

        self.grid = grid
        self.timer = self.create_timer(1.0, self.publish_map)

    def publish_map(self):
        self.grid.header.stamp = self.get_clock().now().to_msg()
        self.pub.publish(self.grid)

def main():
    rclpy.init()
    node = MapPublisher()
    rclpy.spin(node)

if __name__ == '__main__':
    main()
```

Register it in `setup.py` (`entry_points`) exactly as in section 3, build, source, run — same pattern every time.

### 6.4 Viewing it in RViz2

```bash
rviz2
```

1. **Global Options → Fixed Frame** → set to `map`
2. **Add → By display type → Map** → OK
3. Expand the new Map entry → **Topic** → `/map`

If you see a `GLSL120/indexed_8bit_image` shader error in the terminal but the map still renders — that's a harmless GPU/driver rendering quirk, safe to ignore. Try toggling the Map display's **Color Scheme** (map/costmap) if it bothers you.

---

## 7. Installing Python Packages Without `pip --break-system-packages`

Order of preference:

1. Check if it's already installed: `python3 -c "import yaml"` (swap module name)
2. Install via apt (matches what ROS2 itself uses): `sudo apt install python3-yaml` (or `python3-pil` for Pillow, etc.)
3. Virtual environment, only if apt isn't an option — adds complexity with ROS2's Python path, so avoid unless necessary.

---

## 8. Quick Command Cheat-Sheet

|Task|Command|
|---|---|
|Create workspace + pkg|`mkdir -p ws/src && cd ws/src && ros2 pkg create --build-type ament_python pkg_name --dependencies rclpy`|
|Build one package|`colcon build --packages-select pkg_name`|
|Source workspace|`source install/setup.bash`|
|Run a node|`ros2 run pkg_name node_command`|
|List topics|`ros2 topic list`|
|Inspect one message|`ros2 topic echo /topic --once`|
|Open RViz2|`rviz2`|

---
#lecture 