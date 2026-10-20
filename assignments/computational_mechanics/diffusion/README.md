#

## Summary

## Mathematical Model

Forward:
$$\frac{d\Phi}{dx} \approx \frac{\Phi_{i+1} - \Phi_i}{\Delta x}$$

Backward:
$$\frac{d\Phi}{dx} \approx \frac{\Phi_i - \Phi_{i-1}}{\Delta x}$$

Central:
$$\frac{d\Phi}{dx} \approx \frac{\Phi_{i+1} - \Phi_{i-1}}{2\Delta x}$$

$$\Phi(x_{i+1}) = \Phi(x_i + \Delta x) = \Phi_{i+1}$$

$$\Phi(x_i + \Delta x) = \Phi(x_i) + \frac{d\Phi}{dx}\Delta x + \frac{d^2\Phi}{dx^2}\frac{\Delta x^2}{2} + \frac{d^3\Phi}{dx^3}\frac{\Delta x^3}{6} + \dots$$

$$\Rightarrow \Phi(x_i + \Delta x) - \Phi(x_i) = \frac{d\Phi}{dx}\Delta x + \frac{d^2\Phi}{dx^2}\frac{\Delta x^2}{2} + \dots$$

$$\Rightarrow \frac{\Phi(x_i + \Delta x) - \Phi(x_i)}{\Delta x} = \frac{d\Phi}{dx} + \left(\frac{d^2\Phi}{dx^2}\frac{\Delta x}{2} + \dots\right)$$

$$\frac{d\Phi}{dx} = \frac{\Phi(x_i + \Delta x) - \Phi(x_i)}{\Delta x} = \frac{\Phi_{i+1} - \Phi_i}{\Delta x}$$

$$\Phi(x_i - \Delta x) = \Phi(x_i) - \frac{d\Phi}{dx}\Delta x + \frac{d^2\Phi}{dx^2}\frac{\Delta x^2}{2} - \dots$$

$$\Rightarrow \frac{d^2\Phi}{dx^2} = \frac{\Phi_{i+1} - 2\Phi_i + \Phi_{i-1}}{\Delta x^2}$$

---

$$\frac{d\Phi}{dx} = 6x + \frac{d^2\Phi}{dx^2}$$

Assume:
$$u \cdot \frac{d\Phi}{dx} = 0$$

Now:
$$\frac{d^2\Phi}{dx^2} = \pm 6x$$

$$\frac{\Phi_{i+1} - 2\Phi_i + \Phi_{i-1}}{\Delta x^2}$$

Grid: $x_0, x_1, x_2, x_3, x_4$ with step $\Delta x = 0.25$

Boundary conditions:
$$\Phi(0) = 1$$
$$\left.\frac{d\Phi}{dx}\right|_{x=1} = 0$$

Equations:

1. $\Phi_2 - 2\Phi_1 + \Phi_0 = 6 \times 0.25^3$
2. $\Phi_3 - 2\Phi_2 + \Phi_1 = 6 \times 0.5 \times 0.25^2$
3. $\Phi_4 - 2\Phi_3 + \Phi_2 = 6 \times 0.75 \times 0.25^2$
4. $\Phi_0 = 1$
5. $\Phi_4 - \Phi_3 = 0$

System of equations formulation:

- $1\Phi_0 + 0\Phi_1 + 0\Phi_2 + 0\Phi_3 + 0\Phi_4 = 1$
- $1\Phi_0 - 2\Phi_1 + 1\Phi_2 + 0\Phi_3 + 0\Phi_4 = 0.09375$
- $0\Phi_0 + 1\Phi_1 - 2\Phi_2 + 1\Phi_3 + 0\Phi_4 = 0.1875$
- $0\Phi_0 + 0\Phi_1 + 1\Phi_2 - 2\Phi_3 + 1\Phi_4 = 0.28125$
- $0\Phi_0 + 0\Phi_1 + 0\Phi_2 - 1\Phi_3 + 1\Phi_4 = 0$

---

Matrix representation:

