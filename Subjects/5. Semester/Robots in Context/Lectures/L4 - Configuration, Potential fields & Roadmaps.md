
---
**Date:** 2026-09-22

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[weekly4_E26.pdf]]
[[RIC_4_Roadmaps_E26.pdf]]
[[RIC_4_PotentialFields_E26.pdf]]
[[RIC_4_config_E26.pdf]]
[[RIC_PE_GVD_E26.pdf]]


# Topics


# Notes

```bash
cd ~/ros2_ws
colcon build --packages-select brushfire_interfaces brushfire_pkg my_map_pkg

ros2 run my_map_pkg map_publisher # Publish white/black map as 0/100 occupancy grid
ros2 run brushfire_pkg brushfire_node # Run algorithm to generat brushfire
ros2 run brushfire_pkg colorizer_node # Colorize in HSV red to blue color range

# See visualized brushfire in rqt
ros2 run rqt_image_view rqt_image_view
```

## Example of brushfired map (NO GVD)
![[map1-brushfired.png|680]]

---
#lecture 