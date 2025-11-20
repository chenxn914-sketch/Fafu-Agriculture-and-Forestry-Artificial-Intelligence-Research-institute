# Fafu-Agriculture-and-Forestry-Artificial-Intelligence-Research-institute
基于Ubuntu22.04 ros2 humble版本的2d雷达车，具备自主避障导航功能。
按照下方使用说明中流程可正常使用本项目代码

## 使用说明

本说明介绍如何使用本项目中的启动雷达建图、导航的功能
需注意雷达和驱动文件的参数是否与正在使用型号是否相同
### 1. 构建与环境设置

首次或更新源码后进行编译，并在当前终端加载环境：

1、 在终端中切换到所在的工作空间，2D_car_ws的存放位置。
```
cd /home/jetson/2D_car_ws 
```
2、对工作空间进行编译
```
colcon build --symlink-install
```

<img width="930" height="510" alt="image" src="https://github.com/user-attachments/assets/355bf019-0f58-456f-87ee-9c5d667ba428" />


3、然后加载工作空间(新开终端的时候记得都要重新进入工作空间的文件夹并进行加载)
```
source /home/jetson/2D_car_ws/install/setup.bash
```
<img width="894" height="516" alt="image" src="https://github.com/user-attachments/assets/4b51861f-6c4b-430d-9ce1-48625f0424b5" />


### 2. 雷达接口、小车接口权限

再打开一个终端，给予雷达接口、小车串口的权限
如果串口号不一样，通过ls /dev/tty*来进行查询
```bash
sudo chmod 666 /dev/ttyUSB0   #这个是雷达接口

sudo chmod 666 /dev/ttyACM0  #这个是底盘小车的接口
```


---

 

### 3. 启动建图
1）开始建图
```bash
ros2 launch turn_on_dlrobot_robot gmapping_demo.launch.py
```

<img width="903" height="501" alt="image" src="https://github.com/user-attachments/assets/918e4efc-1083-4e0e-a709-08ece578d2c1" />


2）启动rviz可视化
```bash
rviz2 #(另外开一个终端)
```
<img width="1461" height="944" alt="image" src="https://github.com/user-attachments/assets/a0158a30-b739-4c5d-8541-4de8d7192fe7" />


3）保存地图(另外开一个终端)

```bash
ros2 run nav2_map_server map_saver_cli -f /home/jetson/1_ws/src/turn_on_dlrobot_robot/maps/test_map_210
```
# /home/jetson/1_ws/src/turn_on_dlrobot_robot/maps/test_map_210 这个为保存地图的绝对路径。
test_map_210是地图文件的名称，可自命名。
---
<img width="903" height="330" alt="image" src="https://github.com/user-attachments/assets/35016f19-f6b3-494b-b159-e2fe333c721f" />
<img width="1221" height="636" alt="image" src="https://github.com/user-attachments/assets/76a6516f-f111-40ea-bb1d-8e79fdd534f4" />


### 4. 开始导航

```bash
ros2 launch turn_on_dlrobot_robot navigation_demo.launch.py map:=//home/jetson/1_ws/src/turn_on_dlrobot_robot/maps/newest1_map_214.yaml
```
# map:=这后面跟的是你保存的地图文件中里yaml文件的绝对路径
<img width="1446" height="975" alt="image" src="https://github.com/user-attachments/assets/997a63b6-1fce-4785-a4ff-d703cc897cb9" />


点击上面的2D Pose Estimate进行定位
<img width="1742" height="1005" alt="image" src="https://github.com/user-attachments/assets/f6abca01-63f1-4785-bc24-4e18494212e2" />

定位完成之后，用Nv2 Goal在地图上来选定你要导航到的目标位置

