# SARG04 protocol

SARG04 is yet another modification of [BB84](BB84) in which one additional change is
made in that Alice does not reveal the basis $b$ of her bit, which ensures that
a potential eavesdropper needs to store more copies of the qubit in order to be
able to determine the state, compared to the original protocol.

1. Alice creates two $n$-bit strings $a$ and $b$. She encodes the information
   as an tensor product of $n$ qubits where each individual qubit corresponds
   to one bit of $a$ and $b$ such that $b_i$ determines the encoding basis of
   $a_i$. Four mutually orthogonal basis states are used -- the Hadamard basis
   and the standard basis. The state is transmitted to Bob.
2. Bob randomly generates a bit string $b'$ of length $n$ deciding in which
   basis to measure the qubits of the quantum state. Measurement yields a bit
   string $a'$. Bob announces that he is ready.
3. For each transmitted qubit, Alice prepares one state in the computational
   basis and one in the Hadamard basis and sends these to Bob.
4. For each qubit, Bob checks whether his measurement is consistent with either
   of the possible states. If it is consistent with both, the bit is announced
   to be invalid since he cannot determine which state was actually
   transmitted. Likewise, if one o the states is inconsistent with the
   measurement, the bit can be announced to be valid since he can deduce the
   state and thus also the original bit.
5. Alice randomly chooses a subset $I$ of indices of the $k$ bits on which
   Bob's measurement was conclusive, of size $k / 2$ and sends these to Bob.
6. Alice and Bob compare whether their bits on these indices agree above a
   predetermined threshold. If they do, the remaining bits can be used as a
   shared secret key.
