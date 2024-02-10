- Hardware logic & control algorithm logic
- Publisher/Subscriber model to communicate between these two logics
	- **Slow**! 
	- Should be no delay between **Controller** and **Hardware Interface**


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
