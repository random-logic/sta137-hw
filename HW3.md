# 3.1
For $MA(1)$, the autocorrelation function is given as:
$$\gamma(h) = Cov[x_{t + h}, x_t]$$
$$\gamma(h) = Cov[w_{t + h} + \theta w_{t + h - 1}, w_t + \theta w_{t - 1}]$$

When $h = 0$:
$$\gamma(0) = Cov[w_{t} + \theta w_{t - 1}, w_t + \theta w_{t - 1}]$$
$$\gamma(0) = Var[w_{t} + \theta w_{t - 1}]$$
$$\gamma(0) = (1 + \theta^2) \sigma^2_w$$

When $h = 1$:
$$\gamma(1) = Cov[w_{t + 1} + \theta w_{t}, w_t + \theta w_{t - 1}]$$
$$\gamma(1) = E[(w_{t + 1} + \theta w_{t})(w_t + \theta w_{t - 1})] - E[w_{t + 1} + \theta w_{t}]E[w_t + \theta w_{t - 1}]$$
$$\gamma(1) = E[(w_{t + 1} + \theta w_{t})(w_t + \theta w_{t - 1})] - 0$$
$$\gamma(1) = E[\theta w_{t}w_t]$$
$$\gamma(1) = \theta \sigma^2_w$$

Solve for $\rho_x(1)$:
$$\rho_x(1) = \frac{\gamma(1)}{\gamma(0)}$$
$$\rho_x(1) = \frac{\theta \sigma^2_w}{(1 + \theta^2) \sigma^2_w}$$
$$\rho_x(1) = \frac{\theta}{1 + \theta^2}$$

Find which $\theta$ results in minimum and maximum values of $\rho_x(1)$:
$$\frac{\delta \rho_x(1)}{\delta \theta} = \frac{\theta}{1 + \theta^2}$$
$$\frac{\delta \rho_x(1)}{\delta \theta} = \frac{1-\theta^2}{(1 + \theta^2)^2}$$

Set $\frac{\delta \rho_x(1)}{\delta \theta} = 0$, then the minimum and maximum values are at:
$$\theta = \pm 1$$

At $\theta = 1$:
$$\rho_x(1) = \frac{1}{1 + 1} = \frac{1}{2}$$

At $\theta = -1$:
$$\rho_x(1) = \frac{-1}{1 + 1} = -\frac{1}{2}$$

We know that $\theta = \pm 1$ are global maximums and minimums since both limits to infinity are within the range of the minimum and maximum:
$$\lim_{\theta \to -\infty} \frac{\theta}{1 + \theta^2} = \lim_{\theta \to -\infty} \frac{1}{2\theta} = 0$$
$$\lim_{\theta \to \infty} \frac{\theta}{1 + \theta^2} = \lim_{\theta \to -\infty} \frac{1}{2\theta} = 0$$

Since $-\frac{1}{2} \leq \rho_x(1) \leq \frac{1}{2}$:
$$|\rho_x(1)| \leq \frac{1}{2}$$

# 3.4
### (a)
Rewriting the model with backshift operator:
$$x_t = .8Bx_t - .15B^2x_t + w_t - .3Bw_t$$
$$x_t - .8Bx_t + .15B^2x_t = w_t - .3Bw_t$$
$$(1 - .3B)(1 - .5B)x_t = (1 - .3B)w_t$$

We can reduce the model to:
$$(1 - .5B)x_t = w_t$$

This is an $AR(1)$ model.

AR polynomial:
$$\phi(B) = 1 - .5B$$

MA polynomial:
$$\theta(B) = 1$$

Check the roots of AR polynomial:
$$1 - .5z = 0$$
$$z = 2$$

Since the root is outside of the unit circle, this process is causal.

There is no MA component, so this process is trivially invertible.

The causal representation is:
$$x_t = .5x_{t - 1} + w_t$$
$$x_t = .5(.5x_{t - 2} + w_{t - 1}) + w_t$$
$$...$$
$$x_t = \sum_{j = 0}^\infty .5^jw_{t - j}$$

The invertible representation is:
$$w_t = x_t - .5x_{t - 1}$$

### (b)
Rewriting with backshift operator:
$$x_t = Bx_t - .5B^2x_t + w_t - Bw_t$$
$$x_t - Bx_t + .5B^2x_t = w_t - Bw_t$$
$$(1 - B + .5B^2)x_t = (1 - B)w_t$$

Since we can't factor $1 - B + .5B^2$, our model is already in simplest form with no redundant parameters.

This is an $ARMA(2, 1)$ model.

AR polynomial:
$$\phi(B) = 1 - B + .5B^2$$

MA polynomial:
$$\theta(B) = 1 - B$$

Check the roots of AR polynomial:
$$1 - z + .5z^2 = 0$$

Using the quadratic formula:
$$z = \frac{1 \pm \sqrt{(-1)^2 - 4*.5*1}}{2*.5}$$
$$z = 1 \pm \sqrt{-1}$$
$$z = 1 \pm i$$

Since the complex roots are outside of the unit circle, this process is causal.

Check the roots of MA polynomial:
$$1 - z = 0$$
$$z = 1$$

Since the root is on the unit circle, this process is NOT invertible.

Since this process is causal, this can be written as:
$$
x_t = \sum_{j=0}^\infty \psi_j w_{t-j}
$$

To find the causal representation, derive the Coefficients. Let:
$$
\psi(B) = \sum_{j=0}^\infty \psi_j B^j
$$

Since:
$$x_t = \frac{\theta(B)}{\phi(B)}w_t$$

We can use the identity:

$$
\phi(B)\psi(B) = \theta(B)
$$

TODO: double check understanding of the below

In time-domain convolution, this gives the recursion:

$$
\sum_{k=0}^2 \phi_k \psi_{j-k} = \theta_j
$$

Where:

- $\phi_0 = 1$, $\phi_1 = -1$, $\phi_2 = 0.5$
- $\theta_0 = 1$, $\theta_1 = -1$, $\theta_j = 0$ for $j \geq 2$

We initialize:

- $\psi_{-1} = 0$
- $\psi_0 = 1$

Then recursively compute:

- $\psi_1 = \psi_0 - 0.5 \psi_{-1} + \theta_1 = 1 - 0 - 1 = 0$
- $\psi_2 = \psi_1 - 0.5 \psi_0 + 0 = 0 - 0.5 = -0.5$
- $\psi_3 = \psi_2 - 0.5 \psi_1 = -0.5 - 0 = -0.5$
- $\psi_4 = \psi_3 - 0.5 \psi_2 = -0.5 + 0.25 = -0.25$
- etc.

---

## General Recursive Formula

The coefficients follow the second-order linear recurrence:

$$
\begin{cases}
\psi_0 = 1 \\
\psi_1 = 0 \\
\psi_j = \psi_{j-1} - 0.5 \psi_{j-2}, & j \geq 2
\end{cases}
$$

---

## Final Representation

The causal representation of the process is:

$$
x_t = \sum_{j=0}^\infty \psi_j w_{t-j}
$$

Where:
$$
\begin{cases}
\psi_0 = 1 \\
\psi_1 = 0 \\
\psi_j = \psi_{j-1} - 0.5 \psi_{j-2}, & j \geq 2
\end{cases}
$$

