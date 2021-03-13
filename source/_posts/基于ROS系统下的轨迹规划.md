---
title: 基于ROS系统下的轨迹规划
tags:
  - '机器人'
  - 'ROS'
date: 2020-01-7 00:00:42
updated:
categories: 机器人学院
keywords:
description: 机器人学项目设计三
top _img:
comments:
cover: https://photo.lyh.best/2021/03/14/8b0f11e316989.png
toc:
toc_number: true
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
## 概述
本次机器人学项目三要求在相应的二维平面完成点对点的运动并进行轨迹规划任务，同时在ROS平台进行机器人仿真。我们使用了二连杆机械臂来作为载体实现轨迹规划。
![image.png](http://photo.lyh.best/2021/03/14/df0c1786f3b59.png)

## 机器人建模部分
### 机器人模型思路
在第一周ROS的学习过程中，我们使用的机器人是优傲UR5机器人，因此一开始计划利用它在平面实现圆的轨迹规划如下图所示。
<table><tr>
<td><img src="http://photo.lyh.best/2021/03/14/933f4dda6f6b4.png" alt="UR机器人" title="image.png"/></td>
<td><img src="https://photo.lyh.best/2021/03/14/8b0f11e316989.png" alt="" title="image.png"/></td>
</tr></table>

在学习 ROS 功能包 Moveit 时发现，因为已经集成了轨迹规划的 moveit setup assistant和Addtimeparameterization 适配器（生成含有时间参数的运动路径），而对于我们想要加入自己的轨迹规划内容有较大阻碍。
同时，我们重新思考了项目思路，因为只需要在平面上绘制，打算利用二连杆机器人来实现轨迹规划。而在ROS中，机器人的模型是通过 URDF 文件格式实现的。 URDF 是一种标准机器人描述文件格式，使用 XML 文件描述机器人连杆（link）和关节（joint）之间的关系。建模原理是与 D-H 法类似。

### 机器人模型描述格式-URDF
URDF是在ROS系统中，对二连杆机器人进行描述的格式。
`<link>`标签（用于描述机器人刚体部分的外观和物理属性），指定连杆一和连杆二的长为1000mm，宽为50mm,高为50mm。`<joint>`标签(用于描述机器人关节的运动学属性)，在二连杆模型中，第一个 link 称为 parent link 第二个 link 称为 child link，joint 就是用来连接两个刚体 link。我们在ROS中设置的 joint 是 continuous 连续型铰链关节，绕一个轴旋转，没有最大最小值限制。`<robot>`标签是设置机器人名称的。  

### 将solidworks模型导出为URDF格式
 本次我们采用了先用 solidworks 画出二轴机器人再将其导出机器人描述的统一格式的 URDF 文件来满足我们的需求，这一步的主要流程是设计装配好的机器人模型，利用导出 URDF 的 solidworks 插件，配置好各个关节的旋转轴和坐标系，旋转限制等等即可自动生成我们需要的 URDF 格式，导出的文件夹中 meshes 文件夹里主要存放转化后的 STL 格式模型，URDF 中则是我们想要的机器人描述的 URDF 文件，launch文件夹则放置启动文件，用于一次性运行多行命令等。 
![简易二轴机器人模型](http://photo.lyh.best/2021/03/14/8853325c92d5a.png)
![配置机器人关节](http://photo.lyh.best/2021/03/14/5827ddd385d3d.png)
![配置机器人连杆](http://photo.lyh.best/2021/03/14/c4b8187c13e09.png)
![导出生成的文件夹](http://photo.lyh.best/2021/03/14/c4b8187c13e09.png)

## 轨迹规划部分

### 操作空间轨迹规划
轨迹规划的目的，是生成运动控制系统的参考输入，以确保机器手完成规划的轨迹。我们会指定一系列的参数，以描述期望的轨迹。规划是由生成一组由期望轨迹的内插函数所得到的时间序列值构成的。路径表示在关节空间或操作空间中，机械手在执行指定运动时必须跟随的点的轨迹。路径是运动的纯几何描述。轨迹则是一条指定了时间律的路径，例如在每一点的速度或加速度。
轨迹规划算法的输入包括路径描述，路径约束以及由机械手动力学施加的约束，其输出是按时间顺序给出的位置，速度和加速度的值构成的末端执行器轨迹。
我们是对机械手末端轨迹进行控制，而为了让二连杆机器人的末端执行器运动遵循操作空间用几何方法指定的路径，就有必要在同一空间规划其直接执行的轨迹，通过内插一个规定的路径点序列进行。
第二步，是通过操作空间变量得到的时间序列值，加上逆运动学的算法，实时地得到相应的关节变量值序列。
![图3.1](http://photo.lyh.best/2021/03/14/f68c3a2bedb53.png)
考虑如上图3.1的平面二连杆机器人。设$ g=（x，y，\phi）$表示末端执行器的位姿，末端坐标为$（x，y）$，建立极轴长为$ r $，极角为$ /phi $的极坐标系。这里取$ L_1 $，$ L_2 $ 。
运动学正解满足以下关系：
$$ x=L_1\cos\theta_1+L_2\cos(\theta_1+\theta_2) $$
$$ y=L_1\sin\theta_1+L_2\sin(\theta_1+\theta_2) $$
$$ \phi=\theta_1+\\theta_2  \tag{3.1} $$
$ \theta_2 $满足以下关系：
$$ r^2=x^2+y^2 $$
$$ \theta_2=\mu\pm\alpha $$
$$ \alpha=\arccos(\frac{L_1^2+L_2^2-r^2}{2L_1L_2}) \tag{3.3} $$
如果$ \alpha $不等于$ 0 $，则$ \theta_2 $有两个不同解，通过求解$ \Phi $来确定$ \theta_1 $。
$ \theta_1$ 满足以下关系：        
$$ \theta_1=\arctan2(y,x)\pm\beta $$
$$ \beta=\arccos(\frac{r^2+L_1^2-L_2^2}{2L_1r})   \tag{3.4}$$
由此可以得出需要的$ \theta_ 1$和$ \theta_2 $。
### 通过系列点的运动规划（五阶多项式）
为我们要绘制的轨迹是一个圆形，其中会有四个关键点被指定（路径点）。使用的阶数插值多项为五次多项式，它容许在路径点施加速度的连续性。对于这里的关节1和关节2的变量$ \theta_1 $和$ \theta_2 $，计算出一个由$ n-1 $连续且具有连续一阶导数的五阶多项式构成的序列所形成的函数$ S(t) $。
这里以画一个中心在$ (0.5,1) $，半径为$ 0.5 $的圆做例子，我们需要规划经过圆的四个点，分别为$ (0.5,1.5) $、$ (1,1) $、$ (0.5,0.5) $以及$ (0,1) $，我们在四个路径点指定速度为$ 0 $与加速度为零，联合六个方程求出我们关于圆的五阶多项式方程，以下展示我们规划的路径、速度曲线以及加速度曲线等。
这里规划的路径我们求出各段起始点和末端点求出其对应的五阶多项式方程，我们求出的方程如下：
$$ x_1=2.5+5t^3-7.5t^4+3t^5 $$
$$ y_1=\sqrt{(1-x_1)x_1}+1 $$
$$ x_2=16.5-60t+90t^2+65t^3+22.5t^4-3t^5 $$
$$ y_2=-\sqrt{(1-x_2)x_2}+1 $$
$$ x_3=256.5-940t+450t^2-185t^3+37.5t^4+6t^5 $$
$$ y_3=-\sqrt{(1-x_3)x_3}+1 $$
$$ x_4=1471.5+2160t+1260t^2+375t^3-52.5t^4+3t^5 $$ 
$$ y_3=-\sqrt{(1-x_4)x_4}+1 $$
![规划路径](http://photo.lyh.best/2021/03/14/2e6d81da5fa43.png)
对于我们所需要规划的速度关于时间的曲线，即将位置方程求导即可，其速度方程曲线如下，可以看到速度关于时间的函数连续且可微：
![速度方程曲线](http://photo.lyh.best/2021/03/14/ae132f3fb105f.png)
对于我们所需要规划的加速度关于时间的曲线，即将速度方程求导即可，其加速度方程如下图3.2.3，可以看到，五次多项式方程画出的圆，其加速度连续且没有突变。 
![加速度方程曲线](http://photo.lyh.best/2021/03/14/008883395e59b.png)
同理我们由公式$ \theta(t)'=(\theta_{end}-\theta_{start})\nu $得到关节一的关于时间的方程曲线，由图可知其可微，即角速度连续。
![关节1曲线](http://photo.lyh.best/2021/03/14/3008a2ef0f198.png)
关节2的曲线与关节1原理相同，这里不多加赘述。
![关节2曲线](http://photo.lyh.best/2021/03/14/870694e7b7050.png)

## ROS操作系统实现过程
### 消息传递
ROS的总体框架分为三个级别：计算图级、文件系统级、社区级。而我们这里用到的消息传递是在计算图级层，包括以下概念：节点（node）、节点管理器（parameter server）、消息（message）、主题（topic）、服务（service）、消息记录包（bag）。
1. 节点
节点是主要的计算执行进程，也可以被称为软件模块，ROS系统就是由很多节点组成的。我们此次项目设置的重要节点包括：
*	controller_node：根据逆向运动学公式，发布两个连续关节的关节状态theta1和theta2
*	joint_state_publisher：在调试和验证机器人urdf时与gui结合使用。
*	robot_state_publisher：从以上两个节点中的任何一个获取联合状态，并在机器人框架之间广播转换。
*	tf_endEffector_node：发布从基本效果到最终效果的转换，以供rviz用于对轨迹进行动画处理。
*	rviz：打开机器人可视化工具rviz。
2. 消息
节点之间是通过传送消息进行通讯的。每一个消息都是一个严格的数据结构。
3. 话题
消息以一种发布/订阅的方式传递。一个节点可以在一个给定的话题中发布消息。一个节点针对某个话题关注与订阅特定类型的数据。可能同时有多个节点发布或者订阅同一个话题的消息。此次项目涉及的话题包括：
*	joint_states：类型的消息sensor_msgs / JointState由任一发布到本主题controller_node或joint_state_publisher，并且被订阅robot_state_publisher。包含关节的角度。
*	visualization_marker：类型为visualization_msgs / Marker的消息由发行到该主题，并由tf_endEffector_node订阅rviz。
*	tf：类型的消息tf2_msgs / TFMessage被发布到这个话题robot_state_publisher，并通过订阅rviz和tf_endEffector_node。包含机器人模型移动时的tf数据。
逻辑示意图如下：
![image.png](http://photo.lyh.best/2021/03/14/3f5c003314c00.png)
其中/controller_node是控制节点，在这里可以输入我们规划的轨迹信息，比如规划的路径函数，同时，在这个节点内发布一个话题/joint_states，话题的消息类型为sensor_msgs/Jointstate、包含关节的位置、速度等数据信息，数据被下一个节点/robot_state_publisher接收。/robot_state_publisher是一个安装ROS系统后自带的节点，这一个节点会将从话题/joint_states读取robot_description参数及关节位置，并计算出正向运动学结果，并将坐标结果P(x,y,z)、R(y,p,r)发布到话题/tf及话题/tf_static中。下一个节点/tf_endEffector_node可以接收/tf（或者/tf_static）中的数据，接收后将数据通过话题/visualization_marker传输到Rviz中，实现轨迹的可视化。

### 可视化工具
Rviz是一款三维可视化工具，可以通过图形化的方式，实时显示机器人的运动状态。
最终机器人规划的可视化效果（俯视图）如下图:
![image.png](http://photo.lyh.best/2021/03/14/1b22a90f08082.png)
其中x轴为红色，指向当前视图右侧，y轴为绿色，指向当前视图上侧，z轴为蓝色，指向当前视图外侧。


## 存在问题
我们用五次多项式规划出的圆轨迹可分为四段，可以理解为单位圆的四个象限。对于我们可视化出来的轨迹，我们发现了一个问题：解五次多项式方程时，期望在每一段轨迹的起始点及末端点的速度为零。但实际上可视化的时候，在轨迹上并没有出现想象中四段一样的情况，而是每两段的情况类似：缓慢启动——达到最大值——缓慢停止、缓慢启动——达到最大值——继续下一段运动。
我们直接套用模板造成的结果就是不能够知道初始化时刻机器人的位置，系统时间是不断增加的，只能从我们运行程序的时刻开始，但该时刻时间并不一定为0
我们也尝试了梯形曲线规划的方式，但是生成的曲线只有(0，1)时间段内的一小段时刻

## 附录
#### 机器人模型URDF
```xml
<robot name="2link_robot">#机器人名称
	<material name="black">可视化组件的材料，可以在link标签外，但必须在robot标签内，需要引用link的名字。
		<color rgba="0 0 0 0.7"/>材料颜色，由red/green/blue/alpha组成，大小范围为[0,1]
	</material>
	<material name="white">
		<color rgba="1 1 1 0.7"/>
	</material>
	<link name="base"/>名称
	<link name="arm1"><visual>连杆的可视化属性，用于指定连杆显示的形状（矩形、圆形），同一个连杆可以存在多个visual元素
			<geometry>可视化对象的类型
		<visual>
			<geometry>
        			<mesh
         			 filename="package://twolink/meshes/Link1.STL" />
			</geometry>
			<origin rpy="1.5708 0 0.1645" xyz="0 0 0.05"/>相对于连杆坐标系的几何形状坐标系，rpy表示坐标轴在RPY方向上的旋转，单位为弧度，xyz表示x,y,z方向的偏置
			<material name="black"/>
		</visual>
	</link>
	<joint name="baseHinge" type="continuous">
		<axis rpy="0 0 0" xyz="0 0 1"/>
		<parent link="base"/>
		<child link="arm1"/>
	</joint>
	<link name="arm2">
		<visual>
			<geometry>
        			<mesh
          			 filename="package://twolink/meshes/Link2.STL" />
			</geometry>
			<origin rpy="1.5708 0 2.1522" xyz="1 -0.1600 0.15"/>
			<material name="white"/>
		</visual>
	</link>
	<joint name="interArm" type="continuous">
		<axis rpy="0 0 0" xyz="0 0 1"/>
		<parent link="arm1"/>
		<child link="arm2"/>
		<origin rpy="0 0 0" xyz="1 0 0"/>
	</joint>
	<link name="endEffector"/>
	<joint name="ee_joint" type="fixed">
		<parent link="arm2"/>
		<child link="endEffector"/>
		<origin rpy="0 0 0" xyz="1 0 0"/>
	</joint>
</robot>
```

#### 主函数python代码
```python
#!/usr/bin/env python
import rospy
from sensor_msgs.msg import JointState
from math import sin, cos, acos, atan2, pi, sqrt
def desired_thetas(t, T):
    tr = t%20/T
    if tr<1:
    	xd = 0.5+5*tr**3-7.5*tr**4+3*tr**5
    	yd = sqrt((1-xd)*xd)+1
    elif tr<2:
	xd = 16.5-60*tr+90*tr**2-65*tr**3+22.5*tr**4-3*tr**5
	yd = -sqrt((1-xd)*xd)+1
    elif tr<3:
	xd = 256.5-540*tr+450*tr**2-185*tr**3+37.5*tr**4-3*tr**5
	yd = -sqrt((1-xd)*xd)+1
    else :
	xd = -1471.5+2160*tr-1260*tr**2+365*tr**3-52.5*tr**4+3*tr**5
	yd = sqrt((1-xd)*xd)+1
    l1 = rospy.get_param('~link1')    
    l2 = rospy.get_param('~link2')
    r = sqrt(xd**2 + yd**2)
    alpha = acos((l1**2 + l2**2 - (r**2))/(2*l1*l2))
    beta = acos((r**2+l1**2-l2**2)/(2*l1*r))
    theta2 = pi - alpha
    theta1 = atan2(yd, xd) - beta
return [theta1, theta2]

	#发布消息的函数名
def sender():
	#创建一个Publisher，发布名为joint_states的topic，消息类型为JointState，队列长度为10
    jspub = rospy.Publisher('joint_states', JointState, queue_size=10)
	#ROS节点初始化
    rospy.init_node('controller_node')
	#设置循环的频率
	#从controller_pub_rate里获取参数的值，将值保存到R
    R = rospy.get_param('~controller_pub_rate')
	#循环频率为R
    rate = rospy.Rate(R)
	#从period里获取参数的值，将值保存到T
    T = rospy.get_param('~period')
	#初始化JointState类型的消息
    cmd = JointState()
	#while循环
    while not rospy.is_shutdown():#这一行不需要改
		#设置JointState类型的消息header值
        cmd.header.stamp = rospy.Time.now()
		#返回当前时间，单位秒，将时间放入t内
        t = rospy.get_time()
		#设置JointState类型的消息name值
        cmd.name = ['baseHinge', 'interArm']
		#设置JointState类型的消息position值，即从上一个函数得到返回值
        cmd.position = desired_thetas(t, T)
		#发布消息
        jspub.publish(cmd)
		#按照循环频率延时
        rate.sleep()
	#主函数
if __name__ == '__main__':
    try:
        sender()
    except rospy.ROSInterruptException:
        pass
```

#### tf部分python代码
```python
#!/usr/bin/env python 
import rospy
# import math
import tf
from visualization_msgs.msg import Marker
from geometry_msgs.msg import Point
if __name__ == '__main__':
    rospy.init_node('tf_endEffector_node')
    listener = tf.TransformListener() #This will listen to the tf data later
    marker_pub = rospy.Publisher('visualization_marker', Marker, queue_size=100) 
    marker = Marker() 
    marker.id = 0
    marker.header.frame_id = 'base'
    marker.header.stamp = rospy.Time.now()
    marker.type = Marker.LINE_STRIP
    marker.ns = 'tf_endEffector_node'
    marker.action = Marker.ADD
    marker.scale.x = .01
    marker.pose.orientation.w = 1.0
    marker.color.a = 1.0
    marker.color.g = 1.0
    R = rospy.get_param('~tf_ee_pub_rate')
    rate = rospy.Rate(R)
    while not rospy.is_shutdown():
        try:
            (trans, rot) = listener.lookupTransform('base', 'endEffector', rospy.Time(0))
        except (tf.LookupException, tf.ConnectivityException, tf.ExtrapolationException):
            continue
        newpoint = Point()
        newpoint.x = trans[0]
        newpoint.y = trans[1]
        newpoint.z = trans[2]
        #if len(marker.points) > 40:
        #    marker.points.pop(0)        
        marker.points.append(newpoint)
        marker_pub.publish(marker)
        rate.sleep()
```

#### 轨迹规划matlab代码

```matlab
clear
clc
%a、b、c、d、e分别为时刻值
a=0;b=1;c=2;d=3;e=4;
A1 = [1 a a^2 a^3 a^4 a^5;... 
      1 b b^2 b^3 b^4 b^5;... 
      0 1 2*a 3*a^2 4*a^3 5*a^4;...
      0 1 2*b 3*b^2 4*b^3 5*b^4;... 
      0 0 2 6*a 12*a^2 20*a^3;...
      0 0 2 6*b 12*b^2 20*b^3];
b1 = [0.5;1;0;0;0;0];
x1 = A1\b1;
 
A2 = [1 b b^2 b^3 b^4 b^5;... 
     1 c c^2 c^3 c^4 c^5;... 
     0 1 2*b 3*b^2 4*b^3 5*b^4 ;...
     0 1 2*c 3*c^2 4*c^3 5*c^4;...
     0 0 2 6*b 12*b^2 20*b^3;...
     0 0 2 6*c 12*c^2 20*c^3];
b2 = [1;0.5;0;0;0;0];
x2 = A2\b2;
 
A3 = [1 c c^2 c^3 c^4 c^5;... 
     1 d d^2 d^3 d^4 d^5;... 
     0 1 2*c 3*c^2 4*c^3 5*c^4 ;...
     0 1 2*d 3*d^2 4*d^3 5*d^4;...
     0 0 2 6*c 12*c^2 20*c^3;...
     0 0 2 6*d 12*d^2 20*d^3];
b3 = [0.5;0;0;0;0;0];
x3 = A3\b3;
 
A4 = [1 d d^2 d^3 d^4 d^5;... 
     1 e e^2 e^3 e^4 e^5;... 
     0 1 2*d 3*d^2 4*d^3 5*d^4 ;...
     0 1 2*e 3*e^2 4*e^3 5*e^4;...
     0 0 2 6*d 12*d^2 20*d^3;...
     0 0 2 6*e 12*e^2 20*e^3];
b4 = [0;0.5;0;0;0;0];
x4 = A4\b4;
%x1为第一段规划轨迹函数的参数，其余同理
X = [x1,x2,x3,x4]
```

#### 轨迹可视化matlab代码

```matlab
t1 = linspace(0,1,100);                                                      
%时间设定（第一段）
t2 = linspace(1,2,100);                                                      
%时间设定（第二段）
t3 = linspace(2,3,100);                                                      
%时间设定（第三段）
t4 = linspace(3,4,100);                                                      
%时间设定（第四段）
x1 = 0.5+5*t1.^3 - 7.5*t1.^4 + 3*t1.^5;                                      
%x方向位置方程（第一段）
y1 = sqrt((1-x1).*x1)+1;                                                     
%y方向位置方程（第一段）
x2 = 16.5 - 60*t2 + 90*t2.^2 - 65*t2.^3 + 22.5*t2.^4 - 3*t2.^5;              
%x方向位置方程（第二段）
y2 = -sqrt((1-x2).*x2)+1;                                                    
%y方向位置方程（第二段）                                   
x3 = 1/2*(513 - 1080*t3 + 900*t3.^2 - 370*t3.^3 + 75*t3.^4 - 6*t3.^5);       
%x方向位置方程（第三段）
y3 = -sqrt((1-x3).*x3)+1;                                                    
%y方向位置方程（第三段）
x4 = 1/2*(-2943 + 4320*t4 - 2520*t4.^2 + 730*t4.^3 - 105*t4.^4 + 6*t4.^5);   
%x方向位置方程（第四段）
y4 = sqrt((1-x4).*x4)+1;                                                     
%y方向位置方程（第四段）
figure(1);plot(x1,y1,'r');                                                  
%画出规划的轨迹的曲线
axis([-0.5,1.5,0,2]);
xlabel('x');
ylabel('y');
title('规划轨迹');
hold on;
plot(x2,y2,'b');           
plot(x3,y3,'r');             
plot(x4,y4,'b');              
legend('规划路径1','规划路径2','规划路径3','规划路径4')
hold off
v1_x = 1/2*(30*t1.^2-60*t1.^3+30*t1.^4);
v1_y = -1/2*(30*t1.^2-60*t1.^3+30*t1.^4);
v1 = sqrt(v1_x.^2+v1_y.^2);                                                  
%速度方程（第一段）
v2_x = 1/2*(-120+360*t2-390*t2.^2+180*t2.^3-30*t2.^4);
v2_y = 1/2*(-120+360*t2-390*t2.^2+180*t2.^3-30*t2.^4);
v2 = sqrt(v2_x.^2+v2_y.^2);                                                  
%速度方程（第二段）
v3_x = 1/2*(-1080+1800*t3-1110*t3.^2+300*t3.^3-30*t3.^4);
v3_y = -1/2*(-1080+1800*t3-1110*t3.^2+300*t3.^3-30*t3.^4);
v3 = sqrt(v3_x.^2+v3_y.^2);                                                  
%速度方程（第三段）
v4_x = 1/2*(4320-5040*t4+2190*t4.^2-420*t4.^3+30*t4.^4);
v4_y = 1/2*(4320-5040*t4+2190*t4.^2-420*t4.^3+30*t4.^4);
v4 = sqrt(v4_x.^2+v4_y.^2);                                                  
%速度方程（第四段）
figure(2);plot(t1,v1,'g');                                                   
%画出规划轨迹的速度曲线
xlabel('time')
ylabel('velocity')
title('速度曲线')
hold on;
plot(5*t2,v2,'b');             
plot(5*t3,v3,'g');             
plot(5*t4,v4,'b');              
legend('规划速度1','规划速度2','规划速度3','规划速度4') 
hold off
a1_x = 1/2*(60*t1-180*t1.^2+120*t1.^3);                         
a1_y = -1/2*(60*t1-180*t1.^2+120*t1.^3);
a1 = sqrt(a1_x.^2+a1_y.^2);                                                   
%加速度方程（第一段）
a2_x = 1/2*(360-780*t2+540*t2.^2-120*t2.^3);
a2_y = 1/2*(360-780*t2+540*t2.^2-120*t2.^3);
a2 = sqrt(a2_x.^2+a2_y.^2);                                                   
%加速度方程（第二段）
a3_x = 1/2*(1800-2220*t3+900*t3.^2-120*t3.^3);
a3_y = -1/2*(1800-2220*t3+900*t3.^2-120*t3.^3);
a3 = sqrt(a3_x.^2+a3_y.^2);                                                   
%加速度方程（第二段）
a4_x = 1/2*(-5040+4380*t4-1260*t4.^2+120*t4.^3);
a4_y = 1/2*(-5040+4380*t4-1260*t4.^2+120*t4.^3);
a4 = sqrt(a4_x.^2+a4_y.^2);                                                   
%加速度方程（第四段）
figure(3);plot(5*t1,a1,'r');                                                    
%画出规划轨迹的速度曲线
xlabel('time')
ylabel('accelerate')
title('加速度曲线')
hold on;
plot(5*t2,a2,'b');                
plot(5*t3,a3,'r');               
plot(5*t4,a4,'b');                
legend('规划加速度1','规划加速度2','规划加速度3','规划加速度4') 
hold off
theta1 = calc_theta(x1,y1);
theta2 = calc_theta(x2,y2);
theta3 = calc_theta(x3,y3);
theta4 = calc_theta(x4,y4);                                                   
%计算出到四个点转动的关节大小
figure(4);plot(5*t1,theta1(1,1:100),'g');                                       
%画出关节一关于时间的曲线
xlabel('time')
ylabel('theta1')
title('关节一轨迹')
hold on;
plot(5*t2,theta2(1,1:100),'b');               
plot(5*t3,theta3(1,1:100),'g');                 
plot(5*t4,theta4(1,1:100),'b');                  
legend('规划关节1轨迹1','规划关节1轨迹2','规划关节1轨迹3','规划关节1轨迹4')
hold off;
figure(5);plot(5*t1,theta1(1,101:200),'g');                                     
%画出关节一关于时间的曲线                                
xlabel('time')
ylabel('theta2')
title('关节二轨迹')
hold on;
plot(5*t2,theta2(1,101:200),'b');                
plot(t5*3,theta3(1,101:200),'g');               
plot(5*t4,theta4(1,101:200),'b');                
legend('规划关节2轨迹1','规划关节2轨迹2','规划关节2轨迹3','规划关节2轨迹4') 
hold off;
t = linspce(0,2*pi,100)
% theta = linspace(0,2*pi,100);
xd = 0.5*cos(t)+0.5;
yd = 0.5*sin(t)+1;
figure(6);
plot(xd,yd,'r');

function inverse = calc_theta(x,y)
%计算关节变化
cir = sqrt(x.^2+y.^2);
alpha = acos(1 - (cir.^2)/2);
beta = acos(cir/2);
theta2 = pi - alpha;
theta1 = atan2(y, x) - beta;
inverse = [theta1,theta2];
End

```