$$
\begin{bmatrix}
1 & 0 & 0 & 0 & 0 \\
1 & -2 & 1 & 0 & 0 \\
0 & 1 & -2 & 1 & 0 \\
0 & 0 & 1 & -2 & 1 \\
0 & 0 & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
u_0 \\
u_1 \\
u_2 \\
u_3 \\
u_4
\end{bmatrix}
=
\begin{bmatrix}
1 \\
0.09375 \\
0.1875 \\
0.28125 \\
0
\end{bmatrix}
$$

- Error minimized at Dirichlet because we know the exact soln, but Neumann error maximized because we have the slope, not exact soln.

- Convection with finite differences:
  $$\frac{\partial u}{\partial t} + u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y} = -\frac{1}{\rho}\frac{\partial P}{\partial x} + g_x + \nu\left(\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2}\right)$$

- Convection - flow direction; Diffusion - scattered.

$$3\frac{d^2\Phi}{dx^2} = 75\frac{d\Phi}{dx} - 8x$$
_(Diffusion term = Convection term $\to$ positive (left to right side))_

$$\Rightarrow 3\frac{\Phi_{i+1} - 2\Phi_i + \Phi_{i-1}}{\Delta x^2} = 75\frac{\Phi_{i+1} - \Phi_{i-1}}{2\Delta x} - 8x_i$$

---

$$\Rightarrow \left(\frac{3}{\Delta x^2} - \frac{75}{2\Delta x}\right)\Phi_{i+1} - \frac{6}{\Delta x^2}\Phi_i + \left(\frac{3}{\Delta x^2} + \frac{75}{2\Delta x}\right)\Phi_{i-1} = -8x_i$$

**Stability:** Sometimes it might happen that we end up with some oscillations in our solution, and this is weird.

- _Cause:_ Improper numerical simulation condition. Example: for diffusion we can use the central difference method, but for convection we can't use it. Rather we have to choose forward or backward difference method based on convection coefficient $\left(K\frac{d\Phi}{dx}\right)$.
- If $K$ is positive, that means the flow is going from left to right and we have to use backward scheme, whereas if $K$ is negative, we have to use forward difference scheme.

- Using central difference scheme, if we increase the number of grid points, it might happen that the numerical solution matches with exact solution and can be stable. This is not always practical.

---

**Peclet Number ($Pe$):**
$$Pe = \frac{u \Delta x}{K}$$
_(where $K$ is the diffusion constant)_

If $Pe < 2$ and we use central difference scheme, then we are going to have a stable solution.

- Another way to choose numerical scheme that is more consistent with our underlying physics: (backward if $\rightarrow$, forward if $\leftarrow$).
- _Downside:_ Lose some accuracy and solution is 1st order accurate. Solution: using higher order upwinding to preserve accuracy.

**2D Diffusion:**
$$\frac{\partial^2\Phi}{\partial x^2} + \frac{\partial^2\Phi}{\partial y^2} = 0$$

$$\frac{\Phi_{i+1,j} - 2\Phi_{i,j} + \Phi_{i-1,j}}{\Delta x^2} + \frac{\Phi_{i,j+1} - 2\Phi_{i,j} + \Phi_{i,j-1}}{\Delta y^2} = 0$$

$$\Rightarrow \frac{1}{\Delta^2}(\Phi_{i+1,j} + \Phi_{i-1,j} + \Phi_{i,j+1} + \Phi_{i,j-1} - 4\Phi_{i,j}) = 0$$

Grid indexing layout: $(i,j)$ 2D coordinates converted to 1D index array mapping.

---

$$ID = j \times N_x + i + 1$$ _(only works if using left-to-right numbering)_

$$3\left(\frac{\partial^2\Phi}{\partial x^2} + \frac{\partial^2\Phi}{\partial y^2}\right) = 7xy$$

$$\Rightarrow 3\left(\frac{\Phi_{i+1,j} - 2\Phi_{i,j} + \Phi_{i-1,j}}{\Delta x^2} + \frac{\Phi_{i,j+1} - 2\Phi_{i,j} + \Phi_{i,j-1}}{\Delta y^2}\right) = 7x_i y_i$$

$$\Rightarrow \Phi_{i+1,j} + \Phi_{i-1,j} + \Phi_{i,j+1} + \Phi_{i,j-1} - 4\Phi_{i,j} = \frac{7}{3\Delta^2}x_i y_i$$

