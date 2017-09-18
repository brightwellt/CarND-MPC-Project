# The Model
## Student describes their model in detail. This includes the state, actuators and update equations.
The objective was to use Model Predictive Control, to drive a car successfully round the simulator track.
Here is the model used:
!Model.PNG!

The car state required for the simulator included:
- current x, y position
- current heading (psi)
- current velocity 
We also had the cross track error and psi error. 
As per the course video I transformed the coordinate space 


The car itself had two actuators; the steering angle and throttle. These were constrained to +/- 25° and +/- 1. 

A cost function was created, where different criteria were considered, and given appropriate weighting.
- how far away from the desired position the car was (cross track error)
- deviation of our heading (orientation error).
- velocity cost (trying to travel at speed).
- smoothness of heading / throttle changes, to focus on smoother driving (rapid changes in current state, but also comparing with previous values of steering angle and acceleration).

The equations for the model come from the class:


## Tuning of constraints.
My starting position was to use the values derived from the course video.
Set latency to 100ms, had car doing significant amount of fishtailing. Also had the difficulty that when on the ideal line, 
the car would still rapidly steer either side of the line. 
Started tuning values by changing emphasis on constraints. Went for smoother turn rate, which helped but meant we couldn't make turns.
Smoother motion came when started de-emphasising ideal position.
Found fine balance of very slight emphasis on position, compared with much greater emphasis on heading. Couldn't have too smooth
a turn rate or we wouldn't make the turn after the bridge. 

# Timestep Length and Elapsed Duration (N & dt)
## Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. 

For driving round at racetrack speeds, it doesn't make sense to predict more than 1-2 seconds into the future. For certain sections such as tight bends, the required inputs even just 1 second later could be radically different. Were we driving a train, with much slower acceleration then we may want to look further ahead. 
For MPC we have T = N * dt. Given a desired T of 1s, I started out with N = 10, dt = 0.1. I was able to tune my model's weights satisfactorily using these values, but also looked at N = 20, dt = 0.05; another popular choice on the forums.
For fun I also tried N = 50, dt = 0.1.

# Polynomial Fitting and MPC Preprocessing
## A polynomial is fitted to waypoints.
## If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.



# Model Predictive Control with Latency
## The student implements Model Predictive Control that handles a 100 millisecond latency. 
## Student provides details on how they deal with latency.

To cope with the latency, I did some tuning as described previously. I also took the previous state (velocity, steering angle, throttle etc) and estimated the state 100ms later, using this as an input to my model.
