# NAVIGATION2-STUDY

一个用于学习路径规划与控制的项目，当前聚焦于 **混合A\*** 与 **后轴反馈控制算法** 的实现与理解。

## 📁 项目结构

```
.
├── CMakeLists.txt           # 构建配置文件
├── build_x86/              # x86 构建输出
├── install_x86/            # x86 安装目录
├── cmake/                  # CMake 模块或配置
├── script_tool/            # 工具脚本
├── src/                    # 项目源代码
├── resource/               # 配置文件、地图等资源
├── third_party/            # 第三方库（如 jsoncpp）
├── util/                   # 工具类或辅助函数
├── .clang-format           # 代码格式化配置
├── .gitignore              # Git 忽略文件
├── README.md               # 项目说明文档
├── make.sh                 # 快速构建脚本
```

## 🚀 安装与使用

### 支持的平台
ubuntu22.04

### 安装依赖

```
sudo apt install cmake
sudo apt install g++
sudo apt install gdb
sudo apt install ros-humble-desktop
sudo apt install gazebo
sudo apt install ros-humble-xacro
sudo apt install python3-colcon-common-extensions
```
### ROS包的系统级依赖项

使用rosdepc进行依赖的安装，rosdepc指令找不到可以先运行下面的一键安装命令，选择一键配置rosdep即可。
```
wget http://fishros.com/install -O fishros && . fishros
```
接着在fishbot_ws下运行下面这个命令进行依赖的安装。

rosdepc 是小鱼制作的国内版rosdep，是一个用于安装依赖的工具。该工具的安装可以采用一键安装进行，选项编号为3。安装完成后运行一次rodepc update即可使用。
```
rosdepc install -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO -y
```

### 编译

cartographe包编译
```
colcon build --packages-up-to cartographer_ros
```

navigation2包编译，建议使用单线程编译
```
colcon build --parallel-workers 1 --packages-up-to navigation2
```


### 运行
#### 加载安装脚本
```
source ./install/setup.bash
```
#### 生成urdf文件
```
xacro src/akm_bringup/urdf/model.xacro >src/akm_bringup/urdf/model.urdf
```
#### 编译bringup文件
```
colcon build --packages-up-to  akm_bringup
```
#### 加载安装脚本
```
source ./install/setup.bash
```
#### 运行gazebo仿真
```
ros2 launch akm_bringup gazebo_launch.py
```
#### 运行nav2导航
```
ros2 launch akm_bringup navigation2_launch.py
```




### 脚本参数
- `build` 编译，默认参数
- `run`: 运行，依赖**install_x86**文件夹
- `pack`: 打包产物，生成一个`.tar.gz`后缀的压缩包
- `clear`: 清除产物，比如**build_x86**
- `launch`: 编译后直接运行

## 🔧 配置选项
工程支持跨平台和多架构等功能配置，通过更改`make.sh`中的相关参数来实现，参数会通过cmake脚本处理为cmake参数，一些参数还会通过宏的方式以影响工程中的编译选项，以此来适配不同的平台、架构、版本等等。所有可配置可参考build_xx文件下的build.properties.local。  以下是一些当前常见的配置选项，位于脚本的顶端：
- `project_name`="nav-easy"
- `platform`="linux"
- `architecture`="x86"
- `build_type`="debug"


## 🚗 功能示例
- 待更新

## ⚠️ 注意事项
- 待更新

## 📝 更新日志

| 日期       | 类型     | 内容说明                                               |
|------------|-------|--------------------------------------------------------|
| 2025-04-15 | 创建 | 第一版本                                |


