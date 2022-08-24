
# Smoothing the trajectory of the service robot using artificial intelligence

## Summary
*This section is to be filled out by the project manager based on the [summary document](https://docs.google.com/spreadsheets/d/12xi2yOMm-X5PEecgyRe3WEurcSaN9A5z4DHgBacQT6M).*

| Company | [Yanu](https://yanu.ai/)                                                                                                       |
| :--- |:-------------------------------------------------------------------------------------------------------------------------------|
| Project Manager | [Project Manager](https://profile.link)                                                                                        |
| Project Team | Alvo Aabloo, Houman Masnavi, Karl Kruusamäe, Igor Rybalskii, Kirsi Zirel, Kristjan Laht                                        |
| Challenge Tackled | Developing and testing robot hand trajectory optimization for ROS for smooth robot hand movement                               |
| Technology Used | ROS, MoveIt, TOPP-RA                                                                                                           |
| Lessons Learned | Using and debugging general purpose planners is very difficult and requires a lot of specilized knowledge that is hard to get. |
| Result Published | We integrated optimal trajectory optimization with the ROS robot hand ecosystem                                                |
| Target Group | Manufacturing floors, robot food providers                                                                                     |
| Diagrams/Photos |                                                                                                                                |
| Video |                                                                                                                                |

## Implementation Details

### Description

- This is a ROS package that processes MoveIt trajectories into a trajectory that is optimal with respect to speed / acceleration / time limits. This is usually a nice to have, but for some robots like the Panda Robot, it's a necessary component for smooth operation. Panda robots require jerk-free trajectories but the using the default MoveIt trajectories fails with a lot of jerk. This is _very_ problematic for service robots that need to carry things. 

- This is built upon ROS and [TOPP-RA](https://github.com/hungpham2511/toppra)

### How to Install & Run

0. [Create a working ROS workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
1. [Install toppra](https://github.com/hungpham2511/toppra/blob/develop/cpp/README.md)
    - Or create a toppra wrapper package by cloning toppra to `catkin_ws/src/toppra-ros/toppra`
    - and adding a CMake file with [extra dependencies turned off](https://gist.github.com/KingBoomie/348d0379229965d9ab4be9f6d7bb9ce5) to `catkin_ws/src/toppra-ros`
     
2. Clone this package into `catkin_ws/src` 
    ```bash
    git clone https://github.com/ai-robotics-estonia/smoothing_the_trajectory_of_the_service_robot_using_artificial_intelligence
    ```
3. [Setup MoveIt](https://ros-planning.github.io/moveit_tutorials/doc/getting_started/getting_started.html)
4. in folder `catkin_ws` source ROS workspace `source /opt/ros/noetic && source devel/setup.bash`
5. build with `catkin_make`
6. run the ros service `rosrun toppra_optimizer_ros toppra_optimizer_server`
7. generate a plan using moveit
8. in another terminal run `rostopic pub /optimize_trajectory/goal toppra_optimizer_ros/OptimizeActionGoal` with the message contents being the result from step 7. (or use [this](https://gist.github.com/KingBoomie/982d5c7e5bec87fda6f558af3451c47e) example generated plan)
9. run the resulting trajectory on a real robot


### Credits

If you use this library for your research, we encourage you to
reference the accompanying paper [A new approach to Time-Optimal Path Parameterization based on Reachability Analysis, IEEE Transactions on Robotics, vol. 34(3), pp. 645-659, 2018.](https://www.researchgate.net/publication/318671280_A_New_Approach_to_Time-Optimal_Path_Parameterization_Based_on_Reachability_Analysis)

### Licensing

[MIT License](/LICENSE)

### How to Contribute

Create issues / pull requests in this repo. 

### Testing

*Provide code examples and how to run tests for your project.*
