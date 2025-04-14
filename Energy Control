```latex
\documentclass{article}
\usepackage{amsmath}

\begin{document}

\section*{Derivation of Energy Terms and Lyapunov Function}

\subsection*{System Dynamics}
The dynamics of the 2D rocket system are given by:
\begin{align}
\ddot{x} &= \frac{T \sin(\phi + \theta)}{m}, \label{eq:x_ddot} \\
\ddot{y} &= \frac{T \cos(\phi + \theta)}{m} - g, \label{eq:y_ddot} \\
\ddot{\theta} &= \frac{T l \sin(\phi)}{2 J}, \label{eq:theta_ddot}
\end{align}
where:
\begin{itemize}
    \item \( x, y \): Position coordinates of the rocket's center of mass (m),
    \item \( \theta \): Angle of the rocket from the vertical (rad),
    \item \( \dot{x}, \dot{y}, \dot{\theta} \): Velocities corresponding to \( x, y, \theta \),
    \item \( T \): Thrust magnitude (N),
    \item \( \phi \): Thrust angle relative to the rocket's axis (rad),
    \item \( m \): Mass of the rocket (kg),
    \item \( l \): Length from center of mass to thrust point (m),
    \item \( J \): Moment of inertia about the center of mass (kg·m\(^2\)),
    \item \( g \): Gravitational acceleration (m/s\(^2\)).
\end{itemize}

\subsection*{Total Energy}
The total energy of the system, \( E_{\text{tot}} \), is defined as the sum of kinetic and potential energies:
\begin{align}
E_{\text{tot}} &= \text{Kinetic Energy} + \text{Potential Energy}.
\end{align}

The kinetic energy includes contributions from translational motion in \( x \) and \( y \) directions and rotational motion:
\begin{align}
\text{Kinetic Energy} &= \frac{1}{2} m \dot{x}^2 + \frac{1}{2} m \dot{y}^2 + \frac{1}{2} J \dot{\theta}^2.
\end{align}

The potential energy is due to the gravitational potential at height \( y \):
\begin{align}
\text{Potential Energy} &= m g y.
\end{align}

Thus, the total energy is:
\begin{align}
E_{\text{tot}} &= \frac{1}{2} \left( J \dot{\theta}^2 + m \dot{x}^2 + m \dot{y}^2 \right) + m g y. \label{eq:E_tot}
\end{align}

\subsection*{Lyapunov Function}
The Lyapunov function is defined as:
\begin{align}
L &= -\frac{1}{2} E_{\text{tot}}^2. \label{eq:L}
\end{align}
This function is non-positive (\( L \leq 0 \)) since \( E_{\text{tot}}^2 \geq 0 \), and \( L = 0 \) when \( E_{\text{tot}} = 0 \). The choice of a negative quadratic suggests the control objective is to drive \( E_{\text{tot}} \) to zero, which may correspond to a specific equilibrium depending on the desired state.

\subsection*{Time Derivative of the Lyapunov Function}
To analyze stability, compute the time derivative of \( L \):
\begin{align}
\dot{L} &= \frac{dL}{dt} = \frac{d}{dt} \left( -\frac{1}{2} E_{\text{tot}}^2 \right).
\end{align}
Using the chain rule:
\begin{align}
\dot{L} &= -\frac{1}{2} \cdot 2 E_{\text{tot}} \cdot \dot{E}_{\text{tot}} = -E_{\text{tot}} \dot{E}_{\text{tot}}. \label{eq:L_dot_initial}
\end{align}

We need \( \dot{E}_{\text{tot}} \), the time derivative of the total energy:
\begin{align}
E_{\text{tot}} &= \frac{1}{2} J \dot{\theta}^2 + \frac{1}{2} m \dot{x}^2 + \frac{1}{2} m \dot{y}^2 + m g y.
\end{align}
Differentiate with respect to time:
\begin{align}
\dot{E}_{\text{tot}} &= \frac{\partial E_{\text{tot}}}{\partial \dot{\theta}} \cdot \ddot{\theta} + \frac{\partial E_{\text{tot}}}{\partial \dot{x}} \cdot \ddot{x} + \frac{\partial E_{\text{tot}}}{\partial \dot{y}} \cdot \ddot{y} + \frac{\partial E_{\text{tot}}}{\partial y} \cdot \dot{y}.
\end{align}
Compute each partial derivative:
\begin{align}
\frac{\partial E_{\text{tot}}}{\partial \dot{\theta}} &= J \dot{\theta}, \\
\frac{\partial E_{\text{tot}}}{\partial \dot{x}} &= m \dot{x}, \\
\frac{\partial E_{\text{tot}}}{\partial \dot{y}} &= m \dot{y}, \\
\frac{\partial E_{\text{tot}}}{\partial y} &= m g.
\end{align}
Thus:
\begin{align}
\dot{E}_{\text{tot}} &= J \dot{\theta} \ddot{\theta} + m \dot{x} \ddot{x} + m \dot{y} \ddot{y} + m g \dot{y}. \label{eq:E_dot_terms}
\end{align}

Substitute the dynamics from equations \eqref{eq:x_ddot}, \eqref{eq:y_ddot}, and \eqref{eq:theta_ddot}:
\begin{align}
\ddot{x} &= \frac{T \sin(\phi + \theta)}{m}, \\
\ddot{y} &= \frac{T \cos(\phi + \theta)}{m} - g, \\
\ddot{\theta} &= \frac{T l \sin(\phi)}{2 J}.
\end{align}
Plug into \eqref{eq:E_dot_terms}:
\begin{align}
\dot{E}_{\text{tot}} &= J \dot{\theta} \cdot \frac{T l \sin(\phi)}{2 J} + m \dot{x} \cdot \frac{T \sin(\phi + \theta)}{m} + m \dot{y} \cdot \left( \frac{T \cos(\phi + \theta)}{m} - g \right) + m g \dot{y}.
\end{align}
Simplify each term:
\begin{itemize}
    \item Rotational term:
    \[
    J \dot{\theta} \cdot \frac{T l \sin(\phi)}{2 J} = \frac{T l \dot{\theta} \sin(\phi)}{2}.
    \]
    \item \( x \)-translational term:
    \[
    m \dot{x} \cdot \frac{T \sin(\phi + \theta)}{m} = T \dot{x} \sin(\phi + \theta).
    \]
    \item \( y \)-translational term:
    \[
    m \dot{y} \cdot \left( \frac{T \cos(\phi + \theta)}{m} - g \right) = T \dot{y} \cos(\phi + \theta) - m g \dot{y}.
    \]
    \item Potential term:
    \[
    m g \dot{y}.
    \]
\end{itemize}
Combine:
\begin{align}
\dot{E}_{\text{tot}} &= \frac{T l \dot{\theta} \sin(\phi)}{2} + T \dot{x} \sin(\phi + \theta) + T \dot{y} \cos(\phi + \theta) - m g \dot{y} + m g \dot{y}.
\end{align}
The \( -m g \dot{y} + m g \dot{y} \) terms cancel:
\begin{align}
\dot{E}_{\text{tot}} &= T \left[ \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta) \right]. \label{eq:E_dot}
\end{align}

Substitute into \eqref{eq:L_dot_initial}:
\begin{align}
\dot{L} &= -E_{\text{tot}} \cdot T \left[ \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta) \right]. \label{eq:L_dot}
\end{align}

\subsection*{Control Derivation}
To achieve stability, we want \( \dot{L} \leq 0 \). Since \( L = -\frac{1}{2} E_{\text{tot}}^2 \leq 0 \), stability requires \( \dot{L} \geq 0 \) (so \( L \) increases toward 0, reducing \( |E_{\text{tot}}| \)). Define:
\begin{align}
u &= \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta), \label{eq:u}
\end{align}
so:
\begin{align}
\dot{L} &= -E_{\text{tot}} T u. \label{eq:L_dot_u}
\end{align}
To make \( \dot{L} \geq 0 \):
\begin{itemize}
    \item If \( E_{\text{tot}} > 0 \), choose \( T u \leq 0 \).
    \item If \( E_{\text{tot}} < 0 \), choose \( T u \geq 0 \).
\end{itemize}
Assume a control law for \( T \):
\begin{align}
T &= k \cdot \text{sign}(-E_{\text{tot}}) \cdot |u|, \label{eq:T_control}
\end{align}
where \( k > 0 \) is a gain, and \( \text{sign}(-E_{\text{tot}}) \) ensures the correct direction:
\begin{itemize}
    \item If \( E_{\text{tot}} > 0 \), \( \text{sign}(-E_{\text{tot}}) = -1 \), so \( T u = -k |u| u \leq 0 \).
    \item If \( E_{\text{tot}} < 0 \), \( \text{sign}(-E_{\text{tot}}) = 1 \), so \( T u = k |u| u \geq 0 \).
\end{itemize}
Thus:
\begin{align}
\dot{L} &= -E_{\text{tot}} \cdot k \cdot \text{sign}(-E_{\text{tot}}) \cdot |u| \cdot u.
\end{align}
Since \( |u| \geq 0 \), evaluate:
\begin{itemize}
    \item If \( E_{\text{tot}} > 0 \):
    \[
    \dot{L} = -E_{\text{tot}} \cdot (-k |u| u) = k E_{\text{tot}} |u| u.
    \]
    Need \( u \geq 0 \), or adjust \( \phi \).
    \item If \( E_{\text{tot}} < 0 \):
    \[
    \dot{L} = -E_{\text{tot}} \cdot (k |u| u) = -k |E_{\text{tot}}| |u| u.
    \]
    Need \( u \leq 0 \).
\end{itemize}
Choose \( \phi \) to align \( u \):
\begin{align}
\sin(\phi + \theta) &= -\frac{\dot{x}}{\sqrt{\dot{x}^2 + \dot{y}^2}}, \quad \cos(\phi + \theta) &= -\frac{\dot{y}}{\sqrt{\dot{x}^2 + \dot{y}^2}}, \label{eq:phi_choice}
\end{align}
so:
\begin{align}
u &= \frac{l \dot{\theta} \sin(\phi)}{2} - \dot{x} \cdot \frac{\dot{x}}{\sqrt{\dot{x}^2 + \dot{y}^2}} - \dot{y} \cdot \frac{\dot{y}}{\sqrt{\dot{x}^2 + \dot{y}^2}}.
\end{align}
If \( \dot{\theta} \approx 0 \):
\begin{align}
u &\approx -\sqrt{\dot{x}^2 + \dot{y}^2} \leq 0.
\end{align}
Then:
\begin{align}
T &= k |E_{\text{tot}}|, \label{eq:T_final}
\end{align}
ensuring:
\begin{align}
\dot{L} &= k |E_{\text{tot}}| \cdot |u| \cdot (-E_{\text{tot}}) = -k |E_{\text{tot}}| \cdot |u| \cdot E_{\text{tot}} \leq 0.
\end{align}
Adjust \( \phi \) if \( u > 0 \):
\begin{align}
\phi \to \phi + \pi.
\end{align}

\end{document}
```
