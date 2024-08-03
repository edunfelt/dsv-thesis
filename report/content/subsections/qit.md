### Quantum Information Theory {#ssec:qit}

Analogously to the classical theory of computing, the smallest unit of
computing is defined as a bit, more specifically as a \textit{qubit}, in
quantum information theory. However, there are a number of differences between
how the classical bit and the quantum bit are modeled. Most crucially, a qubit
represents the \textit{state} of a physical system, such as the polarization of
a photon or the two states of an electron orbiting an atom, which is modeled
mathematically as a unit vector in the Hilbert space $\mathbb{C}^2$:

Definition
:   A *qubit* representing a quantum state is a unit vector in $\mathbb{C}^2$, 
    and is denoted using ket-notation as
    $$
    \ket{\psi} = \alpha\ket{0} + \beta\ket{1},
    $$
    where $|\alpha|^2 + |\beta|^2 = 1$ and the symbols $\ket{0}$ and $\ket{1}$ 
    denotes the so-called *fundamental states* which corresponds to the usual 
    orthonormal basis in $\mathbb{C}^2$, i.e.
    $$
    \ket{0} =
    \begin{bmatrix}
        1 \\ 0
    \end{bmatrix}
    \qquad
    \ket{1} =
    \begin{bmatrix}
        0 \\ 1
    \end{bmatrix}.
    $$

Notably, a qubit does not only have two possible states -- 0 or 1 in the
classical case -- but is also allowed to be in a mix of the two. In particular,
if both $\alpha$ and $\beta$ are non-zero, the state is said to be in
*superposition*. Although it might thus appear that a quantum state can hold
more information than a classical state in that it can be in a mix of both the
fundamental states simultaneously, this is not really the case as the
postulates of quantum mechanics tells us that should we wish to retrieve the
value of the constants $\alpha$ and $\beta$ in $\ket{\psi}$ above, the state
collapses into either one of the two fundamental states with probability
$|\alpha|^2$ or $|\beta|^2$, respectively. This occurs through the process of
\textit{measurement} that we shall soon discuss in more detail.

Continuing the analogue to classical systems, we may construct registers of
quantum bits:

Definition
:    An *$n$-qubit system* is given by a unit vector in the space $\mathbb{C}^2 
     \otimes \ldots \otimes \mathbb{C}^2 = (\mathbb{C}^2)^{\otimes n}$. 

    If $\{ \ket{0}_A, \ket{1}_A\}$ denotes the fundamental states of a space 
    $\mathbb{C}_A^{2}$, and similarly $\{\ket{0}_B, \ket{1}_B\}$ denotes the
    fundamental states of $\mathbb{C}_B^2$, then the fundamental states of 
    $\mathbb{C}_A^2 \otimes \mathbb{C}_B^2$ is given by the set 
    $\{\ket{0}_A\otimes\ket{0}_B, \ket{0}_A\otimes\ket{1}_B, 
    \ket{1}_A\otimes\ket{0}_B, \ket{1}_A\otimes\ket{1}_B\}$, which is also
    denoted by $\{\ket{00}, \ket{01}, \ket{10}, \ket{11}\}$.

*Some concluding remarks about registers here.* In general, we consider a qubit
register of $n$ qubits to be an element of a Hilbert space $\mathcal{H}$ of
dimension $n^2$. In fact, there is a one to one correspondence between Hilbert
spaces of finite dimension $n^2$ and spaces of the form
$(\mathbb{C}^2)^{\otimes n}$, see for example Chapter X of
@MurphyAlgebrasOperator2004 for an introduction of this topic.

The information of a quantum state is, although not directly measurable, still
useful through the evolution of the state by applying different quantum gates
which ultimately alter the probability of different measurement outcomes.
A quantum state, much like a classical system, evolves by applying an operation
called a quantum gate. If quantum states are represented by vectors, a quantum
gate is represented by linear transformations, or matrices, in the following
way:

Definition 
:    A *quantum gate* on a state in the space $(\mathbb{C}^{2})^{\otimes n}$ is 
     a unitary transformation from this space to itself.

We choose unitary transformations to represent quantum gates for the simple
reason that such transformations preserves the property of being a unit vector,
hence ensuring that a quantum state is transformed into another. Interestingly,
since unitary linear transformations are invertible, it follows from this
definition that quantum gates are *reversible*.

Example (\texttt{CNOT})
:   One commonly applied quantum gate is the *controlled-\texttt{NOT}*
    gate which is applied to a two qubit state. One qubit in the state in this
    scenario is the control qubit and the other is the target qubit. The effect of
    applying this operation is to flip the value of the target qubit if and only
    if the control qubit is $\ket{1}$. This gate is given by the following matrix:
    $$
    \texttt{CNOT} =
    \begin{bmatrix} 
    1 & 0 & 0 & 0 \\ 
    0 & 1 & 0 & 0 \\
    0 & 0 & 0 & 1 \\
    0 & 0 & 1 & 0
    \end{bmatrix} 
    $$ 
    This operation resembles a classical \texttt{XOR} gate in that the result in
    the target qubit is the \texttt{XOR} of the control and target qubit.

Example (The Hadamard transform)
:   Another common operation is the *Hadamard transform*, which on a single-qubit 
    system is given by the matrix
    $$
    H = \frac{1}{\sqrt{2}}
    \begin{bmatrix} 
    1 & 1 \\
    1 & -1
    \end{bmatrix}.
    $$ 
    This gate has the notable effect that it transforms the standard basis of
    the fundamental states $\{\ket{0}, \ket{1}\}$ to
    $\frac{1}{\sqrt{2}}\left\{\begin{bmatrix} 1\\1 \end{bmatrix}, \begin{bmatrix} 1\\-1 \end{bmatrix}\right\}$, and back again. This basis is also frequently denoted
    $\{\ket{+}, \ket{-}\}$.

