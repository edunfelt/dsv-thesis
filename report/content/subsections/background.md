### Background {#ssec:background}

The goal of Quantum Key Distribution (QKD) is to securely share keys between
multiple parties using properties of quantum mechanics. The key property
utilized here is the fact that an entangled quantum state shared between two
parties, the definition of which is given in Section @ssec:qit, cannot be
eavesdropped upon without permanently disturbing the system in a detectable
way. So in theory, QKD promises to provide a perfectly secure way to distribute
keys between multiple parties thereby solving the inherent issue of using
symmetric encryption schemes such as the provably secure one-time pad.

The first protocol for QKD, known as BB84, was introduced by Bennet and
Brassard in @BennettBrassardQuantumCryptography2014 and did not rely on quantum
entanglement. The idea of using entanglement to prevent eavesdropping and to
obtain a perfectly random string as a shared key was suggested by Artur Ekert
in @EkertQuantumCryptography1991a, and laid the ground for the field of QKD to
this day. The primary developments within the field since Ekert's scheme mainly
concern the specification of the devices involved in the protocols.

The security proofs of the traditional QKD protocols did not take into account
attacks on the infrastructure used in the practical implementation, such as the
quantum devices used in the procedures. This was soon discovered to be
a significant flaw in these protocols as it left them vulnerable to
side-channel attacks, for instance @BrassardEtAlLimitationsPractical2000. In
general, assuming the security of the devices as characterized by the protocols
was found to be a strong assumption which left the suggested QKD schemes
fundamentally vulnerable to novel attacks targeting flaws in the device
implementation.

The solution to this issue was suggested in @MayersYaoQuantumCryptography1998
which introduced the concept of *device-independent* QKD, or diQKD. In this new
paradigm, no specifics are given as to the implementation of the quantum
devices involved. Rather, the security of the devices is proven based on their
behavior in terms of their input and output. If, during the execution of the
protocol, the devices are found to deviate from their expected behavior, the
protocol is terminated as it could indicate an ongoing attack. In modern diQKD
protocols, so-called *Bell tests* are often used to perform this check due to
its correlation properties as we will explore in Section @ssec:games. The major
drawback to diQKD is that the implementation of such protocols often is less
clear than in their device-dependent counterparts as it requires the
implementation of so-called loophole-free Bell tests, as we will discuss later.

There are also a few different approaches to generating the key ad detecting
eavesdroppers, by using different aspects of quantum mechanics. Some, like
Ekert's protocol @EkertQuantumCryptography1991a, rely on entanglement to
exchange the key through the perfectly correlated quantum particles, while
others, such as BB84, rely on Heisenberg's uncertainty principle to guarantee
that an eavesdropper will be detected by the involved parties. For
a comprehensive and recent review of the existing techniques, challenges, and
protocols within the are of QKD the interested reader may refer to
@KumarGarhwalStateoftheArtSurvey2021.

Since this thesis will focus on the implementation and simulation of QKD
protocols we here also include a note on quantum programming and techniques for
simulation. Much like for classical computers, to execute operations on quantum
processors, a quantum instruction instruction set is utilized. Today, there is
a large number of offerings in this area from a number of large corporations
and organizations. We here rely on the software development kit Qiskit, which
is further described in Section @ssec:software.
