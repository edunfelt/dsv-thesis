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
    $$
        \begin{split}
            & \ket{\psi}\ket{0} \xmapsto{U} \ket{\psi}\ket{\psi} \\
            & \ket{\varphi}\ket{1} \xmapsto{U} \ket{\varphi}\ket{\varphi}
        \end{split}
    $$ {#eq:nocl}
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

#### BB84 and B92 {#sssec:bb84}

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

There are many modifications proposed to the original BB84 in the literature,
see for instance [REFERENCES]. In 1992, Bennet proposed a significant
simplification of the original protocol in @BennettQuantumCryptography1992,
referred to as B92. In this version of the protocol, only two non-orthogonal
states are used to encode Alice's original bit-string $a$ into the state
$$
\ket{\psi} = \bigotimes_{i=1}^n \ket{\psi_{a_i}},
$$ 
where
\begin{equation*}
    \begin{split}
        & \ket{\psi_0} = \ket{0} \\
        & \ket{\psi_1} = \frac{1}{\sqrt{2}}(\ket{0} + \ket{1}.
    \end{split}
\end{equation*}
Bob then measures the received qubits either in the standard basis, if $a'_i =
0$, or in the Hadamard basis, if $a_i' = 1$. He records the outcomes in a
bit-string $b$ in which $b_i = 1$ if a measurement was made in the standard
basis and $\ket{0}$ was observed or if a measurement was made in the Hadamard
basis and $\frac{1}{\sqrt{2}}(\ket{0} + \ket{1})$ was observed, and $b_i = 0$
otherwise.

Bob then transmits $b$ and Alice and Bob both discard from $a$ and $a'$ the
bits $i$ for which $b_i = 0$. Now, similar to the original BB84 protocol, half
of the remaining bits can be used to check for eavesdropping before information
reconciliation and privacy amplification can be performed. Pseudocode for B92
is given in Figure X.

#### E91 and BBM92 {#sssec:e91}

In 1991, Ekert proposed a new approach to QKD which utilized quantum
entanglement to generate a shared string secure from eavesdropping
@EkertQuantumCryptography1991a. In this QKD protocol, a Bell pair, such as the
one we have seen in Example [](#ex:bell) is used to create a random bit-string that
is perfectly correlated between Alice and Bob, and which is also known to
satisfy a specific test statistic, namely Tsirelson's bound as was discussed in
Section @ssec:games. The steps of the modification of the original Ekert
protocol suggested in X are now presented here:

Alice and Bob obtain $n$ maximally entangled qubits in the Bell state from an
external source. Alice then generates a random $n$-bit string to represent a
selection of measurement bases for each qubit and performs these measurements,
documenting the outcomes in a bit-string $A$. Finally, she transmits the string
of measurements and the outcomes to Bob.

Bob similarly generates a string of length $n$ in the symbols $\{0, 1, 2\}$, where
2 represents the same basis as Alice's 0. He performs the measurements dictated 
by this string on his qubits and sends the string of measurements as well as the
outcomes to Alice.

Alice now randomly chooses a subset of indices of size $\frac{n}{2}$ and sends
this choice to Bob. Both parties then compare their results on this subset of
measurement outcomes with the Bell test statistic in order to confirm that the
measured qubits has indeed been entangled during the course of the protocol. If
so is the case, the qubits with a common measurement basis can be used to
generate a shared secret key.

The original version of E91 saw the use of three measurement bases for both
Alice and Bob, $\{Z_0, Z_{\frac{\pi}{4}}, Z_{\frac{\pi}{2}}\}$ for Alice and
$\{Z_{\frac{\pi}{4}}, Z_{\frac{\pi}{2}}, Z_{\frac{3\pi}{4}}\}$ for Bob, where
$Z_{\theta}$ represents the basis rotated by angle $\theta$. In this case,
there are two pairs of compatible measurement bases in which cases the measured
results will be perfectly anticorrelated and which can be used to generate a
key.

On a similar note, an alternate version of BB84 called BBM92 was suggested by
Bennet, Brassard, and Mermin in @BennettEtAlQuantumCryptography1992 which also
utilize entanglement to generate the shared secret key, but which does not rely
on Bell's theorem to check for eavesdropping such as E91. In this version of
the protocol, Alice and Bob receive $n$ maximally entangled qubits from a
central source and each party independently and randomly generates an $n$-bit
string representing a choice of measurement bases between the standard basis
and the Hadamard basis. They both then measure their qubits in their respective
bases and publicly share their basis selections. 

Alice and Bob then discard their measurement outcomes on those qubits where
different measurement bases were used, and keep the rest, obtaining a string of
length $k$. At this stage, they rely on the property of entanglement to ensure
that the remaining measurement outcomes are equal. Then, Alice choose a random
subset of $\frac{k}{2}$ indices on which they compare whether the results agree
on a level above a predetermined threshold of allowed error. The remaining
string of length $\frac{k}{2}$ can then be used to generate a shared secret
key.

#### SSP and SARG04 {#sssec:ssp}

Finally, we spend some time to present two of the more notable modifications of
BB84. These protocols will not be implemented in later sections, but are
presented merely for the curious reader and as a reference for further
discussion.

The six-state protocol (SSP) was originally suggested in 1998 by Bruss
@BrussOptimalEavesdropping1998 and was subsequently studied by
Bechmann-Pasquinucci and Gisin in
@Bechmann-PasquinucciGisinIncoherentCoherent1999. In this protocol, three
conjugate bases are used to encode the original bit-string. The three bases
used is the standard basis, the Hadamard basis, and the basis
$\left\{\frac{1}{\sqrt{2}}(\ket{0} + i\ket{1}), \frac{1}{\sqrt{2}}(\ket{0} -
i\ket{1})\right\}$. Bruss showed that this modification increased the resistance to
eavesdropping since Eve in this scenario has lower probability, namely
$\frac{1}{3}$, of guessing the right basis used by Alice for measurement. By
the same property, the resulting key will be smaller than in BB84 for the
number of bits encoded as $\frac{2}{3}$rds of the generated qubits will be
discarded. Furthermore, using more than three conjugate bases for encoding does
not yield any further increase in security as the three bases used in SSP
already span the entire space of $\mathbb{C}^2$.

Another notable modification of BB84 is SARG04, first proposed by Scarani et
al. @ScaraniEtAlQuantumCryptography2004, which was developed with the intended
purpose to be more secure against photon number splitting (PNS) attacks
compared to BB84. A PNS attack allows Eve to measure qubits transmitted by
Alice in the correct basis without introducing any detectable errors. This is
possible due to a practical implementation of QKD protocols in which weak laser
pulses are used to distribute photons through a quantum channel consisting of
optical fibers. In such implementations, the laser pulses contain about 0.1
photons following a Poisson distribution. Under this distribution, most pulses
will contain no photons at all, some will contain exactly one photon, and
others will contain more than one photons. It is this last possibility that
introduces a possibility for attack. In this case, Eve may intercept the
traffic, keep the excess photons to herself and distribute the remaining one to
Bob. When Alice then presents the basis used for encoding, Eve can measure the
captured qubits in the correct basis and obtain information about the key while
remaining undetected since she is no longer constrained by the no-cloning
theorem. See Figure X for a visual representation of a PNS attack.

The SARG04 protocol tackles this possibility by changing the basis
reconciliation step of the original BB84 protocol. In SARG04, Alice uses the
same encoding states as in BB84 and transmits the state $\ket{\psi}$ to Bob.
Again, Bob announces that he has received the state and generates his own
bit-string $b' \in \{0, 1\}^n$ by which he measures the received qubits. Now,
for each qubit, Alice prepares two qubits to send to Bob -- one in the standard
basis and one in the Hadamard basis, such that the corresponding qubit is
either one of these states. With this piece of information along with his
result of the original measurement, Bob now knows that the qubit he received
initially was in either one of these states. If his measurement result was
inconsistent with one of the two states, he may deduce the state of the
original qubit which is now a shared secret between the two parties. He may
then announce to Alice that the bit is valid. If on the other hand, his result
is consistent with both states, he announces to Alice that the bit is invalid.
Finally, on the bits still remaining after this procedure, Alice and Bob may
proceed as in the original BB84 protocol. Table X shows the possible
transmissions by Alice in the basis reconciliation step, and in which cases Bob
may deduce that a bit is valid.
