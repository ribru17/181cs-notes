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
