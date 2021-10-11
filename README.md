# Object_chaser_botcar_ROS
A basic implementation of a simple object chaser robot with ROS, surely to be improved over time.

### Requirements

This makes use of Gazebo7, RViz and ROS Kinetic.

### Directory Structure
```bash
.
├── ball_chaser
│   ├── CMakeLists.txt
│   ├── launch
│   │   └── ball_chaser.launch
│   ├── package.xml
│   ├── src
│   │   ├── drive_bot.cpp
│   │   └── process_image.cpp
│   └── srv
│       └── DriveToTarget.srv
├── my_robot
│   ├── CMakeLists.txt
│   ├── launch
│   │   ├── robot_description.launch
│   │   └── world.launch
│   ├── meshes
│   │   └── hokuyo.dae
│   ├── package.xml
│   ├── urdf
│   │   ├── my_robot.gazebo
│   │   └── my_robot.xacro
│   └── world
│       └── AmanWorld.world
└── README.md
```

### Running the simulation:

#### Update and upgrade packages:

`$ sudo apt update && sudo apt upgrade`

#### First, we need to build a catkin workspace for the project. Navigate to your preferred directory, then:

`$ mkdir -p ocbr_catkin_workspace/src/`

`$ cd ocbr_catkin_workspace/src/`

#### Time to initialize the catkin workspace:

`$ catkin_init_workspace`

#### Now clone this repo:

`$ git clone https://github.com/amanarora9848/Object_chaser_botcar_ROS.git`

#### The 'chaser' ROS nodes have been written for you in the ball_chaser/src directory. 

The `drive_bot` node will provide a service to drive robot around, and the service server publishes messages containing velocities for wheel joints.

The `process_image` node subscibes to robot's camera images, finds our desired object, and then uses the client node to request service from `drive_bot` server node.

#### Navigate back to our base directory `ocbr_catkin_workspace`

#### Here, run `catkin_make` to build the package:

`$ catkin_make`

#### Now, do:

`$ source devel/setup.bash`

#### In this terminal, let's launch our robot inside our strange Gazebo world. The launch file for this can be found in `/src/my_robot/launch/world.launch` relative to the current diretory:

`$ roslaunch my_robot world.launch`

It opens up a nice little Gazebo world, with our robot inside it.

#### Now, open a new terminal window, navigate to our `ocbr_catkin_workspace` directory and run our nodes. It makes use of `ball_chaser.launch` file situated inside `/src/ball_chaser/launch/` directory relative to our current one.

`$ source devel/setup.bash`

`$ roslaunch ball_chaser ball_chaser.launch`

#### If everything works fine, you can place the white object in front of our red bot to test its working.