6 node equation:
$$\Phi_{2,1} + \Phi_{0,1} + \Phi_{1,0} + \Phi_{1,2} - 4\Phi_{1,1} = \frac{7}{3}\frac{x_1 y_1}{\Delta^2}$$

13 node equation:
$$\Phi_{4,2} + \Phi_{2,2} + \Phi_{3,1} + \Phi_{3,3} - 4\Phi_{3,2} = \frac{7}{3}\frac{x_3 y_3}{\Delta^2}$$

---

- Corner node's solution value doesn't affect the solution.

**Convection Finite Difference in 2D:**
$$u\frac{\partial\Phi}{\partial x} + v\frac{\partial\Phi}{\partial y} = K\left(\frac{\partial^2\Phi}{\partial x^2} + \frac{\partial^2\Phi}{\partial y^2}\right) + Q$$
_(Convection terms with directional coefficients $u, v$; Diffusion term with single coefficient $K$; Source term $Q$)_

- Convection can cause solution to become unstable.
- Stability condition:
  $$Pe_x = \frac{u\Delta x}{K} < 2, \quad Pe_y = \frac{v\Delta y}{K} < 2$$

$u > 0$ (left to right), $v > 0$ (bottom to top) $\rightarrow$ Upwinding: stable but less accurate.

Using central difference method for convection and diffusion:
$$u\frac{\Phi_{i+1,j} - \Phi_{i-1,j}}{2\Delta x} + v\frac{\Phi_{i,j+1} - \Phi_{i,j-1}}{2\Delta y} = K\left(\frac{\Phi_{i+1,j} - 2\Phi_{i,j} + \Phi_{i-1,j}}{\Delta x^2} + \frac{\Phi_{i,j+1} - 2\Phi_{i,j} + \Phi_{i,j-1}}{\Delta y^2}\right) + Q_{i,j}$$

---

Assuming $\Delta x = \Delta y = \Delta$, multiplying both sides by $\Delta$:

$$\frac{u\Delta}{2}(\Phi_{i+1,j} - \Phi_{i-1,j}) + \frac{v\Delta}{2}(\Phi_{i,j+1} - \Phi_{i,j-1}) = K(\Phi_{i+1,j} + \Phi_{i-1,j} + \Phi_{i,j+1} + \Phi_{i,j-1} - 4\Phi_{i,j}) + Q_{i,j}\Delta^2$$

$$\Rightarrow \left(\frac{u\Delta}{2} - K\right)\Phi_{i+1,j} + \left(-\frac{u\Delta}{2} - K\right)\Phi_{i-1,j} + \left(\frac{v\Delta}{2} - K\right)\Phi_{i,j+1} + \left(-\frac{v\Delta}{2} - K\right)\Phi_{i,j-1} + 4K\Phi_{i,j} = Q_{i,j}\Delta^2$$

**Cross-Stream Diffusion (False Diffusion):**
$$K_{\text{false}} = \frac{\sqrt{u^2 + v^2}\Delta x \Delta y \sin(2\theta)}{4(\Delta y \sin^3\theta + \Delta x \cos^3\theta)}$$

- $\theta = 45^\circ \Rightarrow K_{\text{false}}$ is maximum.
- Occurs because our finite difference for convection only accounts for single direction and grid lines are not aligned with velocity direction, leading to artificially increased diffusion in the problem.

---

### Finite Volume Method (FVM)

**Divergence Theorem:** Allows us to transform a regional integral to a boundary integral.

1D:
$$\int_a^b \frac{d\Phi}{dx} dx = \int_a^b d\Phi = \Phi(b) - \Phi(a)$$

2D:
$$\iint_A (\nabla \cdot \vec{u}) dA = \oint \vec{u} \cdot \hat{n} dS$$

3D:
$$\iiint_V \nabla \cdot \vec{u} dV = \iint_S \vec{u} \cdot \hat{n} dA$$

In Reynolds transport theorem, in order for any conserved quantity to appear within a control volume, it must cross a boundary. Divergence theorem also lowers order of derivatives in integrand by 1.

---

