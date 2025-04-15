## Rocket System Analysis

### System Dynamics

The dynamics of the 2D rocket system are:

$$
\ddot{x} = \frac{T \sin(\phi + \theta)}{m},
$$

$$
\ddot{y} = \frac{T \cos(\phi + \theta)}{m} - g,
$$

$$
\ddot{\theta} = \frac{T l \sin(\phi)}{2 J},
$$

where:
- $x, y$: Position coordinates (m),
- $\theta$: Angle from vertical (rad),
- $T$: Thrust magnitude (N),
- $\phi$: Thrust angle relative to rocket axis (rad),
- $m$: Mass (kg),
- $l$: Length to thrust point (m),
- $J$: Moment of inertia (kg·m²),
- $g$: Gravitational acceleration (m/s²).

### Total Energy

The total energy $E_{\text{tot}}$ is the sum of kinetic and potential energies:

$$
E_{\text{tot}} = \text{Kinetic Energy} + \text{Potential Energy}.
$$

Kinetic energy:

$$
\text{Kinetic Energy} = \frac{1}{2} m \dot{x}^2 + \frac{1}{2} m \dot{y}^2 + \frac{1}{2} J \dot{\theta}^2.
$$

Potential energy:

$$
\text{Potential Energy} = m g y.
$$

Thus:

$$
E_{\text{tot}} = \frac{1}{2} \left( J \dot{\theta}^2 + m \dot{x}^2 + m \dot{y}^2 \right) + m g y.
$$

### Lyapunov Function

The Lyapunov function is:

$$
L = \frac{1}{2} E_{\text{tot}}^2.
$$

Since $E_{\text{tot}}^2 \geq 0$, $L \geq 0$, with $L = 0$ when $E_{\text{tot}} = 0$.

### Time Derivative of Lyapunov Function

Compute:

$$
\dot{L} = \frac{d}{dt} \left( \frac{1}{2} E_{\text{tot}}^2 \right) = E_{\text{tot}} \dot{E}_{\text{tot}}.
$$

For $\dot{E}_{\text{tot}}$:

$$
E_{\text{tot}} = \frac{1}{2} J \dot{\theta}^2 + \frac{1}{2} m \dot{x}^2 + \frac{1}{2} m \dot{y}^2 + m g y,
$$

$$
\dot{E}_{\text{tot}} = J \dot{\theta} \ddot{\theta} + m \dot{x} \ddot{x} + m \dot{y} \ddot{y} + m g \dot{y}.
$$

Substitute dynamics:

$$
\ddot{x} = \frac{T \sin(\phi + \theta)}{m}, \quad \ddot{y} = \frac{T \cos(\phi + \theta)}{m} - g, \quad \ddot{\theta} = \frac{T l \sin(\phi)}{2 J}.
$$

$$
\dot{E}_{\text{tot}} = J \dot{\theta} \cdot \frac{T l \sin(\phi)}{2 J} + m \dot{x} \cdot \frac{T \sin(\phi + \theta)}{m} + m \dot{y} \cdot \left( \frac{T \cos(\phi + \theta)}{m} - g \right) + m g \dot{y}.
$$

Simplify:

$$
= \frac{T l \dot{\theta} \sin(\phi)}{2} + T \dot{x} \sin(\phi + \theta) + T \dot{y} \cos(\phi + \theta) - m g \dot{y} + m g \dot{y},
$$

$$
\dot{E}_{\text{tot}} = T \left[ \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta) \right].
$$

Thus:

$$
\dot{L} = E_{\text{tot}} T \left[ \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta) \right].
$$

### Control Derivation

Define:

$$
u = \frac{l \dot{\theta} \sin(\phi)}{2} + \dot{x} \sin(\phi + \theta) + \dot{y} \cos(\phi + \theta),
$$

so:

$$
\dot{L} = -E_{\text{tot}} T u.
$$

Since $L \leq 0$, aim for $\dot{L} \geq 0$:
- If $E_{\text{tot}} > 0$, require $T u \leq 0$.
- If $E_{\text{tot}} < 0$, require $T u \geq 0$.

Choose $\phi$:

$$
\sin(\phi + \theta) = -\frac{\dot{x}}{\sqrt{\dot{x}^2 + \dot{y}^2}}, \quad \cos(\phi + \theta) = -\frac{\dot{y}}{\sqrt{\dot{x}^2 + \dot{y}^2}}.
$$

Then, if $\dot{\theta} \approx 0$:

$$
u \approx -\sqrt{\dot{x}^2 + \dot{y}^2} \leq 0.
$$

Set:

$$
T = k |E_{\text{tot}}|,
$$

where $k > 0$, so:

$$
\dot{L} = -E_{\text{tot}} \cdot k |E_{\text{tot}}| \cdot u \geq 0,
$$

since $u \leq 0$. If $u > 0$, adjust:

$$
\phi \to \phi + \pi.
$$

