## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---


# Required Steps for a Passing Submission:
1. Load the 2.5D map in the colliders.csv file describing the environment.
2. Discretize the environment into a grid or graph representation.
3. Define the start and goal locations.
4. Perform a search using A* or other search algorithm.
5. Use a collinearity test or ray tracing method (like Bresenham) to remove unnecessary waypoints.
6. Return waypoints in local ECEF coordinates (format for `self.all_waypoints` is [N, E, altitude, heading], where the drone’s start location corresponds to [0, 0, 0, 0].
7. Write it up.
8. Congratulations!  Your Done!

## [Rubric](https://review.udacity.com/#!/rubrics/1534/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
These scripts contain a basic planning implementation that includes the following:

1) The motion_planning.py file is basically a step forward from the backyard_flyer_solution.py done in the pervious assignment. The motion planning code adds a PLANNING state, which didn't exit on the backyard flyer solution. Furthermore, the motion planning solution change calculate_box to a plan_path, this plan_path import utilities from the planning_utils.py file which inculde a A* algorithim to search for a path from start to goal positions.

2) The planning_utils.py file has different sections:

    a) create_grid: Account for any obstacules represented in the data that will be used to navigate and produce a representation in the form of a 2D grid.
    
    b)Action: Represents west, east, north, south as tuples and defines the cost and delta.
    
    c) valid_actions: Defines the valid moves that the drone can use to move from the start to the goal. The basic actions allow you to move only on the west, east, north, south directions.

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
Here students should read the first line of the csv file, extract lat0 and lon0 as floating point values and use the self.set_home_position() method to set global home. Explain briefly how you accomplished this in your code.

On the motion_planning.py file, from line 127 to 135 the colliders.csv file is read to get the lat0, lon0. On line 139 the home position is set using the lat0, lon0 values obtained from colliders.csv


#### 2. Set your current local position
Here as long as you successfully determine your local position relative to global home you'll be all set. Explain briefly how you accomplished this in your code.

Using the global_to_local method the local position was determine on line 145.


#### 3. Set grid start position from local position
This is another step in adding flexibility to the start location. As long as it works you're good to go!

On line 159 the grid start position was established from the local position. Applying the he north and east offsets to the local position it is possible to achieve it.


#### 4. Set grid goal position from geodetic coords
This step is to add flexibility to the desired goal location. Should be able to choose any (lat, lon) within the map and have it rendered to a goal location on the grid.

From line 164 to 175, this is done by converting ramdon arbitrary goal position which is converted to global position and then to is relative position in the grid using the offsets.


#### 5. Modify A* to include diagonal motion (or replace A* altogether)
Minimal requirement here is to modify the code in planning_utils() to update the A* implementation to include diagonal motions on the grid that have a cost of sqrt(2), but more creative solutions are welcome. Explain the code you used to accomplish this step.

In order to include the diagonal motion: fisrt, on planning_utils.py under class Action, from line 58 to 61 diagonal motions were added with a cost of sqrt(2). In addition, under def valid_actions diagonal motions were added as valid movements (refer to line 93 to 100).


#### 6. Cull waypoints 
For this step you can use a collinearity test or ray tracing method like Bresenham. The idea is simply to prune your path of unnecessary waypoints. Explain the code you used to accomplish this step.

A collinearity method was used to prune the path from points in the path that are no required to achive the goal. This algorithm compares 3 diferents points as it moves towards the goal, it is finds collinearity, it exclude the middle point and select the enxt point towards the goal and compares again. This was done on the motion_planning.py file from line 190 to 215.



### Execute the flight
#### 1. Does it work?
It works!

####I got this validation:

