## Project: Kinematics Pick & Place

---

**Steps to complete the project:**  


1. Set up your ROS Workspace.
2. Download or clone the [project repository](https://github.com/udacity/RoboND-Kinematics-Project) into the ***src*** directory of your ROS Workspace.  
3. Experiment with the forward_kinematics environment and get familiar with the robot.
4. Launch in [demo mode](https://classroom.udacity.com/nanodegrees/nd209/parts/7b2fd2d7-e181-401e-977a-6158c77bf816/modules/8855de3f-2897-46c3-a805-628b5ecf045b/lessons/91d017b1-4493-4522-ad52-04a74a01094c/concepts/ae64bb91-e8c4-44c9-adbe-798e8f688193).
5. Perform Kinematic Analysis for the robot following the [project rubric](https://review.udacity.com/#!/rubrics/972/view).
6. Fill in the `IK_server.py` with your Inverse Kinematics code. 


[//]: # (Image References)

[image1]: ./misc/kine1.PNG
[image2]: ./misc/kine2.PNG
[image3]: ./misc/kine3.PNG
[image4]: ./misc/kine4.PNG
[image5]: ./misc/kine5.PNG
[image6]: ./misc/kine6.PNG
[image7]: ./misc/kine7.PNG
[image8]: ./misc/kine8.PNG
[image9]: ./misc/kine9.PNG
[image10]: ./misc/kine10.PNG
[image11]: ./misc/kine11.PNG
[image12]: ./misc/kine12.PNG
[image13]: ./misc/kine13.PNG
[image14]: ./misc/kine14.PNG
[image15]: ./misc/kine15.PNG
[image16]: ./misc/kine16.PNG
[image17]: ./misc/kine17.PNG
[image18]: ./misc/kine18.PNG
[image19]: ./misc/kine19.PNG
[image20]: ./misc/kine20.PNG
[image21]: ./misc/kine21.PNG
[image22]: ./misc/kine22.PNG
[image23]: ./misc/kine23.jpg
[image24]: ./misc/kine24.PNG

## [Rubric](https://review.udacity.com/#!/rubrics/972/view) Points

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Kinematic Analysis
#### 1. Run the forward_kinematics demo and evaluate the kr210.urdf.xacro file to perform kinematic analysis of Kuka KR210 robot and derive its DH parameters.

The forward_kinematics demo could help test different joint configuration and how the arm would position in space.

![alt text][image21]

The kinematic analysis can be found below, including the DH table (open in other window for more quality).

![alt text][image23]

#### 2. Using the DH parameter table you derived earlier, create individual transformation matrices about each joint. In addition, also generate a generalized homogeneous transform between base_link and gripper_link using only end-effector(gripper) pose.

From the urdf file, the lengths of the links are retreived:

![alt text][image1]

And then the table can be populated.

Links | alpha(i-1) | a(i-1) | d(i-1) | theta(i)
:--- | ---: | ---: | ---: | ---:
0->1 | 0    | 0    | 0.75 | q1
1->2 | -90  | 0.35   | 0  | q2 - 90
2->3 | 0    | 1.25   | 0  | q3
3->4 |  -90 | -0.054   | 1.5 | q4
4->5 | 90   | 0    | 0  | q5
5->6 | -90  | 0    | 0  | q6
6->EE | 0   | 0    | 0.303 | 0

**Constructing Individual Transformation Matrices**

![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]
![alt text][image8]
![alt text][image9]

**Accounting difference in orientation of the gripper link frame**

![alt text][image10]

**Rotation Matrices and Wrist Center Position Calculation**

![alt text][image11]
![alt text][image12]
![alt text][image13]

#### 3. Decouple Inverse Kinematics problem into Inverse Position Kinematics and inverse Orientation Kinematics; doing so derive the equations to calculate all individual joint angles.


![alt text][image14]
_Image from Udacity_

**Calculating sides of triangle**

![alt text][image16]

**Calculating angles of triangle (Law of Cosines)**

![alt text][image17]

![alt text][image15]
_Image from Udacity_

**Calculating Theta1, Theta2 and Theta3**

![alt text][image22]

**Using the Homogeneous RPY rotation from  base link and gripper link, and the Tranpose of the Rotation matrix from link 0 to link 3, obtain R3_6**

![alt text][image18]
![alt text][image19]

**Calculating Theta4, Theta5 and Theta6 using elements from R3_6**

![alt text][image20]

### Project Implementation

#### 1. Fill in the `IK_server.py` file with properly commented python code for calculating Inverse Kinematics based on previously performed Kinematic Analysis. Your code must guide the robot to successfully complete 8/10 pick and place cycles. Briefly discuss the code you implemented and your results. 

Here I'll talk about the code, what techniques I used, what worked and why, where the implementation might fail and how I might improve it if I were going to pursue this project further.  

Once the calculations were completed, it was then first tested in the "IK_debug.py" script. It help to fix bugs on the code and test the implementation. After a few iterations with a significant error, a low percentage was achieved and then the code was ready to pass to the "IK_server.py" file.

Testing the implementation along with the simulation showed that the trayectory was being drawn correctly, and the arm was trying to follow it but having erratic rotations in the wrist. After some research and testing with some angle bounderies for the wrist joints, it was suggested on the course group that it may have been because of the API that performs the inverse transform of R0_3 when obtaining R3_6. Although it is still not clear the reason why it fails, replacing it with a transpose operation seemed to fix the issue, while performing the same final calculation. Further explanation will be pursued for this behaviour.

Following this, the arm performs better, averaging a succesful pickup of 8 cans of every 10, having failures mostly in the grapping of the object or droping it. It is evident that depending of the path set, the time to perform the inverse kinematics calculation is high, and further pruning of the code could be made to improve this e.g. leaving out simplify usage and limiting the use of libraries like numpy.

![alt text][image24]
