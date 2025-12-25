#  MuJoCo MPC 汽⻋仪表盘项⽬

- **学号**: 232011123
- **姓名**: 朱志立
- **班级**: 计科2303班
- **完成日期**: 2025年12月25日

## 项目概述

本项目旨在基于MuJoCo物理引擎和MPC（模型预测控制）实现一个汽车仪表盘可视化系统。通过将物理仿真、控制算法和图形界面相结合，展示车辆在虚拟环境中的运行状态，并实时显示关键数据。

**核心目标**：让小车在MuJoCo仿真环境中成功运行，并建立基础的仪表盘显示框架。

## 环境要求

### 系统环境

- **操作系统**: Ubuntu 22.04 LTS（推荐）
- **编译器**: gcc 11.3.0 或更高版本
- **CMake**: 3.22.1 或更高版本
- **显卡**: 支持OpenGL 3.3+

### 依赖库

bash

```
# 安装必要依赖
sudo apt update
sudo apt install -y \
    build-essential \
    cmake \
    git \
    libgl1-mesa-dev \
    libglfw3-dev \
    libglew-dev \
    libeigen3-dev \
    libopenblas-dev
```



## 编译和运行

### 编译步骤

bash

```
# 1. 克隆项目（如果已有则跳过）
cd ~
git clone https://github.com/google-deepmind/mujoco_mpc.git
cd mujoco_mpc

# 2. 创建编译目录
mkdir -p build && cd build

# 3. 配置项目
cmake .. -DCMAKE_BUILD_TYPE=Release

# 4. 开始编译（使用4个线程加速）
cmake --build . -j4

# 5. 编译完成后，可执行文件在 build/bin/ 目录
ls bin/
```



### 运行程序

bash

```
# 运行默认场景
./bin/mjpc

# 运行自定义汽车场景
./bin/mjpc --mjcf=../mjpc/tasks/car/car_simple.xml
```



## 功能说明

### 已实现功能

- **环境配置**：成功搭建MuJoCo MPC开发环境
- **基础场景**：能够加载和运行车辆场景
- **物理仿真**：实现车辆在虚拟环境中的物理运动
- **用户控制**：支持通过键盘控制车辆移动
- **基础数据显示**：在控制台输出车辆基本状态信息

### 当前进展

- **速度表**：基础框架已完成，需要完善图形显示
- **转速表**：数据获取已实现，需要添加可视化
- **数字显示**：油量、温度等数据的显示逻辑已完成
- **小地图**：未实现（计划中）

### 已完成的"跑起来"功能

1. **车辆模型加载**：成功创建包含车身、车轮、关节的完整车辆模型
2. **物理仿真运行**：车辆能够响应物理引擎计算，实现加速、转向等动作
3. **用户交互控制**：
   - `W/A/S/D` 或方向键控制车辆移动
   - 鼠标控制视角旋转
   - 实时物理反馈

## 项目结构

text

```
mujoco_mpc/
├── mjpc/                    # 主程序目录
│   ├── app.cc              # 应用程序主逻辑
│   ├── simulate.cc         # 仿真循环
│   ├── render.cc           # 渲染代码
│   └── tasks/              # 任务场景
│       └── car/            # 汽车场景
│           └── car_simple.xml  # 简单车辆模型
├── build/                  # 编译输出目录
│   └── bin/               # 可执行文件
└── README.md              # 项目说明文档
```



## 使用说明

### 1. 启动程序

bash

```
cd ~/mujoco_mpc/build
./bin/mjpc
```



### 2. 控制车辆

- **W/↑**：加速前进
- **S/↓**：减速/后退
- **A/←**：左转
- **D/→**：右转
- **鼠标拖动**：旋转视角
- **鼠标滚轮**：缩放视角
- **ESC**：退出程序

### 3. 查看数据

程序运行时会在终端输出实时车辆状态：

text

```
位置: (x, y, z)
速度: 0.0 m/s
加速度: (ax, ay, az)
运行时间: 00:00:00
```



## 常见问题

### Q1: 编译时出现"找不到mujoco.h"错误

bash

```
# 设置库路径
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/mujoco_mpc/build/lib
```



### Q2: 运行后窗口空白

bash

```
# 检查显卡驱动
glxinfo | grep "OpenGL version"
# 如果没有glxinfo，先安装
sudo apt install mesa-utils
```



### Q3: 无法加载场景文件

bash

```
# 检查文件路径是否正确
ls ../mjpc/tasks/car/car_simple.xml
# 确保文件存在且格式正确
```



## 开发计划

### 近期目标（1-2周）

1. 完成速度表的图形化显示
2. 实现转速表的基本框架
3. 添加简单的数字信息显示

### 中期目标（3-4周）

1. 完善仪表盘UI设计
2. 实现数据实时更新机制
3. 添加更多车辆状态显示

### 远期目标

1. 实现完整的汽车仪表盘系统
2. 添加高级功能（小地图、导航等）
3. 优化性能和视觉效果

## 技术特点

### 物理引擎

- **MuJoCo**：高性能多关节动力学仿真引擎
- **真实物理模拟**：重力、碰撞、摩擦力等
- **实时计算**：每秒数千个仿真时间步

### 控制算法

- **MPC（模型预测控制）**：先进的控制算法
- **实时优化**：基于模型预测进行控制决策
- **约束处理**：自动处理系统约束

### 图形界面

- **OpenGL渲染**：高性能图形显示
- **实时更新**：数据与显示同步
- **跨平台支持**：支持多种操作系统

## 学习收获

通过本项目，我已经掌握了：

1. **MuJoCo物理引擎**的基本使用方法
2. **C++大型项目**的编译和调试技巧
3. **Ubuntu开发环境**的配置和管理
4. **物理仿真**与**图形显示**的结合方法

虽然仪表盘的完整功能尚未实现，但已经完成了最核心的"让小车跑起来"目标，为后续开发奠定了坚实基础。

## 参考资料

1. [MuJoCo官方文档](https://mujoco.readthedocs.io/)
2. [MuJoCo MPC GitHub仓库](https://github.com/google-deepmind/mujoco_mpc)
3. [OpenGL学习指南](https://learnopengl-cn.github.io/)
4. [CMake入门教程](https://cmake.org/cmake/help/latest/guide/tutorial/)

## 联系方式

- **姓名**: 朱志立

- **学号**: 232011123

- **班级**: 计科2303班

  