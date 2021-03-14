# Teaching Myself Quantum Mechanics, Part Two.

On the previous episode, we said that any spin state can be represented as a linear combination of the basis vectors $\vert u\rangle$ and $\vert d\rangle$, which represent the *up* and *down* spin states. Now, we would like to derive an expression for the $\vert r\rangle$ and $\vert l\rangle$ states in terms of our basis.

Experimentally, we know that is we prepare state $\vert r\rangle$ and then measure $\sigma_z$, we get equal probabilities for *up* and *down*. What does this means mathematically? It means that the magnitude of the components of $\vert u\rangle$ and $\vert d\rangle$ need to be equal in our representation of $\vert r\rangle$ and  $\vert l\rangle$. That is, $\sigma_u^{*}\sigma_u=\sigma_d^{*}\sigma_d = \frac{1}{2}$. Let's find a vector that satifies these conditions:

$$\vert r\rangle = \frac{1}{\sqrt{2}}\vert u\rangle + \frac{1}{\sqrt{2}}\vert d\rangle$$

Great! Now let's find a formulation for the vector $\vert l\rangle$. As for $\vert r\rangle$, we know that once the spin as been prepared in the *left* configuration, the probabilities for the $\sigma_z$ states are again $\frac{1}{2}$. Moreover, we should now be able to see that $\vert r\rangle$ and $\vert l\rangle$ should be orthogonal, as if the spin is *right*, it is definitely not *left,* and viceversa. Thus, as we have already stated in the *up* and *down* case,

$$\langle r \vert l \rangle = 0$$
$$\langle l \vert r \rangle = 0$$

and this condition gives us

$$\vert l\rangle = \frac{1}{\sqrt{2}}\vert u\rangle - \frac{1}{\sqrt{2}}\vert d\rangle$$

It's worth noticing that this is not the only solution, due to something called *phase ambiguity*. Basically, if we multiply $\vert l \rangle$ by a phase factor (a complex number with unit magnitude, in the form $e^{i\theta}$, then the vector will still be normalized, and will still be orthogonal to $\vert r \rangle$. (I think) we will be able to get back to this observation.

If we apply the same kind of conditions to the spin vectors along the $y$-axis, we finally get

$$\vert i\rangle = \frac{1}{\sqrt{2}}\vert u\rangle + \frac{i}{\sqrt{2}}\vert d\rangle$$
$$\vert o\rangle = \frac{1}{\sqrt{2}}\vert u\rangle - \frac{i}{\sqrt{2}}\vert d\rangle$$

### Spin States as Column Vectors

Up to this points, we have kept our state vectors abstract, and didn't provide a numerical representation that would allow us to make actual calculations. However, the task is quite easy. Remember that $\vert u \rangle$ and $\vert d \rangle$ need to have unith length and be mutually orthogonal. A pair of vectors that satisfies both these conditions is

$$\vert u \rangle = \begin{bmatrix}           1 \\
0 \\
\end{bmatrix}$$
$$\vert d \rangle = \begin{bmatrix}           0 \\
1 \\
\end{bmatrix}$$

Once we have this, using the equation we have derived, it's easy to get column vector representations for all the other spin states.

So, what have we accomplished so far?

- We made some (fake) spin experiments, and based on the results, we chose three pairs of mutually orthogonal basis vectors. We noticed that spin states along the same direction are physically distinct, which meant that the state vectors are mutually orthogonal.
- Arbitrarily, we chose the *up* and *down* state vectors as basis vectors to represent all spin states. and figured out a way to derive the other state vectors by imposing orthogonality and probability-based constraints.
- We established a way of representing our state vectors as column vectors which actual numbers in them.

### Linear Operators, Hermitian Conjugation

In QM, the quantities we measure in a system are called *observables*. The position, or the angular momentum of a particle are examples of observables.
Observables are represented by linear operators, which are essentially linear funcions (in matrix form) being applied to vectors (in our case, the state vectors), as in

$$M \vert A \rangle = \vert B \rangle$$

with $M$ being the operator applied to vector $\vert A \rangle$, resulting in $\vert B \rangle$.