**General Conservation Equation (GCE) (Vector form):**
$$\frac{\partial\Phi}{\partial t} + \nabla \cdot (\vec{v}\Phi) = \nabla \cdot (\Gamma \nabla \Phi) + Q$$
_(Unsteady term + Convection term = Diffusion term + Source term)_

Assuming steady state $\frac{\partial\Phi}{\partial t} = 0$, and integrating over a FV cell (2D):
$$\iint_A \nabla \cdot (\vec{v}\Phi) dA = \iint_A \nabla \cdot (\Gamma \nabla \Phi) dA + \iint_A Q dA$$

$$\Rightarrow \oint \Phi(\vec{v} \cdot \hat{n}) dS = \oint \Gamma \nabla \Phi \cdot \hat{n} dS + \iint_A Q dA$$
_(Convective flux across boundary = Diffusive flux across boundary + Source)_

**Flux:** Transport of a certain quantity across a boundary. Can cross into/out of FV cell either through convection or diffusion.

---

**Trapezoidal Rules:**
1D:
$$\int_a^b f(x) dx \approx \frac{f(a) + f(b)}{2}(b - a)$$

Midpoint approximations:
$$\iint_A f(x,y) dA \approx f(x_c, y_c) A$$
$$\iiint_V f(x,y,z) dV \approx f(x_c, y_c, z_c) V$$
_(Accuracy: $O(\Delta x^2)$ - Second-order accurate)_

### Diffusion with FVM

Diffusion equation:
$$K \nabla \cdot (\nabla \Phi) = Q$$

$$\nabla \Phi = \left(\frac{\partial\Phi}{\partial x}, \frac{\partial\Phi}{\partial y}\right)$$

$$\nabla \cdot \nabla \Phi = \frac{\partial^2\Phi}{\partial x^2} + \frac{\partial^2\Phi}{\partial y^2}$$

1D Diffusion equation with FVM:
$$K \frac{d}{dx}\left(\frac{d\Phi}{dx}\right) = Q(x)$$

$$\int_{x_l}^{x_r} K \frac{d}{dx}\left(\frac{d\Phi}{dx}\right) dx = \int_{x_l}^{x_r} Q(x) dx$$

---

$$\Rightarrow K \int_{x_l}^{x_r} d\left(\frac{d\Phi}{dx}\right) = \int_{x_l}^{x_r} Q(x) dx$$

$$\Rightarrow K \left( \left.\frac{d\Phi}{dx}\right|_{x=x_r} - \left.\frac{d\Phi}{dx}\right|_{x=x_l} \right) = Q(x_c)(x_r - x_l)$$

Central difference approximations at boundaries $x_r, x_l$:
$$\left.\frac{d\Phi}{dx}\right|_{x=x_r} = \frac{\Phi_{i+1} - \Phi_i}{\Delta x}, \quad \left.\frac{d\Phi}{dx}\right|_{x=x_l} = \frac{\Phi_i - \Phi_{i-1}}{\Delta x}$$

$$K \left( \frac{\Phi_{i+1} - \Phi_i}{\Delta x} - \frac{\Phi_i - \Phi_{i-1}}{\Delta x} \right) = Q(x_c)(x_r - x_l)$$

$$\Rightarrow \Phi_{i+1} - 2\Phi_i + \Phi_{i-1} = \frac{Q(x_c)}{K}\Delta x^2$$

Since FVM stores solutions at cell centers, we no longer have solution values evaluated directly on the boundary.

---

### FVM: Dirichlet and Neumann Boundary Conditions

**Dirichlet BC on Left Side of Cell ($\Phi(x_l) = \Phi_0$):**
$$K \left( \left.\frac{d\Phi}{dx}\right|_{x=x_r} - \left.\frac{d\Phi}{dx}\right|_{x=x_l} \right) = Q(x_c)\Delta x$$

$$K \left( \frac{\Phi_{i+1} - \Phi_i}{\Delta x} - \frac{\Phi_i - \Phi_0}{\Delta x / 2} \right) = Q(x_c)\Delta x$$

$$\Rightarrow \Phi_{i+1} - 3\Phi_i = \frac{Q(x_c)}{K}\Delta x^2 - 2\Phi_0$$

