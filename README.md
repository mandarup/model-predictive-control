# Model Predictive Control


## The Model

### State
State of the system contains following five attributes:

- x, y  coordinates of position of car
- car orientation compared to reference trajectory $\psi$
- Cross track error
- Error in car orientation with respect to reference trajectory

### Actuators
The car's motion is controlled via throttle and steering angle as actuators.


### Update Equations
\begin{align}
    & x_{t+1} = x_t + v_t * cos(\psi_t) * dt \\
\end{align}
