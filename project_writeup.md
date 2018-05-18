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
These scripts contain a basic planning implementation that includes:
- functions to create a grid representation for the planning problem
- functions to search for the optimal path to go from the start position to the end position while avoiding obstacles (A*)
- function to control the drone by changing the state/behavior of the drone when certain conditions are met


### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
To set my global home position, I did the following:
- I used the readline function to read the first line of the file
- I replaced the strings 'lat0' and 'lon0' with empty strings
- I then split the strings into array elements using the ',' character as the delimeter
- then I finally converted the array of strings into an array of floats

#### 2. Set your current local position
To set my current local position I did the following:
- I used the global_to_local function to convert the longitude and latitude values in the global position into NED values for the local position.

#### 3. Set grid start position from local position
I set the grid start postion by offsetting the current position by the corner/edge values of the grid.
I basically transformed the vehicle's position into the grid's space

#### 4. Set grid goal position from geodetic coords
This was a bit tricky.
I initially tried to randomize this section, but I had some issues with random points overlapping with obstacles, thus it was impossible to find a path to these points at the latter stages.
I could have created a loop that keeps randomizing the goal position until a position is found that has no overlap with obstacles.
Nice Idea, but I am behind this class and I am trying hard to catch up.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
This was already done in the code.
The code uses the `np.linalg.norm` function to normalize the difference between the current position and the goal position.
In the case of horizontal or vertical movements, the value of this would be 1 since this would evaluate to sqrt(1^2 + 0^2) or sqrt(0^2 + 1^2) which is equal to 1.
For diagoanal movements, this would evaluate to sqrt(1^2 + 1^2) which is equal to sqrt(2)

#### 6. Cull waypoints 
For this step, I used the collinearity check to remove points that exist on the same plane.
I could have used a bresman type algorithm to further prune out way points to reduce some zig zaggyness of the movement of the drone, but like I mentioned earlier I am trying to catch up and my slogan is simple, quick, fast, but thorough

### Execute the flight
#### 1. Does it work?
It works!

### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  
# Extra Challenges: Real World Planning
The only extra thing I did was adjust the deadbands to help smoothen out the movement of the drone a bit.
But yes, there is a lot more that I could have done to go above and beyond, but not today sir! :)


