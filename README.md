# Damped-Pendulum
Project Report:

A pendulum is a simple mechanical system often introduced in basic physics courses to illustrate principles of harmonic motion, gravitational acceleration, and energy conservation. In an idealized, frictionless environment, a pendulum would oscillate indefinitely, with constant total mechanical energy. However, real-world pendulums experience energy loss due to damping—resistive forces such as air friction or internal friction in the pivot. Modeling a damped pendulum allows us to analyze how energy dissipates over time and how the system settles into equilibrium.

This project implements a numerical simulation of a damped pendulum in MATLAB. The code integrates the equations of motion for a pendulum under the influence of gravity and a damping torque. It prompts the user for key parameters (gravity, pendulum length, damping coefficient, initial angle, total simulation time, and time step) and produces a dynamic, animated plot of the pendulum’s motion. Additionally, it calculates and displays the total mechanical energy of the system at each time step, showing how the energy decreases over time due to damping.

My 5 objectives were:

Physical Modeling: Represent the equations of motion for a damped pendulum in a computational framework.

Numerical Integration: Use a time-stepping method (Euler’s method) to solve the ordinary differential equations (ODEs).

Visualization: Animate the pendulum’s motion and display the trajectory as it slows and returns toward equilibrium.

Energy Analysis: Compute the total mechanical energy (potential + kinetic) at each time step and illustrate how damping reduces energy over time.

Modularity and Clarity: Structure the code into separate functions for computing gravitational torque, damping torque, and updating the state

To actually implement the physical model I had to use equations of motion.

Consider a pendulum of length L and mass m (assumed to be 1 kg for simplicity) swinging under gravity g. Let θ be the angular displacement from the vertical. The governing equation of motion is:

Id^2θ/dt^2​ = Tnet​
The moment of inertia for a point mass at the end of a massless rod is I=mL^2=L^2 if m=1.
The net torque Tnet consists of:
1. Gravitational torque: Tg=−gLsin⁡(θ)
2. Damping torque: Td=−cdθ/dt​, where cis the damping coefficient.
Using the above knowledge we then know,

d^2θ/dt^2​ = (Tg+Td)/L^2 = (-gLsin(θ)-cdθ/dt)/L^2
Which can simplify to,

d^2θ/dt^2 =-gsin(θ)/L -cdθ/L^2dt
When considering total mechanical energy, E, I had to consider the effects of kinetic energy, potential energy, and the damping torque against the motion of the system.

Kinetic Energy: K = m(v^2)/2, for rotation, v = Ldθ/dt, which simplifies to K = (L^2(dθ/dt)^2)/2
Potential Energy: U = mgh, with defining the zero of potential energy at the equilibrium (lowest) point, h=L(1−cos⁡(θ)). With m=1: U = gL(1−cos(θ))
Therefore total energy equation becomes:

E = K+U = (L^2(dθ/dt)^2)/2 + gL(1−cos(θ))

As the simulation proceeds, the damping torque does work against the motion, removing energy from the system. The result is a decreasing total mechanical energy profile over time
To finally tackle the problem of time integration I used Eulers Method for time step dt:

θn+1 = θn + dt * dθ/dt|n
dθ/dt|n+1 = dθ/dt|n + dt * d^2θ/dt^2|n
While Euler’s method is not as accurate as more advanced methods, implementing time steps in this way is a simple and easier way to illustrate the key concepts of the program.
Code Breakdown:

Main script (damped_pendulum_simulation.m):
Sets initial conditions and preallocates arrays.
Uses a loop to update θ and dθ/dt
Computes positions (x, y) of the pendulum bob for plotting.
Calculates energy at each step and stores the results.
Animates the pendulum motion and plots the energy versus time.
Functions:
computeGravitationalTorque(angle, g, L): Returns the gravitational torque given angle, gravity, and length.
computeDampingTorque(angularVelocity, dampingCoefficient): Returns the damping torque.
updatePendulumState(angle, angularVelocity, g, L, dampingCoefficient, dt): Updates the angle and angular velocity using Euler’s method.
Running the simulation reveals the characteristic behavior of a damped pendulum:
Initial Motion and Damping Effects:
The pendulum starts swinging from its initial angle. Due to the damping torque, the amplitude of oscillation decreases with each subsequent swing. Over time, the pendulum approaches its equilibrium (vertical) position.
Energy Dissipation:
By plotting the total mechanical energy over time, we see a clear and steady decline. Initially, the energy is some combination of potential (at the turning points) and kinetic (as it passes through the bottom). As damping does work against the system, energy is lost to the environment, causing the total mechanical energy to decrease until it nearly plateaus at a low value when the pendulum is barely moving.
Parameter Sensitivity:
Changing parameters, such as the damping coefficient c, gravity g, or the length L, affects the rate at which energy is lost and how quickly the pendulum settles. A higher damping coefficient leads to faster energy dissipation and a quicker return to equilibrium, while a lower damping coefficient prolongs the oscillations but still results in gradual energy loss.

References:
MATLAB Documentation (for basic plotting, input/output, and numerical methods)
Standard numerical analysis texts for reference on Euler’s method and ODE solving
