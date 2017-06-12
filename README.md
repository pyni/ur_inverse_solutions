# ur_inverse_solutions
We refer https://github.com/ros-industrial/universal_robot

This is the analytical solutions for UR robot.

Why we use this ?

Usually, Moveit! ,which uses KDL solver or some other plugins , can not 
meet our requirements if we want more IK solutions. But for UR5, we can easily 
get its analytical solutions to obtain all the IK solutions.


But this code does not consider about the collision for the robot itself.
Therefore, some solutions can not be used.
 ![image](https://github.com/pyni/ur_inverse_solutions/blob/master/test.png) 