**Dirichlet BC on Right Side ($\Phi(x_r) = \Phi_0$):**
$$K \left( \frac{\Phi_0 - \Phi_i}{\Delta x / 2} - \frac{\Phi_i - \Phi_{i-1}}{\Delta x} \right) = Q(x_c)\Delta x$$

$$\Rightarrow \Phi_{i-1} - 3\Phi_i = \frac{Q(x_c)}{K}\Delta x^2 - 2\Phi_0$$

**Neumann BC ($\left.\frac{d\Phi}{dx}\right|\_{\text{boundary}} = \gamma$):**
Left side:
$$K \left( \frac{\Phi_{i+1} - \Phi_i}{\Delta x} - \gamma \right) = Q(x_c)\Delta x$$

Right side:
$$K \left( \gamma - \frac{\Phi_i - \Phi_{i-1}}{\Delta x} \right) = Q(x_c)\Delta x$$

---

Example Problem:
$$3\frac{d^2\Phi}{dx^2} = 2x^2, \quad \left.\frac{d\Phi}{dx}\right|_{x=0} = 0, \quad \Phi(x=1) = 10$$

Standard interior cell:
$$\Phi_{i+1} - 2\Phi_i + \Phi_{i-1} = \frac{2x_i^2}{3}\Delta x^2$$

Cell 1 (Left Neumann BC):
$$3\left(\frac{\Phi_2 - \Phi_1}{\Delta x} - 0\right) = 2x_1^2 \Delta x \Rightarrow \Phi_2 - \Phi_1 = \frac{2}{3}x_1^2 \Delta x^2$$

Cell 4 (Right Dirichlet BC):
$$3\left(\frac{10 - \Phi_4}{\Delta x / 2} - \frac{\Phi_4 - \Phi_3}{\Delta x}\right) = 2x_4^2 \Delta x \Rightarrow \Phi_3 - 3\Phi_4 = \frac{2}{3}x_4^2 \Delta x^2 - 20$$

---

### 2D Diffusion Equation in FVM

$$\iint_A K \nabla \cdot \nabla \Phi dA = \iint_A Q(x,y) dA$$

$$\Rightarrow \oint K \nabla \Phi \cdot \hat{n} dS = Q(x_c, y_c)\Delta x \Delta y$$

Face normals:

- East ($e$): $\hat{n} = (1, 0)$
- North ($n$): $\hat{n} = (0, 1)$
- West ($w$): $\hat{n} = (-1, 0)$
- South ($s$): $\hat{n} = (0, -1)$

Evaluating flux terms:
$$\oint \nabla \Phi \cdot \hat{n} dS = \int_e \frac{\partial\Phi}{\partial x} dS + \int_n \frac{\partial\Phi}{\partial y} dS - \int_w \frac{\partial\Phi}{\partial x} dS - \int_s \frac{\partial\Phi}{\partial y} dS$$

Using Trapezoidal Rule:
$$\left(\frac{\partial\Phi}{\partial x}\right)_e \Delta y + \left(\frac{\partial\Phi}{\partial y}\right)_n \Delta x - \left(\frac{\partial\Phi}{\partial x}\right)_w \Delta y - \left(\frac{\partial\Phi}{\partial y}\right)_s \Delta x = \frac{Q(x_c,y_c)}{K}\Delta x \Delta y$$

---

Assuming $\Delta x = \Delta y$:
$$\left(\frac{\partial\Phi}{\partial x}\right)_e = \frac{\Phi_E - \Phi_C}{\Delta x}, \quad \left(\frac{\partial\Phi}{\partial y}\right)_n = \frac{\Phi_N - \Phi_C}{\Delta y}$$

$$\Rightarrow (\Phi_E - \Phi_C) + (\Phi_N - \Phi_C) + (\Phi_W - \Phi_C) + (\Phi_S - \Phi_C) = Q(x_c,y_c)\frac{\Delta^2}{K}$$

$$\Rightarrow \Phi_E + \Phi_N + \Phi_W + \Phi_S - 4\Phi_C = Q(x_c,y_c)\frac{\Delta^2}{K}$$

