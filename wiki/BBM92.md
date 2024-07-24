# BBM92 protocol

BBM92 is an entanglement-based version of [BB84](BB84) which does not rely
on Bell's theorem, in contrast to [E91](E91). It is the first steps of BBM92
which differ from BB84:

1. Alice creates an $n$-bit string.
2. Alice and Bob receive an entangled qubit from an external source.
3. Alice chooses $n$ random bases, either the standard or the Hadamard basis
   and Bob does the same. They both measure the state using their selected
   bases and then publish the basis selection.
4. Both Alice and Bob keep the $k$ qubits on which they measured in the same basis
   and discard the rest. 
5. Alice randomly chooses a subset $I$ of indices of the remaining qubits, of
   size $k / 2$ and sends these to Bob.
6. Alice and Bob compare whether their bits on these indices agree above a
   predetermined threshold. If they do, the remaining bits can be used as a
   shared secret key.
