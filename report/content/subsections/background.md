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

- [ ] diQKD
- [ ] quantum programming languages