**Dirichlet Boundary Condition Impact:**
If West face is a Dirichlet boundary $\Phi = \Phi_0$:
$$\left(-\frac{\partial\Phi}{\partial x}\right)_w \Delta y = -\frac{\Phi_C - \Phi_0}{\Delta x / 2}\Delta y = 2(\Phi_0 - \Phi_C)$$

$$\Rightarrow \Phi_E + \Phi_N + \Phi_S - 5\Phi_C = Q(x_c,y_c)\frac{\Delta^2}{K} - 2\Phi_0$$

---

**Neumann Boundary Condition Impact:**
If South face has Neumann condition $\left.\frac{\partial\Phi}{\partial n}\right|_s = \gamma$:
$$-\int_s \left(\frac{\partial\Phi}{\partial y}\right)_s dS = \gamma \Delta x$$

$$\Rightarrow \Phi_N + \Phi_E + \Phi_W - 3\Phi_C = Q(x_c,y_c)\frac{\Delta^2}{K} + \gamma \Delta x$$

Example Grid Setup ($\Delta x = \Delta y = 0.5$):
$$\frac{\partial^2\Phi}{\partial x^2} + \frac{\partial^2\Phi}{\partial y^2} = 3xy$$

Equations for specified nodes:

- **Cell 10 (Interior Cell):**
  $$\Phi_6 + \Phi_9 + \Phi_{11} + \Phi_{14} - 4\Phi_{10} = \frac{Q(x_c,y_c)}{K}\Delta^2$$

- **Cell 12 (East Neumann Boundary $\gamma = 20$):**
  $$\Phi_8 + \Phi_{11} + \Phi_{16} - 3\Phi_{12} = \frac{Q(x_c,y_c)}{K}\Delta^2 + \gamma \Delta x$$

- **Cell 13 (West Dirichlet $\Phi=50$, North Neumann $\gamma=10$):**
  Write out full balances for cell face fluxes.

---

Expanding Cell 13 formulation:
$$\Phi_{14} - \Phi_{13} - \Phi_{13} + \Phi_9 - 2\Phi_{13} + 100 + 10\Delta x = \frac{Q(x_c,y_c)\Delta x \Delta y}{K}$$

$$\Rightarrow \Phi_9 - 4\Phi_{13} + \Phi_{14} = \frac{3x_c y_c}{K}\Delta^2 - 10\Delta x - 100$$

### Convection with Finite Volumes

Governing Equation:
$$\nabla \cdot (\vec{v}\Phi) - K \nabla \cdot (\nabla \Phi) = Q(x,y)$$

1D Convection-Diffusion Equation:
$$\frac{d}{dx}(u\Phi) - K\frac{d}{dx}\left(\frac{d\Phi}{dx}\right) = Q(x)$$

Integrating along cell:
$$\int_{x_l}^{x_r} \frac{d}{dx}(u\Phi) dx - \int_{x_l}^{x_r} K\frac{d}{dx}\left(\frac{d\Phi}{dx}\right) dx = \int_{x_l}^{x_r} Q(x) dx$$

$$\Rightarrow \left[ u\Phi|_{x=x_r} - u\Phi|_{x=x_l} \right] - K \left[ \left.\frac{d\Phi}{dx}\right|_{x=x_r} - \left.\frac{d\Phi}{dx}\right|_{x=x_l} \right] = Q(x_c)\Delta x$$

---

Evaluating face values:
Using linear interpolation (Central Difference analogue):
$$\Phi_r = \frac{\Phi_C + \Phi_E}{2}, \quad \Phi_l = \frac{\Phi_C + \Phi_W}{2}$$

Substituting:
$$\left(\frac{u}{2} - \frac{K}{\Delta x}\right)\Phi_E + \left(-\frac{u}{2} - \frac{K}{\Delta x}\right)\Phi_W + \frac{2K}{\Delta x}\Phi_C = Q(x_c)\Delta x$$

**Stability:**
Central difference interpolation becomes unstable if $Pe > 2$.
Upwind strategy selects face values based on direction of $u$:

- If $u > 0$: $\Phi_r = \Phi_C, \Phi_l = \Phi_W$
- If $u < 0$: $\Phi_r = \Phi_E, \Phi_l = \Phi_C$

