# What is ROS2_Control
This framework helps to create a standardized method for the hardware and software control for robot movement. It addresses the issue of having to write custom controllers and drivers for the various problems that have been solved before. This framework also allows us to pick and choose different combination of algo and different drivers for different setups, making changes and upgrades much easier.

![[Pasted image 20240217195212.png]]

By having standardized messages between the controller and drivers, we can easily swap and replace the nodes.

# Components

### Controller Manager 
- main component of the ros2_control framework
- manages
	- lifecycle of controllers
	- access to hardware interfaces
	- offers service
##### Determinism 
- controller manager should have as little *jitter* as possible 
- normal linux kernel is not well suited for hardware control
- configurations must be performed to allow scheduling priorities
	- https://control.ros.org/humble/doc/ros2_control/controller_manager/doc/userdoc.html

### Hardware Interface 
For controller manager to work with the hardware, it expects a hardware interface. The hardware interface has two interface types to consider
- Command interfaces (Read/Write)
	- Like the name suggests this is where commands are sent. Ex. motors can be controlled by speed, torque, etc.
- State interfaces (Read only)
	- This would be like velocity, position, etc.

One robot can have multiple hardware interfaces, each with different command and state interfaces. To collect and define all these interfaces to the controllers, the resource manager reads the URDF and looks for <ros2_control> tags.
![[Pasted image 20240217201155.png]]

# Controller 
The controller will take in commands from inputs through cmd_vel (?) and do the calculations to send to the hardware through hardware interfaces exposed by the resource manager. 

- ROS2 controller package already covers most use cases and in our case, the differential drive controller will be used. There are other ones such as ackermann drive controller, and many more for different movement configurations.

# Controller Manager
The controller manager takes the commands from the controllers and links them up to the appropriate hardware interfaces through the hardware manager.
![[Pasted image 20240217201913.png]]

# Resource 
https://www.youtube.com/watch?v=4QKsDf1c4hc