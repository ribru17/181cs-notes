# CS 181 Notes

<!-- vim: set spell: -->

<!-- Lecture 1 -->

## Course Subjects

- Data: Representations of objects
- Algorithms: Operations on data

## Different Forms of Data

### Roman Numerals vs. Decimal

To show the distance to the moon, Roman numerals would require a small book
while decimal requires only seven digits.

## Algorithms

### Multiplication

- First elementary algorithm for this is repeated addition (add the first number
  to itself the second number times).
- Grade school addition is more practical, you traverse digits and multiply them
  across for each tens place (takes $O(n^{2})$ operations).

When multiplying two 20 digit numbers, repeated addition takes $10^{20}$
operations while grade school addition takes only 400. Nowadays we have
discovered that multiplication can be done in $O(n\cdot \log n)$ time.

## Representing Objects

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

<!-- Lecture 2 -->

## Encodings

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

## Algorithms

- **Algorithms:** Gave a procedure for solving quadratic equations
  - From Al-Khwarizmi (9th century)
  - Informally: A series of simple steps to solve some problem.
- Steps are defined as basic operations, i.e. boolean circuits
  - `AND`, `OR`, `NOT`
  <!-- Lecture 3 -->
- $A(n, m, s)$ is a boolean circuit that is a DAG with $n + s$ vertices.
  - $n$ is the number of variables, $m$ is the number of output variables, and
    $s$ is the size of the circuit.
  - Exactly $n$ of these vertices are labeled as `x[0]`, `x[1]`, ... `x[n-1]`.
  - The other $s$ vertices are gates (`AND`, `OR`, `NOT`).
    - `AND` and `OR` have two inputs while `NOT` has one
  - $m$ of the gates are labeled as outputs `y[0]`, `y[1]`, ... `y[m-1]`.
  - $m \le n + s$
- `NAND` Circuits
  - $(n, m, s)\text{NAND}$ circuit is a DAG where there are:
    - $n$ inputs `x[0]`, `x[1]`, `x[2]`, ... `x[n-1]`
    - $s$ gates each having exactly two inputs (computing `NAND`)
    - $m$ vertices labeled `y[0]`, `y[1]`, ... `y[m-1]`
  - Given a `NAND` circuit $C$, we can define a function $C: \langle 0, 1
    \rangle^{n} \longrightarrow \langle 0, 1 \rangle^{m}$ that $C$ computes.
    - A `NAND` circuit $C$ computes a function $f$ if $f(x) = C(x) \forall x$.
  - If we have a `NAND` gate computing a function $f$, we can also get a boolean
    circuit for it.
    - We can compute `NOT` with `NAND` gates (`NAND` $a$ with itself)
    - We can also compute `AND` (use regular `NAND` and then a `NOT` using the
      above method)
    - We can compute `OR` because $\text{OR}(a, b) = \text{NAND}(\lnot a, \lnot
      b)$
  - **Theorem:** Boolean circuits are equivalent to `NAND` in computing power.
    - `AND` and `OR` is not enough to create any complete circuit.
  - **Theorem:** Every function $f: \langle 0, 1 \rangle^{n} \longrightarrow
    \langle 0, 1 \rangle^{m}$ can be computed by a boolean circuit of size
    $O(n\cdot m\cdot 2^{n})$.
    - **Remark:** Addition $\text{ADD}(x, y): \langle 0, 1 \rangle^{n} \times
      \langle 0, 1 \rangle^{n} \longrightarrow \langle 0, 1 \rangle^{n+1} = x +
      y$ can be computed by a boolean circuit of size $O(n)$. Multiplication
      $\text{MULT}(x, y): \langle 0, 1 \rangle^{n} \times \langle 0, 1
      \rangle^{n} \longrightarrow \langle 0, 1 \rangle^{2n} = x \cdot y$ can be
      computed by a circuit of size $O(n^{2})$.

<!-- Lecture 4 -->

## Functions

- **Theorem:** Every function $f: \langle 0, 1 \rangle^{n} \longrightarrow
  \langle 0, 1 \rangle^{m}$ can be computed by a boolean circuit of size $O(m
  \cdot n \cdot 2^{n})$.

  - Example when $m = 1$:

    - $f: \langle 0, 1 \rangle^{n} \longrightarrow \langle 0, 1 \rangle$
    - We can make a table with entries of every possible input of bits and their
      output:

      | Input Strings | Output   |
      | ------------- | -------- |
      | 0 0 ... 0     | 0        |
      | 0 0 ... 1     | 1        |
      | $\vdots$      | $\vdots$ |

      The table has $2^{n}$ rows of size $n$, plus one extra bit in the rows for
      their output.

- We can have a set $S$ as all possible inputs where our above function $f$
  evaluates to one, $S(f) = \langle \alpha \in \langle 0, 1 \rangle^{n}:
  f(\alpha) = 1 \rangle$.
- **Definition:** For a string $\alpha \in \langle 0, 1 \rangle^{n}$ define
  $E_\alpha: \langle 0, 1 \rangle^{n} \longrightarrow \langle 0, 1 \rangle$.
  $E_\alpha(x) = \begin{cases} 1 & x = \alpha \\ 0 & x \neq \alpha \end{cases}$
  - This is a very trivial function that is essentially a "spike", only one when
    the input is exactly alpha and zero everywhere else.
    - E.g. when $\alpha = (1, 1, \ldots, 1), E_{\alpha}(x) = \text{AND}(x[0],
      x[1], \ldots, x[n-1])$