\begin{center}
    \begin{quantikz}
        \lstick{$\ket{\psi}$} & \ctrl{1} & \rstick{$\ket{\psi}$}\\
        \lstick{$\ket{\varphi}$} & \targ{} & \rstick{$\ket{\psi\oplus\varphi}$}
    \end{quantikz}
    \qquad
    \begin{quantikz}
        & \gate{H} &
    \end{quantikz}
    \captionof{figure}{Circuits representing the \texttt{CNOT} and Hadamard gates.}
    \label{fig:gates}
\end{center}

Much like in classical computation, qubits and operations on these can be
represented using circuits, which are used to give a pictorial representation
of the transformations performed. Our notation in this regard follows that of
@NielsenChuangQuantumComputation2010. Figure \ref{fig:gates} shows the circuits
representing the \texttt{CNOT} and Hadamard gate.

The final concept in need to be introduced is the notion of quantum measurements. 
Due to the peculiar nature of quantum physics, the actual value, i.e. the values of
the coefficients of the linear combination of the fundamental states, cannot be
directly retrieved from the state. Though, through a measurement process of the state
its value can be, at least partially, obtained. This processed is constrained by the
postulates of quantum mechanics:

Definition (The Born rule)
:   Measurement of the quantum state $\ket{\psi} = \alpha\ket{0} + \beta\ket{1}$
    results in an observation of the fundamental state $\ket{0}$ or $\ket{1}$ with
    probability $|\alpha|^2$ or $|\beta|^2$, respectively.

This postulate extends in the expected way to multi-qubit states. The Born rule
postulates that a quantum measurement effectively collapses the state to either
one of the fundamental states according to some probability distribution. We
formally define measurements as follows:

Definition
:   Let $\ket{\psi}$ be a quantum state in $(\mathbb{C}^2)^{\otimes n}$, and let
    $[n] = \{1, \ldots, n\}$ be a set of outcomes. Then, a *projective valued measurement
    (PVM)* is a collection of self-adjoint projections $\{P_i\}_{i \in [n]}$ such
    that $\sum_{i=1}^{n} P_i = \mathds{1}$. The probability of observing outcome
    $i$ upon measuring $\ket{\psi}$ is given by 
    $$
    ||P_i\ket{\psi}||^2 = \bra{\psi}P_i^*P_i\ket{\psi} = \bra{\psi}P_i\ket{\psi},
    $$ 
    upon which the state collapses to
    $$
    \frac{P_i\ket{\psi}}{\sqrt{\bra{\psi}P_i\ket{\psi}}}.
    $$ 

The specific kind of measurement we rely on in this thesis are the projective 
valued measurements. In the theory of quantum mechanics, there are also other types of
measurements, that, although the general principle remains the same in that they all
adhere to the Born rule, *some text here that motivates this choice of measurement*.

\begin{center}
    \begin{quantikz}
    & \meter{} &
    \end{quantikz}
    \captionof{figure}{Circuit representation of applying a measurement.}
    \label{fig:measurement}
\end{center}

The most surprising property of quantum mechanics, which puzzled researchers
for decades, is that of *entanglement*. It is this concept that we will later
utilize to create systems of perfectly correlated but separated systems which
can be used to securely distribute keys. 

As we have seen in the definition of multi-qubit systems, these systems are
unit vectors in the space $(\mathbb{C}^2)^{\otimes n}$. However, not all unit
vectors in this space can be written as a tensor product of unit vectors from
the $n$ individual Hilbert spaces $\mathbb{C}^2$. Such states nonetheless
exists and are said to be *entangled*. We now give an example of such a state,
that will be of great significance in later sections.

Example ex:bell (Bell-pair)
:   Consider the qubits $\ket{0}$ and $\ket{0}$ forming the two-qubit register
    $\ket{00}$ in $\mathbb{C}^2 \otimes \mathbb{C}^2$. To this state, we apply
    two consequtive gates -- first the Hadamard transform, and then the 
    \texttt{CNOT} gate -- to obtain the following state:
    $$
    \texttt{CNOT}(H \otimes \mathds{1}) \ket{00} = \frac{\ket{00} + \ket{11}}{\sqrt{2}}.
    $$ 
    This sequence of operations can be represented by the circuit in Figure \ref{fig:bell}.
    The resulting state is entangled and is often called a *Bell-pair*.

\begin{center}
    \begin{quantikz}
        \lstick{$\ket{0}$} & \gate{H} & \ctrl{1} & \rstick[wires=2]{$\frac{\ket{00}+\ket{11}}{\sqrt{2}}$}\\
        \lstick{$\ket{0}$} & & \targ{} &
    \end{quantikz}
    \captionof{figure}{Quantum circuit for creating a Bell-pair.}
    \label{fig:bell}
\end{center}

Crucially, when we measure an entangled state, the involved qubits no longer
behave like independent systems, but rather the resulting measurement outcomes
are closely correlated. For example, considering the Bell-pair defined above,
upon applying the measurement given by the PVM
$$
\left\{
\begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix},
\begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} 
\right\},
$$ 
to the first qubit, one observes $\ket{0}$ in this qubit with probability
$\frac{1}{2}$. In this case, the state in its entirety would collapse to
$\ket{00}$, since this is the only viable outcome. Thus, without measuring we
immediately know that the second qubit also is $\ket{0}$. Conversely, if
$\ket{1}$ is observed in the first qubit after measurement, the second qubit
must also be $\ket{1}$.
