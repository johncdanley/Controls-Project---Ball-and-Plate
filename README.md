# Control System Design of Ball and Plate
#### MECA482 - Control System Design
### Angel Mendoza, Chen Hung Yang, Jonathan Gomez, Marco Machuca, John Danley
-----------------------------------------------------------------------------------------
## 1. Introduction
 **Description of the project:**

The ball and plate system consists of a tiltable plate controlled by two motors at perpendicular orientations with a ball positioned on the plate. The goal is to develop the Simulink model that controls the X and Y axis of the plate system in Coppelia Sim Edu.

test

test

#### Table of Contents
- [1. Introduction](#1-Introduction)
- [2. Modeling](#2-Modeling)
- [3. Controller Design and Simulations](#3-Controller-Design-and-Simulations)  
  - [3.1. Force Calculations](#31-Force_Calculations)  
  - [3.2. Input Voltage to Position Change Transfer Function](#32-Input_Voltage_to_Position_Change_Transfer_Function)  
  - [3.3. Motor Parameters](#33-Motor_Parameters_to_Refine_Transfer_Function)
  - [3.4. System Parameters](#34-System_Parameters)
  - [3.5. Coded Simulation](#35-Coded_Simulation)
- [4. Checklist](#4-Checklist)
- [5. References](#5-References)
  
-----------------------------------------------------------------------------------------
## 2. Modeling
The system is simulated in Coppelia Sim Edu utilizing a plate that is supported by two revolute joints on the individual sides that control the tilting mechanism for the balance of the ball. The control system described is to hold a freely rolling ball in a specific position on the plate using a senor for a feedback loop to maintain the position of the ball. For measuring the ball position, a camera sensor was used to provide feedback information.

The data is processed in the following way:
* The camera observes the position of the ball in CoppeliaSim and sends the data to Matlab
* Matlab recieves data from Coppelia
* Simulink retrieves the data from the Matlab workspace and calculates the rotation of the motors, 


-----------------------------------------------------------------------------------------
## 3. Controller Design and Simulations
A controller was developed to balance the ball on the plate with the following specifications:
* Settling time: Ts(s) ≤ 3.0
* Percent Overshoot: %OS ≤ 10

test

### 3.1. Force Calculations
To mathematically develop the proper equations to relate the necessary angle of lift on the balance plate (α) to the distance the ball has strayed away from the balance plate’s target location (x). Using the free body diagram below (Figure 1), forces from the ball’s inertia (Fr) and due to gravity on the ball (Fg) can be mapped out to determine the proper functions. 
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82175334-886c6200-9888-11ea-8444-ffbccba078fc.png" height = "auto" style="margin:auto">
</p>
The sum of forces can be written:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82176611-1b5acb80-988c-11ea-8478-a5c56a67b5a1.png" height = "auto" style="margin:10px 10px">
</p>
Relating the angle of tilt of the plate (α) to the force on the ball by gravity (Fg) gives the following equation: 
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82176622-2150ac80-988c-11ea-9fc1-96699cde30c8.png" height = "auto" style="margin:auto">
</p>
Using torque, an equation can be formed relating force of intertia to ball radius (rb) with the proper torque equaton of the rolling ball:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82176629-2877ba80-988c-11ea-805e-8a4c82cd2360.png" height = "auto" style="margin:auto">
</p>
The equation for the hollow ball inertia is given below: 
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82177723-3e3aaf00-988f-11ea-9f3a-0af57457e515.png" height = "auto" style="margin:auto">
</p>-
By plugging the ball's inertia into inertial force (Fr) equation, the new equation is shown below:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82177735-45fa5380-988f-11ea-8ed7-a186885a379d.png" height = "auto" style="margin:auto">
</p>
Fr and Fg can be used to construct the new force equation for ball displacement vs lift angle of plate.
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82179844-20237d80-9894-11ea-9b4a-b4c48017d1fc.png" height = "auto" style="margin:auto">
</p>
The angle displacements of the plate and motor can be written through trigonometric relationships:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82179883-38939800-9894-11ea-9651-b8c4025f54bc.png" height = "auto" style="margin:auto">
</p>
With small angle approximation and laplace transform, the transfer function is given below:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82269652-29a9f580-9927-11ea-8369-a91bb23e6c33.png" height = "auto" style="margin:auto">
</p>

### 3.2 Input Voltage to Position Change Transfer Function
The block diagram below illustrates the in put of Vm(s) through the servo plant (SRVO2), outputting the servo angle (θ(s)), which in response, adjusts the position of the ball (X(S)) after going through the plant of the balance plate (Pbb(S)):
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82269395-6d502f80-9926-11ea-90be-a226339a803f.png" height = "auto" style="margin:auto">
</p>

### 3.3 Motor Parameters to Refine Transfer Function

Using a SRV02, after motor analysis accounting for the motor specifications, the motor's transfer function is given below:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82267116-573f7080-9920-11ea-9f5a-a0bd27307374.png" height = "auto" style="margin:auto">
</p>
Where: 
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82267124-5c042480-9920-11ea-9d45-57eee2b533ca.png" height = "auto" style="margin:auto">
</p>
Using the above parameters, the simplified transfer function relating input motor voltage to position change of the ball is given below:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82269395-6d502f80-9926-11ea-90be-a226339a803f.png" height = "auto" style="margin:auto">
</p>

### 3.4 System Parameters 

A camera is employed to control the PD controller. As the ball changes position, the sensor captures the movement and passes this information to the controller. Using the above transfer function, the controller powers the motors to position the plate accordingly. 
The following parameters were determined to find the appropriate gains for the controller
<p align = "center">
Ts ≤ 3.0 s  

%OS ≤ 10
</p>
The above specifications are used to determine the natural frequency value (ωn) whose equations ar shown below:
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82270804-cc17a800-992a-11ea-8323-f520f54a101e.png" height = "auto" style="margin:auto">
</p>

### 3.5 Coded Simulation
<p align = "center">
  <img src = "https://user-images.githubusercontent.com/65521928/82269359-53aee800-9926-11ea-9e1f-07e72668d748.png" height = "auto" style="margin:auto">
</p>


-----------------------------------------------------------------------------------------
## 4. Checklist
Deliverables:
* Project Presentation
* Webpage
* Mathematical model of the system using MATLAB/Simulink
* Show that the algorithm facilitates the design requirements
* Test algorithms on the physical system

-----------------------------------------------------------------------------------------
## 5. References

[1] Subramanian, Raaja Ganapathy, et al. "Uniform ultimate bounded robust model reference adaptive
PID control scheme for visual servoing." Journal of the Franklin Institute 354.4 (2017): 1741-1758.

[2] Kildare, R., Hansen E., Leon, E., PID Control of Furuta Pendulum, Control System Design Project Fall
2019

##### Use this for inserting images into the middle of the document
<p align = "center">
  <img src = "img" height = "auto" style="margin:auto">
</p>

-----------------------------------------------------------------------------------------