---

### Boundary Conditions in 1D Convection-Diffusion

**Dirichlet Boundary on West Side ($\Phi(x_l) = \Phi_0$):**
$$u \left[ \frac{\Phi_C + \Phi_E}{2} - \Phi_0 \right] - K \left[ \frac{\Phi_E - \Phi_C}{\Delta x} - \frac{\Phi_C - \Phi_0}{\Delta x / 2} \right] = Q(x_c)\Delta x$$

$$\Rightarrow \left(\frac{u}{2} + \frac{3K}{\Delta x}\right)\Phi_C + \left(\frac{u}{2} - \frac{K}{\Delta x}\right)\Phi_E = Q(x_c)\Delta x + u\Phi_0 + \frac{2K\Phi_0}{\Delta x}$$

**Neumann Boundary on East Side ($\left.\frac{d\Phi}{dx}\right|\_{x_r} = \gamma$):**
Flux balances adjusted by directly substituting derivative boundary values.

---

### 2D Convection-Diffusion Equation in FVM

$$\iint \nabla \cdot (\vec{u}\Phi) dA - \iint K \nabla \cdot (\nabla \Phi) dA = \iint Q(x,y) dA$$

$$\oint \Phi(\vec{u} \cdot \hat{n}) dS - K \oint \nabla \Phi \cdot \hat{n} dS = Q(x_c, y_c)\Delta x \Delta y$$

East face flux balance:
$$\int_e \left[ \Phi u - K \frac{\partial\Phi}{\partial x} \right] dS \approx \left[ \Phi_e u - K \left(\frac{\partial\Phi}{\partial x}\right)_e \right] \Delta y$$

North face flux balance:
$$\int_n \left[ \Phi v - K \frac{\partial\Phi}{\partial y} \right] dS \approx \left[ \Phi_n v - K \left(\frac{\partial\Phi}{\partial y}\right)_n \right] \Delta x$$

---

Substitute face values:
$$\left[ \left(\frac{\Phi_C + \Phi_E}{2}\right)u - K\left(\frac{\Phi_E - \Phi_C}{\Delta x}\right) \right] \Delta y + \dots = Q(x_c,y_c)\Delta x \Delta y$$

**Upwind Scheme Selection in 2D:**

- $x$-direction ($u > 0$): $\Phi_e = \Phi_C, \quad \Phi_w = \Phi_W$
- $x$-direction ($u < 0$): $\Phi_e = \Phi_E, \quad \Phi_w = \Phi_C$
- $y$-direction ($v > 0$): $\Phi_s = \Phi_S, \quad \Phi_n = \Phi_C$
- $y$-direction ($v < 0$): $\Phi_s = \Phi_C, \quad \Phi_n = \Phi_N$

Peclet numbers:
$$Pe_x = \frac{u\Delta x}{K}, \quad Pe_y = \frac{v\Delta y}{K}$$

---

### Unsteady Problems (Navier-Stokes & Time Marching)

Navier-Stokes equation (1D component momentum):
$$\frac{\partial u}{\partial t} + u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y} = -\frac{1}{\rho}\frac{\partial P}{\partial x} + g_x + \nu\left(\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2}\right)$$

Time index: $n$
Spatial index: $i, j$

### Explicit Euler Method

Forward difference in time, central difference in space.

1D Convection-Diffusion transient equation:
$$\frac{\partial\Phi}{\partial t} = -u\frac{\partial\Phi}{\partial x} + K\frac{\partial^2\Phi}{\partial x^2} + Q(x)$$

$$\frac{\partial\Phi}{\partial t} \approx -u\left(\frac{\Phi_{i+1}^n - \Phi_{i-1}^n}{2\Delta x}\right) + K\left(\frac{\Phi_{i+1}^n - 2\Phi_i^n + \Phi_{i-1}^n}{\Delta x^2}\right) + Q(x_i)$$

---

$$\frac{\Phi_i^{n+1} - \Phi_i^n}{\Delta t} = -u\left(\frac{\Phi_{i+1}^n - \Phi_{i-1}^n}{2\Delta x}\right) + K\left(\frac{\Phi_{i+1}^n - 2\Phi_i^n + \Phi_{i-1}^n}{\Delta x^2}\right) + Q(x_i)$$

