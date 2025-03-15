#  组备赛规划
## 一、小组信息及分工
- 曹彩杰 主要负责软件方向
- 吕思涵 主要负责硬件方向
- 张晋嘉
### 成员技术栈
- 曹彩杰

- 吕思涵
## 二、方向选择
### 2021年F题智能送药小车
#### 1. 整体硬件方案设计 根据题目要求，设计出了硬件系统。除了车身结构，控制系统分为 7 个基本 模块，包括主控、视觉模块、驱动模块、药物放入检测模块、灯光显示模块、通信模块、电源模块。
#### 2. 车身结构选择 
- 方案一：采用传统四轮车模，将摄像头用纤维杆固定在车头顶端，车身上放置主控以及各模块。
- 方案二：采用抽屉式结构，将物品沿 Z 轴放置于平台之上，摄像头放置到 可调机械臂上用于视野变动。 题目中要求小车长×宽×高不大于25cm×20cm×25cm 且考虑到在弯道处尽量不压线，传统四轮车模难以完成上述功能，因此团队成员摒弃传统车模设定，自定义一款直径 15cm 的圆盘小车，采用三层抽屉式机械机构，分别放置主控系 统、供电系统以及药物。 最终选择方案二的车架结构。 
#### 3. 视觉模块 
##### （1）数字识别方案选择 
- 方案一：采用图像模板匹配进行学习，将数字以 1 张图片的形式保存下来并与赛道上的数字进行比较判别。 
- 方案二：采用神经网络算法，对不同光线，视角下的数字照片训练，在 Mv 中调用训练好的模型进行识别。 在实际测试的过程中团队发现，模板匹配方案在速度、方向、光强、高度、角度等各种因素数据特定时检测灵敏，但在实际巡线中的不确定性以及小车自身的反应速度，其模板匹配方案有一定的局限性，受外界环境的影响较大。相比上述方案，在实操中将每个数字选取不同角度的 100 张图片放入机器进行学习，并得出神经网络阵进行路面实际情况检测。使用伸进网络识别速度较快，精度明显高于模板匹配，而且受光线影响小。最终选择神经网络算法。
##### （2）循迹方案比较 
- 方案一：灰度循迹，在车头装若干灰度传感器，根据灰度传感器的返回值 调节小车左右轮速 
- 方案二：采用视觉循迹。红色是三原色之一，对彩色图像通道拆分后可以 轻松找到红色色块，而且这种巡线方式不会被黑色的跑到边界干扰。 两种方案理论上均可实现，实际测试中由于灰度传感器受光线影响较大而且 容易被跑到边界的黑线干扰，而视觉巡线基本不受光线影响，分辨率也远好于灰 度模块循迹。根据 Open Mv 返回的最大红色块坐标判断小车的偏差，并通 过 pid 算法给出电机的控制量，经检验此方案可行，且响应迅速，抗干扰能力好。 最终选择 RGB 视觉巡线。 
#### 4. 主控方案 主控选择 stm32 单片机。该单片机片上资源丰富，定时器还支持直接读取电 机编码器，一定程度上可以降低项目的工作量。相对于 51，树莓派等，32 单片 机有更复杂的中断系统，更能胜任逻辑量大的程序。 
#### 5. 驱动模块控制方案选择 首先本系统采用有刷减速电机来控制小车运动 
- 方案一：开环控制，直接用 pwm 控制电机转速 
- 方案二：采用闭环控制，读取编码器值计算电机的转速，时刻调节输出功 率让电机在不同负载下维持设定的转速。优先选择了对电机闭环控制。实际测试中，加入闭环后，小车速度会更加稳定，步长控制更加精准，小车左右转等角度不再受到重心或电池电量的 影响。
#### 6. 药物到位检测装置 由于药物重量设定在 200g 左右，团队在药物检测中使用重物阈值检测法。 实际操作中，将 200g 砝码放置于压力应变片上时会有电压改变，但检测精度不 高，在 1kg 量程左右变化，对于题目中 200g 检测并不是很灵敏，因此，将信号进行了放大，并用 ADC 采集判断。此外，加入光电传感器使判断更加可靠。
### 方向所需技术栈
- 熟练使用stm32单片机、openmv、电机驱动模块、编码器、超声波模块、红外/灰度传感器
- 会使用巡线算法、数字识别
-熟练巡线环（方向误差）、位移环（位置误差）、速度环（电机调速）三级PID
- OpenMV与STM32串口通讯
## 三、设备清单
### 1、工具
热风枪、电烙铁
### 2、硬件材料
小车底盘、电池、最小系统板stm32、电机驱动模块、openmv、陀螺仪、编码器、超声波模块、红外/灰度传感器、oled显示屏、LED指示灯
### 3、软件工具链
代码编程使用keil5，代码管理github、openmv IDE
## 四、学习计划
### 1、3.16——3.22
### 2、3.23——3.29
### 3、3.30——4.5
### 4、4.6——4.11
基本完成题目一
### 5、4.13——4.19
### 6、4.20——4.26
### 7、4.27——5.3
### 8、5.4——5.9
完美完成题目一或基本完成题目二
### 9、5.12——6.6
构建通用方案