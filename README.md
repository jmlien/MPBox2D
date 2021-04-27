# MPBox2D++

## Overview

MPBox2D++ is a library for motion planning in dynamic 2D enviroment with moving obstacles. Obstacles' motion are unknown and unpredictable. What only know to MPBox2D++ are the maximum translational and angular velocities of every obstacles. For more information, please visit the project website [http://masc.cs.gmu.edu/wiki/ECT](http://masc.cs.gmu.edu/wiki/ECT).


## To Build

```
./gen.sh
cd build/release
make
```

----

## Usage

```
./mpbox2d [options] *.mp
```
Options:

* `-s1 value` random seed1, for motion planning
* `-s2 value` random seed2, for simulation
* `-rv value` robot velocity
* `-i value` maximum iterations, default is 10
* `-f value` use fixed time replan, replan every `value` second
* `-t value` simulation interval in second, default is 0.01
* `-j` use jurs method
* `-z` replan every time
* `-d` analysis
* `-g` disable OpenGL

----

## Problem Definition 

A .mp file defines a motion planning problem in which restores all the settings and configration parameters required for a simulation.
An example .mp file looks like below:

```
#a line start with # is comment

#define motion planner
#use rrt planner
#k = maximum samples for initial planning
#d = maximum expension distance
#ka = maximum samples for replanning
Tree=(rrt k=5000 d=0.5 w=0.2 ka=1000 da=0.2 wa=0.5)

#define local planner
#use straight line local planner
LP=sl

#define distance metric
DM=euler

#define workspace
WKSpace=warehouse.ws

#define query
#start goal
Query = (-13,8) (13,-8)

#reserved buget before ECT
budget = 0.05
```

For more examples of supported labels and values, please refer to the provided .mp files.

----

## WorkSpace

Each .mp file must refer to a workspace which defines the simulation environment in a .ws file. A .ws file includes the following content:

* Translational resolution

```
tres=0.01
```

* Rotational resolution

```
rres=0.01
```

* Bounding box of the space. For example:

```
bbox=[-18,15,-10,13.5,0,0]
```

* Specified number of obstacles. For example:

```
obstacle 5
```

* Reference to .poly files for each obstacle with initial configurations. For example:

```
models/plane.poly tx=-15 ty=-6 v=10 w=0.1  sx=0.4 sy=0.4 rz=-2
models/plane.poly tx=8 ty=10 v=10 w=0.1  sx=0.4 sy=0.4
models/plane.poly tx=-5 ty=-6 v=10 w=0.1  sx=0.4 sy=0.4 rz=-1.57
models/crown-7.gif.poly tx=-0.5 ty=-8 sx=0.15 sy=0.30 rz=1.57
models/crown-7.gif.poly tx=-2 ty=-2 sx=0.15 sy=0.30 rz=3.14
```

* Number of robots (usually one). For example:

```
robot 1
```

* DOF and velocity of the robot. For example:

```
tx ty v=1
```


| Instance  | Descrption |
|:---------:|:-----------:|
| tx        | robot can move along x axis |
| ty        | robot can move along y axis |
| v = value | maximum transolational velocity of the robot/obstacle |
| w = value | maximum angluar velocity of an obstacle |
| sx / sy = value | x scale / y scale of the geometry model |
| tx / ty = value | obstacle's initial x / y position |
| rz = value | obstacle's initial orientation |
| bbox = [values] | bounding box [xmin,xmax,ymin,ymax,zmin,zmax] |

----

## GUI Key Bindings

| Key     | Description   | 
|:-------:| ------------- |
| ? | Print key bindings |
| r | Toggle roadmap |
| p | Toggle executed path |
| c | Change roadmap node color |
| w | Toggle displaying solid |
| o | Toggle obstacles |
| t | Toggle displaying replanning times |
| j | Toggle joints and base |
| l | Toggle current target |
| . | Toggle displaying polygon robot config as point |
| - | Backward one frame |
| < | Backward one frame |
| = | Forward one frame |
| > | Backward one frame |
| s | Toggle saving images |
| q | Reset animation |
| blank | Toggle animation |
| R | Reset animation speed factor |
| ] | Increase animation speed factor |
| [ | Decrease animation speed factor |
| D | Dump current config of robot and all obstacles |

----

##Authors

* Yanyan Lu, [blackjade6@gmail.com](mailto:blackjade6@gmail.com), SDE, Amazon
* Zhonghua Xi, [zxi@gmu.edu](mailto:zxi@gmu.edu), Ph.D. Student, CS Dept., George Mason University 
* Yue Hao, [yhao3@gmu.edu](mailto:yhao3@gmu.edu), Ph.D. Student, CS Dept., George Mason University 
* Jyh-Ming Lien, [jmlien@cs.gmu.edu](mailto:jmlien@cs.gmu.edu), Associate Professor, CS Dept., George Mason University 



## Publications
* **Predict Collision Among Rigid and Articulated Obstacles with Unknown Motion**, Yanyan Lu and Zhonghua Xi and Jyh-Ming Lien, The Eleventh International Workshop on the Algorithmic Foundations of Robotics (WAFR), Aug. 2014 
* **Collision Prediction Among Polygons with Arbitrary Shape and Unknown Motion**, Yanyan Lu and Zhonghua Xi and Jyh-Ming Lien, IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Sep. 2014
* **Collision Prediction: Conservative Advancement Among Obstacles With Unknown Motion**, Yanyan Lu and Zhonghua Xi and Jyh-Ming Lien, International Design and Engineering Technical Conferences & Computers and Information in Engineering Conference (IDETC/CIE), ASME, Aug. 2014 
* **Conservative Collision Prediction Among Polygons with Unknown Motion**, Yanyan Lu and Zhonghua Xi and Jyh-Ming Lien, George Mason University, (Technical Report), 2013