- Observation of $S(f)$: $f(x) = 1 \iff x \in S(f)$. Thus $f(x) =
  \text{OR}(E_{\alpha^{0}}(x), E_{\alpha^{1}}(x), \ldots, E_{\alpha^{n-1}}(x))$.
- If we construct a circuit to compute the above function, the circuit computes
  $f$ using at most $(2n-1)2^{n}$ gates.
- **Theorem (Shannon, 1949):** Some functions require $\frac{2^{n}}{24n}$ gates
  to compute!
- _Remark:_ The "upper bound" can be improved: every function can be computed
  with $O(\frac{2^{n}}{n})$ gates.
- We can also encode circuits themselves as $\langle 0, 1 \rangle^{\ast}$
  strings. This will allow for "universal circuits", i.e. circuits that can be
  passed as inputs into other circuits.
- **Theorem:** Every $(n, m, s)$ - `NAND` circuit can be represented by a
  boolean string of length $O((n+s) \cdot \log_2(n + s))$.
  - $\text{CIRCUIT}(n,m,s)$ = All circuits of $n$ inputs, $m$ outputs, and $s$
    gates.
- To encode a circuit, we must know:
  - How many inputs $n$
  - How many outputs $m$
  - How many gates $\le s$
  - Which nodes correspond to the output variables
  - What are the incoming wires (inputs) for each gate
- We first number each input, and then afterwards we number each gate (starting
  with the indices after the $n$ inputs, so first gate will be numbered $n$ with
  0-based indexing).
- We organize the data as $(n, m, s_0, \_, \_, \ldots, \_)$ where each
  underscore is the index of a node that is an output (thus there are $m$
  underscores).
  - We still need a way to specify the connections (map inputs to gates /
    outputs)!
- After the $m$ indices, we store tuples of the indices of the nodes into gate
  1, gate 2, etc. There will be $s_0$ such tuples (same as number of gates).
- **Theorem:** There is an encoding $E: \text{CIRCUIT}(n, m, s) \longrightarrow
  \langle 0, 1 \rangle^{\ast}$ such that the length of the encoding $\le
  12(n+s)\log_2(n+s)$. <!-- Lecture 5 -->
- **Theorem:** There exists a function $f: \langle 0, 1 \rangle^{n}
  \longrightarrow \langle 0, 1 \rangle$ that has no `NAND-CIRCUIT` of size $\le
  c \cdot \frac{2^{n}}{n}$ (for some fixed constant $c > 0$).

<!-- Lecture 6 -->

### Functions of Unbounded Input Length

An algorithm is a **finite** answer to an **infinite** number of questions.

A function $f: \langle 0, 1 \rangle^{\ast} \longrightarrow \langle 0, 1
\rangle^{\ast}$ has unbounded input length. (We can also consider functions of
the form $f: \langle 0, 1 \rangle^{\ast} \longrightarrow \langle 0, 1 \rangle$)

We can take an example from an `XOR` function which returns `1` when the sum of
the inputs is odd and `0` if even. It is a single-pass algorithm since it only
passes over the data once. It also has constant additional memory (only stores
the current sum).

- **GOAL:** Build a model for single-pass, constant memory algorithms.
  - We do this with finite state machines.
  - Using the previous example we have:

    ```mermaid
    flowchart LR

    A(Output = 0) -->|1| B(Output = 1)
    B -->|1| A
    B -->|0| B
    A -->|0| A
    ```

- **Deterministic Finite Automata (`DFA`):** `DFA` with $C$ sates over $\langle
  0, 1\rangle$ is a pair $D = (T,S)$ where $T: [C] x \langle 0, 1 \rangle
  \longrightarrow [C]$ and $S \le [C]$
  - $T(i, a) = j$: "If in state $i$, read bit $a$ -> jump to state $j$."
- $D: \langle 0, 1 \rangle^{\ast} \longrightarrow \langle 0, 1 \rangle$. On
  input $x$:
  - Start from state $s_0 = 0$
  - For $i = 0, \ldots, len(x) - 1$: $s_{i+1} = T(s_{i}, x[i])$
  - Output `1` if final state is in $S$, `0` otherwise.
- We say a `DFA` $D = (T, S)$ computes a function $f: \langle 0, 1
  \rangle^{\ast} \longrightarrow \langle 0, 1 \rangle$ if $f(x) = D(x) \forall x
  \in \langle 0, 1 \rangle^{\ast}$
- Can we compute operations on functions computed by `DFA` (e.g. `NOT`)?
  - If $f$ is computable by `DFA`, so is $\text{NOT}f$. To get $\text{NOT}f$ we
    simply flip the states.
  - However, `AND`ing two `DFA` functions are not computable by `DFA`, because
    it becomes not single-pass.
    - Here we must make a new `DFA` that computes the `AND` of the two. We
      compute the two functions in parallel when passing over the data. If the
      first function had $C_1$ states and the second $C_2$, the new function
      will have $C = C_1 \cdot C_2$ states.
    - With `OR`, the amount of states are the same, and the transition function
      remains the same.
