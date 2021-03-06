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

In QM, the quantities we measure in a system are called *observables*. The position, or the angular momentum of a particle are examples of observables. The spin components we were measuring earlier, such as $\sigma_z$ of $\sigma_x$, are also observables.
Observables are represented by linear operators, which are essentially linear funcions (in matrix form) being applied to vectors (in our case, the state vectors), as in

$$M \vert A \rangle = \vert B \rangle$$

with $M$ being the operator applied to vector $\vert A \rangle$, resulting in $\vert B \rangle$.

Moreover, in QM we deal with *Hermitian* operators, meaning that the operator matrix is always equal to its Hermitian conjugate (the transpose of the complext conjugate).

Equipped with these abstract and apparently meaningless notions, we are now ready to state the *fundamental theorem* of quantum mechanics:

* The eigenvectors of a Hermitian operator are a complete set. This means that any vector the operator can generate can be expanded as a sum of its eigenvectors.
* If $\lambda_1$ and $\lambda_2$ are two unequal eigenvalues of a Hermitian operator, then the corresponding eigenvectors are orthogonal.
* If two eigenvalues are equal, the corresponding eigenvectors can be chosen to be orthogonal.

We can summarize this by saying that *the eigenvectors of a Hermitian operator form an orthonormal basis*.


I will finish this post by finally stating the principles of quantum mechanics. In the next episode, we will get back to the principles and show an example of their application in the context of the *spin* of a system.

* **Principle 1**: the observable quantities of quantum mechanics are represented by linear operators (very abstract, I know)
* **Principle 2**: The possible results of a measurement are the eigenvalues of the operator that represents the observable. The state that results in a certain measurement value is the corresponding eigenvector.
* **Principle 3**: Unambigously distinguisihible states are represented by orthogonal vectors
* **Principle 4**: If $\vert A \rangle$ is the state-vector of a system, and the observable $L$ is measurd, the probability to observe value $\lambda_i$ is

$$
P(\lambda_i) = \langle A \vert \lambda_i \rangle \langle \lambda_i \vert A \rangle
$$

where $\lambda_i$ are the eigenvalues of L, and $\vert \lambda_i \rangle$ are the corresponding eigenvectors.

Again, everything is still very abstract and hardly self-explanatory, but everything should make much more sense going forward with this series.

However, we can already have a high-level understanding of these principles.
For example, Principle 2 is telling us that the result of the measurement of an observable are always real numbers from a set of possible results (note that the eigenvalues of a hermitian operator are always real). This makes sense: we can't expect an actual physical quantities such as the energy of a particle to be complex. The real world is inherently real :)

As an example, the eigenvalues of the spin operator need to have exactly two eigenvalues corresponding to $+1$ and $-1$, since those are the only possible results of the measurement.