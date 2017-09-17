#The Model
## Student describes their model in detail. This includes the state, actuators and update equations.
Started out at 0ms latency, using values derived from course video.
Set latency to 100ms, had car doing significant amount of fishtailing. Also had the difficulty that when on the ideal line, 
the car would still rapidly steer either side of the line. 
Started tuning values by changing emphasis on constraints. Went for smoother turn rate, which helped but meant we couldn't make turns.
Smoother motion came when started de-emphasising ideal position.
Found fine balance of very slight emphasis on position, compared with much greater emphasis on heading. Couldn't have too smooth
a turn rate or we wouldn't make the turn after the bridge. 

# Timestep Length and Elapsed Duration (N & dt)
## Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. 
Additionally the student details the previous values tried.

# Polynomial Fitting and MPC Preprocessing
## A polynomial is fitted to waypoints.
## If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.

# Model Predictive Control with Latency
## The student implements Model Predictive Control that handles a 100 millisecond latency. 
## Student provides details on how they deal with latency.
