# 2D-Rocket-Landing

## Overview
The `2D-Rocket-Landing` project focuses on modeling and controlling a two-dimensional (2D) rocket system operating in a planar environment. This repository outlines the plant (the rocket system), the control objectives, and a high-level description of the system architecture. The emphasis is on designing a control strategy to achieve a safe and precise landing under gravitational influence, leveraging energy-based principles.

## Plant
The system under consideration is a 2D rocket characterized by three degrees of freedom (DOFs):
- **Translational Motion**: Movement along the $x$-axis (horizontal) and $y$-axis (vertical) in the 2D plane.
- **Rotational Motion**: Rotation about the axis normal to the plane (typically the $z$-axis in a 3D context, but constrained to a single angular DOF in 2D), denoted as $\theta$.

The rocket is modeled as a rigid body with a mass $m$ and a characteristic length $l$, resembling an inverted pendulum in its dynamic behavior. It is equipped with a single rotatable thruster mounted at its base (bottom). This thruster serves as the primary actuation mechanism, capable of:
- Generating a thrust force of variable magnitude.
- Adjusting its orientation relative to the rocket’s body to direct the thrust vector at an angle.

This configuration allows the rocket to manipulate both its translational position and rotational orientation within the 2D plane, providing the necessary control authority to achieve the desired landing objectives.

### Coordinate System and Variables
- $x$: Horizontal position of the center of mass (positive right).
- $y$: Vertical position of the center of mass (positive up).
- $\theta$: Orientation of the rocket centerline, measured clockwise from the vertical ($+y$-axis), so $\theta = 0$ is upright.
- $\phi$: Thrust angle, measured counterclockwise from the rocket centerline.
- $T$: Thrust magnitude, applied at the bottom of the rocket.
- $m$: Mass, concentrated at the center of mass.
- $l$: Rocket length.
- $J$: Moment of inertia about the center of mass (e.g., $J = \frac{m l^2}{12}$ for a uniform rod, or $J = m \left(\frac{l}{2}\right)^2 = \frac{m l^2}{4}$ for a point mass at $l/2$).
- $g$: Gravitational acceleration (positive downward).

### Equations of Motion
The system’s dynamics are governed by Newton’s laws for translation and rotation. Thrust is applied at the bottom, offset $l/2$ from the center of mass, with components influenced by both $\theta$ and $\phi$.

$$
\ddot{x} = \frac{T \sin(\theta + \phi)}{m} \\;
\ddot{y} = \frac{T \cos(\theta + \phi)}{m} - g \\;
\ddot{\theta} = \frac{T \sin(\phi) \cdot l}{2 J} 
$$

### State-Space Representation
$$
S = [x, y, \theta, \dot{x}, \dot{y}, \dot{\theta}],
$$
$$
\dot{S} = \begin{bmatrix}
\dot{x} \\
\dot{y} \\
\dot{\theta} \\
\frac{T \sin(\theta + \phi)}{m} \\
\frac{T \cos(\theta + \phi)}{m} - g \\
\frac{T \sin(\phi) \cdot l}{2 J}
\end{bmatrix}.
$$

### Action Space
$$
a = \begin{bmatrix}
T \\
\phi \\
\end{bmatrix}.
$$

### Notes
- The system is nonlinear due to the trigonometric terms $\sin(\theta - \phi)$, $\cos(\theta - \phi)$, and $\sin(\phi)$.
- Control inputs $T$ and $\phi$ allow manipulation of all degrees of freedom, though the system is underactuated (2 inputs, 3 DOFs).
- Goal: Drive $S = [x, y, \theta, \dot{x}, \dot{y}, \dot{\theta}]$ to $[0, 0, 0, 0, 0, 0]$ for a vertical landing at the origin.

## Goal
The primary objective of this project is to design and implement an energy-based Lyapunov controller to guide the rocket during its descent under gravity. The controller must:
- Regulate the thrust force magnitude and the thruster’s angular orientation.
- Ensure the rocket transitions from an arbitrary initial state in the sky (e.g., falling with non-zero velocity and orientation) to a stable landing configuration on the ground.
- Achieve a soft landing, defined as reaching a target position (typically $y = 0$, with $x$ at a designated landing site) with zero velocity and a controlled orientation (e.g., upright).

The Lyapunov-based approach leverages the system’s energy (kinetic and potential) to construct a control law that guarantees stability and convergence to the desired state, optimizing the rocket’s trajectory for safety and efficiency.

## Description of the Whole System
The 2D rocket operates in a gravitational field, descending toward the ground under the influence of a constant gravitational acceleration $g$ acting along the negative $y$-direction. The system is conceptualized as a planar inverted pendulum with a controllable base, where the thruster’s action mimics the pivot control of a pendulum, extended to two spatial dimensions.

### State Variables
The rocket’s state is fully described by six variables, capturing its translational and rotational behavior:
- $x$: Position along the horizontal axis (inertial frame).
- $y$: Position along the vertical axis (inertial frame), with $y = 0$ representing ground level.
- $\dot{x}$ (or $v_x$): Velocity in the $x$-direction.
- $\dot{y}$ (or $v_y$): Velocity in the $y$-direction.
- $\theta$: Angular position, representing the orientation of the rocket’s longitudinal axis relative to the inertial $x$-axis (counterclockwise positive).
- $\dot{\theta}$ (or $\omega$): Angular velocity about the normal to the plane.

These state variables define the rocket’s configuration and motion at any instant, providing a complete representation of its phase space.

### Actions 
The rocket is actuated through two control inputs applied via the thruster at its base:
- **Thrust Force ($F$)**: The magnitude of the force generated by the thruster, directed along the rocket’s thruster axis (adjusted by $\theta$). This force influences both $x$- and $y$-motion based on its orientation.
- **Thruster Angle ($\theta$)**: Causes the rotational torque about the rocket’s center of mass.
The torque ($\tau$) induced either by the thruster’s angular adjustment or additional control mechanisms (e.g., offset thrusters). This controls the rate of change of $\theta$.

In practice, the thruster’s orientation may be parameterized as an angle relative to the rocket’s body, but here, $\tau$ encapsulates the net rotational effect, while $F$ is modulated in magnitude and direction via $\theta$.

### System Behavior
Initially, the rocket is in free fall, subject to gravity, with arbitrary initial conditions for $x$, $y$, $\dot{x}$, $\dot{y}$, $\theta$, and $\dot{\theta}$. The control system activates the thruster to:
- Counteract gravitational acceleration.
- Adjust the rocket’s trajectory to align with the landing target.
- Stabilize its orientation for a vertical or near-vertical landing.

The interplay between $F$ and $\tau$ allows the controller to balance translational and rotational dynamics, ensuring the rocket lands safely at $(x_{\text{target}}, 0)$ with $\dot{x} = 0$, $\dot{y} = 0$, and an appropriate $\theta$ (e.g., $\theta = \frac{\pi}{2}$ for upright landing).

### Implementation Notes
This repository will serve as a foundation for simulating and testing the Lyapunov controller. Future sections may include simulation code and control law derivations, all aimed at achieving the outlined landing objective.
