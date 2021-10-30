# Course 4 Final Project

In this project, the implementation of many of the behavioral and local planning concepts discussed in Course 4 are carried out. The goal of this project will be to have a functional motion planning stack that can avoid both static and dynamic obstacles while tracking the center line of a lane, while also handling stop signs. To accomplish this, you will have to implement behavioral planning logic, as well as static collision checking, path selection, and velocity profile generation.

To do this assignment, the CARLA simulator along with the assignment code needs to be installed. Please follow these instructions:

# Implementing the Motion Planner

In this project, I have edited the "**behavioral_planner.py**", "**collision_checker.py**", "**local_planner.py**", "**path_optimizer.py**", and "**velocity_planner.py**" class files (found inside the "Course4FinalProject". This is where the implementation of motion planner is done. There are 5 main aspects of the planner that are implemented, behaviour planning logic, path generation, static collision checking, path selection, and velocity profile generation. Let's go over each of these in kind.

## Behaviour Planning Logic

In this part of the project, I have implemented the behavioral logic required to handle a stop sign. As in the lecture videos, I have implemented a state machine that transitions between lane following, deceleration to the stop sign, staying stopped, and back to lane following, when it encounters a stop sign. All of the code for the behavioral planner is contained in behavioral_planner.py.

To do this, I have first implemented the helper functions get_closest_index() and get_goal_index(). These will let the behavioral planner know where it is relative to the global path, and to compute the current goal point from the global path. Once these are done, I have then implemented the transition_state() function, which contains the behavioral state machine logic. The required details about each of these functions are given in the code comments.

## Path Generation

Here, I have computed the goal state set (the set of goal points to plan paths to before path selection) using the get_goal_state_set() function, as well as some of the path generation helper functions. In particular, you will implement thetaf(), which computes the yaw of the car at a set of arc length points for a given spiral, optimize_spiral(), which sets up the optimization problem for a given path. Finally, once the optimization is complete, the resulting spiral will be sampled to generate the path. This functionality is implemented in sample_spiral(). The required details about each of these functions are given in the code comments in the files local_planner.py and path_optimizer.py. 

## Static Collision Checking

For this part of the motion planner, I have edited `collision_checker.py`. In particular, I have implemented `circle-based` collision checking on our computed path set using the `collision_check() `function. I have implemented the circle location calculation for each point on the path. For futher details, please refer to the given code comments.

## Path Selection

The path selection portion of the project involved me evaluating an objective function over the generated path set to select the best path. The goal of this section is to eliminate paths that are in collision with static obstacles, and to select paths that both track the centerline of the global path. To encourage robust obstacle avoidance, I also added a term that penalizes how close the planned path is to other paths in the path set that are in collision with a static obstacle. I have implemented path selection in the select_best_path_index() function within collision_checker.py. For further details, please refer to the given code comments.

## Velocity Profile Generation

The last step of the project is velocity profile generation. This velocity planner will not handle all edge cases, but will handle stop signs, lead dynamic obstacles, as well as nominal lane maintenance. This is all captured in the compute_velocity_profile() function in velocity_planner.py. I have implemented the physics functions at the end of the file which will be used for velocity planning. For further details, please refer to the given code comments. 


# Evaluating the simulation results

Run the CARLA Simulator to start the simulation and run the developed Python client. Once you reach the end of the scenario, the Python client will output controller_output/trajectory.txt and controller_output/collision_count.txt.
