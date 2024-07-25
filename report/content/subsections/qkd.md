### Quantum Key Distribution {#ssec:qkd}

Existing quantum key distribution protocols are largely based on two different
techniques. The earliest example of QKD is the so-called BB84 protocol, named
as such by its inventors, Bennet and Brassard
@BennettBrassardQuantumCryptography2014, utilizes Heisenberg's uncertainty
principle. Later protocols, notably the E91 protocol proposed by Ekert
@EkertQuantumCryptography1991a instead relies on entangled pairs of photons as
we will see. These entanglement-based protocols builds on Bell's theorem and
the Bell pair of qubits that we have seen in Section @ssec:qit to detect
potential eavesdroppers during the key distribution process. In this section,
we will present these two significant protocols, as well as others, that will
later be implemented and compared in terms of their efficiency.

The two key quantum mechanical properties which are used in order to ensure
privacy and security in QKD protocols are the no-cloning theorem, and the
already discussed property that any measurement of a quantum state inevitably
and permanently disturbs the state. 

Theorem (The No-Cloning Theorem)
:   Let $H$ be a Hilbert space. There does not exist a unitary operation $U$ 
    on $H \otimes H$ such that 
    $$
    U(\ket{\psi}\ket{0}) = \ket{\psi}\ket{\psi},
    $$ 
    for any quantum state $\ket{\psi} \in H$.

Proof
:   Suppose such $U$ exist so that for any $\ket{\psi}, \ket{\varphi} \in H$ 
    we have that
    \begin{equation}
        \begin{split}
            & \ket{\psi}\ket{0} \xmapsto{U} \ket{\psi}\ket{\psi} \\
            & \ket{\varphi}\ket{1} \xmapsto{U} \ket{\varphi}\ket{\varphi}
        \end{split}
    \end{equation} {#eq:nocl}
    Since $U$ is unitary, it preserves the inner product so we observe that it
    should hold that 
    $$
    \langle U(\ket{\psi}\ket{0}), U(\ket{\varphi}\ket{0}) \rangle
    = \bra{\psi}\bra{0}\ket{\varphi}\ket{0}
    = \braket{\psi | \varphi} \braket{0 | 0}
    = \braket{\psi | \varphi}.
    $$ 
    Thus, by (@eq:nocl) we find that $\braket{\psi | \varphi} = \braket{\psi |
    \varphi}^2$. This implies that either the states are orthogonal, or
    $\ket{\psi} = \ket{\varphi}$. This shows that $U$ cannot copy arbitrary
    states but only those that are orthoghonal to eachother.

So, a potential eavesdropper cannot copy any quantum state that is transmitted
over a public quantum channel in order to attempt a man-in-the-middle attack, nor
can she measure any transmitted state without causing disturbance that would be 
distinguishable to the parties involved in the QKD protocol.

Most QKD protocols utilize these two properties and measure the amount of
disturbance seen during execution in order to determine the amount of
eavesdropping that has occurred. A tolerable level of eavesdropping is decided
before the start of the protocol, which dictates whether the resulting shared
string should be discarded and the protocol rerun, or if it is permissible to
run a privacy amplification and information reconciliation scheme to ultimately
obtain a shared secret key.

Throughout this section, we assume that a key distribution protocol takes place
between two parties, Alice and Bob, both trusted to behave according to the
rules of the protocol. It can be assumed that an eavesdropper, Eve, is present
and monitoring any public channel.

#### BB84 {#sssec:bb84}

The first key distribution protocol based on the principles of quantum
mechanics was proposed by Bennet and Brassard in 1984
@BennettBrassardQuantumCryptography2014. At the time, this was a revolutionary
idea as the primary practical suggestions utilizing the principles of quantum
mechanics prior to this was mainly in the area of how to transmit
self-destructive messages and on creating unforgeable tokens. In this setting,
as is assumed in most QKD protocols, the parties, often referred to as Alice
and Bob, have access to a quantum channel as well as a classical channel. We
now describe the steps of the key distribution protocol, a description in
pseudocode is also given in Figure X. 

To initiate the protocol, Alice generates two random bit-strings, $a, b \in
\{0, 1\}^{n}$, of length $n$. Both strings are subsequently encoded into a
tensor product of quantum states of the form
$$
\ket{\psi} = \bigotimes_{i = 1}^{n} \ket{\psi_{a_i b_i}},
$$ 
where
\begin{equation*}
    \begin{split}
        & \ket{\psi_{00}} = \ket{0} \\
        & \ket{\psi_{10}} = \ket{1} \\
        & \ket{\psi_{01}} = \frac{1}{\sqrt{2}}(\ket{0} + \ket{1}) \\
        & \ket{\psi_{11}} = \frac{1}{\sqrt{2}}(\ket{0} - \ket{1})
    \end{split}
\end{equation*}
So, in essence, the $i$th bit of $b$ determines the basis into which the
$i$th bit of $a$ is encoded.

Next, Alice transmits the state $\ket{\psi}$ to Bob over the noisy quantum
channel. At this point, Bob announces that he has successfully received the
state and generates a random bit-string $b' \in \{0, 1\}^n$ which determines
the bases for measurement of the qubits in the composite state $\ket{\psi}$.
Applying these measurements, he obtains a resulting bit-string $a' \in \{0,
1\}^n$. 

Alice then publicly announces the string $b$ on the classical channel. Now,
Alice and Bob may publicly compare the bits in $b$ and $b'$ and independently
discard those $a_i$ and $a_i'$ for which $b_i \neq b_i'$. The shared string
obtained in this way should be of length at least $n / 2$, otherwise the
protocol is aborted.

At this point, a shared bit-string has been generated between the parties and
it remains for Alice and Bob to ensure that any disturbance due to
eavesdropping is below the acceptable threshold. To this end, Alice selects
a random sample of the bits in the shared string to serve as a check for noise.
This selection of bits is shared with Bob. Alice and Bob then share and compare
their check bits and abort the protocol if these disagree in more than
$\varepsilon$ instances. Lastly, privacy amplification and information reconciliation
is performed on the remaining $n / 4$ bits in order to obtain a shared secret
key of length $k$.

Note that during the point after which Alice has distributed $\ket{\psi}$ to
Bob, we may note that Eve has no use for this state since it is not known to
her into which bases the information has been encoded, and any attempt at
measuring the state would result in disturbance observable by Bob.