$$\Rightarrow \Phi_i^{n+1} = \Phi_i^n - \frac{u\Delta t}{2\Delta x}(\Phi_{i+1}^n - \Phi_{i-1}^n) + \frac{K\Delta t}{\Delta x^2}(\Phi_{i+1}^n - 2\Phi_i^n + \Phi_{i-1}^n) + Q(x_i)\Delta t$$

Grouping terms by time step $n$:
$$\Phi_i^{n+1} = \left(\frac{u\Delta t}{2\Delta x} + \frac{K\Delta t}{\Delta x^2}\right)\Phi_{i-1}^n + \left(1 - \frac{2K\Delta t}{\Delta x^2}\right)\Phi_i^n + \left(-\frac{u\Delta t}{2\Delta x} + \frac{K\Delta t}{\Delta x^2}\right)\Phi_{i+1}^n + Q(x_i)\Delta t$$

Example parameters:
$$\frac{\partial\Phi}{\partial t} = 3\frac{\partial^2\Phi}{\partial x^2}, \quad u=0, K=3$$
$$\Phi(x=0, t) = 1, \quad \Phi(x, t=0) = 0, \quad \left.\frac{\partial\Phi}{\partial x}\right|_{x=1} = 2, \quad \Delta x = 0.25, \Delta t = 0.1$$

Update equation:
$$\Phi_i^{n+1} = 4.8\Phi_{i-1}^n - 8.6\Phi_i^n + 4.8\Phi_{i+1}^n$$

---

Initial conditions at $t=0$:
$$\Phi_1 = 1, \quad \Phi_2 = 0, \quad \Phi_3 = 0, \quad \Phi_4 = 0, \quad \Phi_5 = 0.5$$

Boundary conditions applied:

- $i=1$: $\Phi_1 = 1$
- Neumann condition at right boundary:
  $$\frac{\Phi_5 - \Phi_4}{0.25} = 2 \Rightarrow \Phi_5^{n+1} = 2\Delta x + \Phi_4^n$$

Step-by-step node update system:
$$\Phi_2^{n+1} = 4.8\Phi_1^n - 8.6\Phi_2^n + 4.8\Phi_3^n$$
$$\Phi_3^{n+1} = 4.8\Phi_2^n - 8.6\Phi_3^n + 4.8\Phi_4^n$$
$$\Phi_4^{n+1} = 4.8\Phi_3^n - 8.6\Phi_4^n + 4.8\Phi_5^n$$
$$\Phi_5^{n+1} = 4.8\Phi_4^n - 8.6\Phi_5^n + 4.8\Phi_6^n$$

---

### Implicit Euler Method

Requires solving a matrix system at each time step. Spatial derivatives evaluated at step $n+1$:

$$\frac{\partial\Phi}{\partial t} + u\frac{\partial\Phi}{\partial x} = K\frac{\partial^2\Phi}{\partial x^2} + Q(x)$$

$$\frac{\Phi_i^{n+1} - \Phi_i^n}{\Delta t} + u\frac{\Phi_{i+1}^{n+1} - \Phi_{i-1}^{n+1}}{2\Delta x} = K\frac{\Phi_{i+1}^{n+1} - 2\Phi_i^{n+1} + \Phi_{i-1}^{n+1}}{\Delta x^2} + Q(x_i)$$

Rearranging for unknown values at $n+1$:
$$\left(-\frac{u\Delta t}{2\Delta x} - \frac{K\Delta t}{\Delta x^2}\right)\Phi_{i-1}^{n+1} + \left(1 + \frac{2K\Delta t}{\Delta x^2}\right)\Phi_i^{n+1} + \left(\frac{u\Delta t}{2\Delta x} - \frac{K\Delta t}{\Delta x^2}\right)\Phi_{i+1}^{n+1} = \Phi_i^n + Q(x_i)\Delta t$$

**Courant Number:**
$$C = \frac{u\Delta t}{\Delta x}$$

## Coding Implementation

## Conclusion
