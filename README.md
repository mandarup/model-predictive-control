# Model Predictive Control


## Simulation Results

The car is able to drive around the simulator track without leaving road, given a reference trajectory by estimating waypoints (by fitting a polynomial to the trajectory) and
finding optimal sequence of actuations (using Ipopt solver) to achieve a smooth ride.

![Result](images/mpc_30mph.gif)



## The Model

### State
State of the system contains following five attributes:

- (x, y)  coordinates of position of car
- Car orientation compared to reference trajectory $\psi$
- Cross track error
- Error in car orientation with respect to reference trajectory

### Actuators
The car's motion is controlled via throttle and steering angle as actuators.


### Update Equations

![Update Equations](images/mpc_model.png)


### Constraints

![Constraints](images/mpc_constraints.png)

### Objective

The objective is to achieve a smoother ride while staying close to the reference
states of trajectory and velocity by:

- Minimizing the use of actuators.
- Minimizing the value gap between sequential actuations inorder to avoid a jerky
  ride (i.e. to get a smoother transition between states)
- Minimizing total changes in state


### Choice Of Parameters

- N = 20, dt = .05 : these are chosen by trial and error from simulation tests, following guideline that smaller dt is better, and ```T = N x dt```

- The multipliers in objective function are chosen by trial and error 


## Latency

Latency is handled by applying update equations (see above) to the  current state to estimate car state 100ms in future.


## Parameters

- The reference velocity is read from `velocity.txt`, and this can be updated while the simulation is running, which allows online testing.

- The weights/penalties in optimization objective are read from `penalties.txt`.
  These are space delimited, specified in the same order in which they appear in the objective function. These are also updated online (read at every update) and can be changed while the simulation is running.
