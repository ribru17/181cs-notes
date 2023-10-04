# CS 181 Notes

<!-- vim: set spell: -->

## Lecture 1

### Course Subjects

- Data: Representations of objects
- Algorithms: Operations on data

### Different Forms of Data

#### Roman Numerals vs. Decimal

To show the distance to the moon, Roman numerals would require a small book
while decimal requires only seven digits.

### Algorithms

#### Multiplication

- First elementary algorithm for this is repeated addition (add the first number
  to itself the second number times).
- Grade school addition is more practical, you traverse digits and multiply them
  across for each tens place (takes $O(n^{2})$ operations).

When multiplying two 20 digit numbers, repeated addition takes $10^{20}$
operations while grade school addition takes only 400. Nowadays we have
discovered that multiplication can be done in $O(n\cdot \log n)$ time.

### Representing Objects

We need a way to represent objects such as:

- Integers
- Complex numbers
- Images
- Text
- Graphs
- Audio
- Video
- Databases
- Etc.

We store all of them as a single sequence of ones and zeros. If we can store any
object of type `T`, we can also store collections of objects of type `T`.

Kleene Star: $A^{\ast} = \emptyset \cdot A \cdot A^{2} \cdot \ldots$

We know all objects can be stored in the form $\Theta \longrightarrow \langle 0,
1 \rangle^{\ast}$.

$E: \Theta \longrightarrow \langle0, 1\rangle^{\ast}$ is an **encoding** method
if and only if there is a $D: \langle0, 1\rangle^{\ast} \longrightarrow \Theta$
such that $\forall x \in \Theta: D(E(x)) = x$.

Encoding is only valid if it is one-to-one, i.e. each input has a unique output.

## Lecture 2

### Encodings

- Prefix-free encodings
  - $E: \Theta \longrightarrow \langle 0, 1 \rangle^{\ast}$ is a prefix-free
    encoding for all $x \neq y \in \Theta \Theta, E(x) \text{is not a prefix of}
    E(y)$
  - E.g. An encoding where data is continually parsed until some delimiter at
    the end that marks the data as complete
- **Theorem:** Suppose we have a prefix-free encoding $pE: \Theta
  \longrightarrow \langle 0, 1 \rangle^{\ast}$. Then $\overline{pE}:
  \Theta^{\ast} \longrightarrow \langle 0,1 \rangle^{\ast}: \overline{pE}([x_0,
  x_1, x_2, \ldots x_{n}]) = pE(x_0) \circ pE(x_1) \circ pE(c_2) \circ \ldots
  \circ pE(x_{n})$ is an encoding.
  - Essentially, with a prefix-free encoding we can easily encode strings of
    objects since we can decode until we hit the ending delimiter, and then know
    we have reached the next object. Before we would have had no way of knowing
    where on object ends and another begins.
- $\overline{pE}$ is _not_ a prefix-free encoding since it is a concatenation.
- However, we can convert any encoding into a prefix-free encoding by doing the
  following:
  - Compute $E(x)$
  - Duplicate each bit
  - Add `01` at the end
- We can use this to convert any list to a prefix-free encoding, such as a list
  of list of integers to binary, $(\mathbb{Z}^{\ast})^{\ast} \longrightarrow
  \langle 0,1 \rangle^{\ast}$ (which itself is not prefix-free but could be
  converted to be prefix-free using the above method).
- Space efficiency of this algorithm:
  - $E \longrightarrow pE \Rightarrow pE(x) = 2\cdot E(x) + 2$
  - $pE^{\ast}(x) = E(x) + 2\log_2(|E(x)| + 1) + 2$
- **Proof (Cantor 1876):** There is no one-to-one mapping from $\mathbb{R}
  \text{ to } \langle 0,1 \rangle^{\ast}$.

### Algorithms

- **Algorithms:** Gave a procedure for solving quadratic equations
  - From Al-Khwarizmi (9th century)
  - Informally: A series of simple steps to solve some problem.
- Steps are defined as basic operations, i.e. boolean circuits
  - `AND`, `OR`, `NOT`
