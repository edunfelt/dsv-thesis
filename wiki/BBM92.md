# BBM92 protocol

BBM92 is an entanglement-based version of [BB84](BB84.md) which does not rely
on Bell's theorem, in contrast to [E91](E91.md). It is the first steps of BBM92
which differ from BB84:

1. Alice creates an $n$-bit string.
2. Alice and Bob receive an entangled qubit from an external source.
3. Alice chooses $n$ random bases, either the standard or the Hadamard basis
   and Bob does the same. They both measure the state using their selected
   bases and then publish the basis selection.
4. Both Alice and Bob keep the qubits on which they measured in the same
   basis and discard the rest.
5. 
