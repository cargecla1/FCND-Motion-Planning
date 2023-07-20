# FCND-Motion-Planning
In this project you will integrate the techniques that you have learned throughout the last several lessons to plan a path through an urban environment. 

The code on this GitHub repository is a collection of Python scripts that implement various motion planning algorithms. The algorithms are designed to be used with the Gazebo simulator, and they can be used to plan paths for robots in a variety of environments.

The repository includes code for the following algorithms:

RRT*
PRM*
A*
D*
Visibility Graph


The code is well-documented, and it includes a number of examples that show how to use the algorithms. The repository is a valuable resource for anyone who is interested in learning about motion planning or using it in their own projects.

Here is a brief summary of each of the algorithms:

RRT*: Rapidly-exploring Random Tree is a sampling-based algorithm that builds a tree of possible paths. The tree is grown by randomly sampling points in the environment and then connecting them to the existing tree if they are within a certain distance.

PRM*: Probabilistic Roadmap is another sampling-based algorithm that builds a graph of possible paths. The graph is built by randomly sampling points in the environment and then connecting them if they are within a certain distance.

A*: A* is a graph search algorithm that finds the shortest path between two points in a graph. The algorithm works by expanding the search frontier one node at a time, and it keeps track of the shortest path that it has found so far.

D*: D* is a variant of A* that uses dynamic programming to improve the efficiency of the search.

Visibility Graph: A visibility graph is a graph that represents the visibility relationships between points in an environment. The graph can be used to plan paths by finding a path that only visits nodes that are visible to each other.