Logs\TLog.txt
Logs\NavLog.txt
starting connection
arming transition
Searching for a path ...
global home [-122.3974533   37.7924804    0.       ], position [-122.3974581   37.7924752    0.188    ], local position [-0.58254445 -0.43099338 -0.18898714]
North offset = -316, east offset = -445
global goal position [136.75006907 131.33622983   0.        ]
Local Start and Goal:  (316, 445) (452, 576)
Planning, please wait...
Found a path.
Pruning path, please wait...
Sending waypoints to simulator ...
takeoff transition
waypoint transition
target position [0, 0, 9, 0]
waypoint transition
target position [127, 127, 9, 0]
waypoint transition
target position [128, 127, 9, 0]
waypoint transition
target position [129, 128, 9, 0]
waypoint transition
target position [130, 128, 9, 0]
waypoint transition
target position [131, 129, 9, 0]
waypoint transition
target position [132, 129, 9, 0]
waypoint transition
target position [133, 130, 9, 0]
waypoint transition
target position [135, 130, 9, 0]
waypoint transition
target position [136, 131, 9, 0]
landing transition
disarm transition
manual transition
Closing connection ...


####And this one:

Logs\TLog.txt
Logs\NavLog.txt
starting connection
arming transition
Searching for a path ...
global home [-122.3974533   37.7924804    0.       ], position [-1.22397457e+02  3.77924805e+01 -6.00000000e-03], local position [ 0.00833986 -0.31414667  0.00691979]
North offset = -316, east offset = -445
global goal position [ 94.37624049 116.45475462   0.        ]
Local Start and Goal:  (316, 445) (410, 561)
Found a path.
Sending waypoints to simulator ...
takeoff transition
waypoint transition
target position [0, 0, 9, 0]
waypoint transition
target position [76, 76, 9, 0]
waypoint transition
target position [76, 77, 9, 0]
waypoint transition
target position [77, 78, 9, 0]
waypoint transition
target position [77, 79, 9, 0]
waypoint transition
target position [78, 80, 9, 0]
waypoint transition
target position [78, 81, 9, 0]
waypoint transition
target position [79, 82, 9, 0]
waypoint transition
target position [79, 84, 9, 0]
waypoint transition
target position [80, 85, 9, 0]
waypoint transition
target position [80, 86, 9, 0]
waypoint transition
target position [81, 87, 9, 0]
waypoint transition
target position [81, 88, 9, 0]
waypoint transition
target position [82, 89, 9, 0]
waypoint transition
target position [82, 90, 9, 0]
waypoint transition
target position [83, 91, 9, 0]
waypoint transition
target position [83, 92, 9, 0]
waypoint transition
target position [84, 93, 9, 0]
waypoint transition
target position [84, 95, 9, 0]
waypoint transition
target position [85, 96, 9, 0]
waypoint transition
target position [85, 97, 9, 0]
waypoint transition
target position [86, 98, 9, 0]
waypoint transition
target position [86, 99, 9, 0]
waypoint transition
target position [87, 100, 9, 0]
waypoint transition
target position [87, 101, 9, 0]
waypoint transition
target position [88, 102, 9, 0]
waypoint transition
target position [88, 103, 9, 0]
waypoint transition
target position [89, 104, 9, 0]
waypoint transition
target position [89, 106, 9, 0]
waypoint transition
target position [90, 107, 9, 0]
waypoint transition
target position [90, 108, 9, 0]
waypoint transition
target position [91, 109, 9, 0]
waypoint transition
target position [91, 110, 9, 0]
waypoint transition
target position [92, 111, 9, 0]
waypoint transition
target position [92, 112, 9, 0]
waypoint transition
target position [93, 113, 9, 0]
waypoint transition
target position [93, 115, 9, 0]
waypoint transition
target position [94, 116, 9, 0]
landing transition
disarm transition
manual transition
Closing connection ...


### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  
# Extra Challenges: Real World Planning

For an extra challenge, consider implementing some of the techniques described in the "Real World Planning" lesson. You could try implementing a vehicle model to take dynamic constraints into account, or implement a replanning method to invoke if you get off course or encounter unexpected obstacles.


