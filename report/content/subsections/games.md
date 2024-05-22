### Non-local Games {#ssec:games}

Finally, we cover some theory on so-called *non-local games*. These can be
understood as theoretical constructs used for realizing the impact of quantum
entanglement in computation. Such games have also been used to experimentally
prove the existence of entanglement @WoodPioneeringQuantum2022, which is their
primary use in the area of QKD.

These games are modeled as taking place between two cooperating "players" that
operate at a large distance, making communication through classical channels
during the course of the game unfeasible. Typically, the players of the games
are referred to as Alice and Bob and a verifier, or *referee*, is introduced to
present the players with input and decide if they win the game based on their
respective outputs. In its most general form, non-local games can be defined as
follows:

Definition 
:   A *non-local game*, $\mathcal{G}(V, \pi)$, between players $A$ and $B$ 
    is given by the following parameters:

    - Question sets $[n_A]$ and $[n_B]$,
    - answer sets $[m_A]$ and $[m_B]$,
    - a probability function $\pi:[n_A] \times [n_B] \to [0, 1] \subset \R$, and
    - a function $V:[m_A] \times [m_B] \times [n_A] \times [n_B] \to \{0, 1\}$.

    Typically, we write $V(a, b \mid x, y)$ in place of $V(a, b, x, y)$ 
    where $(a, b) \in [m_A] \times [m_B]$ and $(x, y) \in [n_A] \times [n_B]$ 
    to indicate that this value represents the result of running the game
    with outputs $(a, b)$ given inputs $(x, y)$.

The referee selects the input questions $(x, y)$ based on the probability
function $\pi$, and distributes $x$ to player $A$ and $y$ to player $B$. Both
players return some output value, $a$ from Alice and $b$ from Bob upon which
the referee decides if they win the game if $V(a, b \mid x, y) = 1$. Crucially,
the players are allowed to discuss a common strategy before the start of the
game in order to maximize their winning probability.

On option for Alice and Bob in this scenario is to rely on a purely
deterministic choice of output based on the given input, or they may use
a randomized procedure. However, they may also decide on a quantum strategy
involving the use of a shared, entangled, quantum state. As we will see, for some
games, a quantum strategy can result in a greater probability of winning the game
compared to a classical strategy. 

We now present one of the most significant examples of a non-local game, which
is the *CHSH game*, so named after physicists John Clauser, Michael Horne,
Abner Shimony, and Richard Holt which first introduced it
@ClauserEtAlProposedExperiment1969.

Example (The CHSH game)
:   Let $[n_A] = [n_B] = [m_A] = [m_B] = \{0, 1\}$, $\pi$ be the uniform probability
    distribution on $[n_A] \times [n_B]$ and define
    $$
    V(a, b \mid x, y) = 
    \begin{cases}
        1 \text{ if } a \oplus b = x \land y\\
        0 \text{ otherwise.}
    \end{cases}
    $$
    By considering the properties of logical operations, we can observe that
    $x \land y = 0$ for all cases except when $x = y = 1$, while $a \oplus b = 0$ 
    only when $a = b$. Therefore, an optimal and fully deterministic strategy
    for Alice and Bob is to decide to alway return $0$ (or $1$), independent of
    their input. This leads to a winning probability of $\frac{1}{4}$.

    Alternatively, if Alice and Bob decide to use a quantum strategy for
    winning the game, they can choose to share an entangled Bell state
    $\ket{\psi} = \frac{1}{\sqrt{2}}(\ket{00} + \ket{11})$, and select the PVMs
    corresponding to measurements in the bases $\{\ket{0}, \ket{1}\}$ if $x
    = 0$ and $\{\frac{1}{\sqrt{2}}(\ket{0} + \ket{1}),
    \frac{1}{\sqrt{2}}(\ket{0} - \ket{1})\}$ if $x = 1$ for Alice, and the
    measurement bases $\{\cos \frac{\pi}{8}\ket{0} + \sin \frac{\pi}{8}\ket{1},
    -\sin \frac{\pi}{8}\ket{0} + \cos \frac{\pi}{8}\ket{1}\}$ if $y = 0$ and
    $\{\cos \frac{\pi}{8}\ket{0} - \sin \frac{\pi}{8}\ket{1}, \sin
    \frac{\pi}{8}\ket{0} + \cos \frac{\pi}{8}\ket{1}\}$ if $y = 1$ for Bob. The
    corresponding PVMs are denoted by $P_i^j$ and $Q_i^j$ for $i, j \in \{0,
    1\}$, respectively.

    With this strategy if, for example, the given input is $x = y = 0$, the
    probability of Alice and Bob winning the game is given by the combined
    probability of the two players measuring and both observing $0$ or $1$,
    i.e.
    $$
    \bra{\psi}P_0^0 \otimes Q_0^0 \ket{\psi} + \bra{\psi}P_1^0 \otimes Q_1^0
    \ket{\psi} = \cos^2 \frac{\pi}{8} \approx 0.85.
    $$ 
    In fact, it can be shown that this is the optimal winning probability of this,
    and in fact any, quantum strategy for this game. This result is known as
    Tsirelson's bound @CirelsonQuantumGeneralizations1980.

