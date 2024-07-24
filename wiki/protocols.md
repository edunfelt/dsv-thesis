# QKD Protocols

Wikipedia has a [useful
list](https://en.wikipedia.org/wiki/List_of_quantum_key_distribution_protocols)
of protocols that exist since BB84.

The survey by Kumar & Garhwal is also incredibly useful to understand the current
landscape. 

In this thesis, we focus on the most important protocols in the timeline of
entanglement based and uncertainty based protocols, and proceed chronologically.
The intention is to explain and implement the following protocols:

- [BB84](BB84.md)(implementation)
  here also the modifications made in [B92](B92.md)
- [E91](E91.md) (implementation)
- BBM92 (implementation)
  this is the entanglement-based version of E91
- Six-state protocol (explanation)
- SARG04 (explanation)
- COW protocol (implementation)
- T12 (explanation)

## Entanglement-based protocols

The first diQKD protocol, E91, was suggested by Ekert in 1991. There are several
modifications made to this protocol, but they all seem to build on the same
idea with slight changes to improve security etc. These include:

- Ekert 1991
- Acín et al. 2009 (based on 2006 idea)
- Vazirani & Vidick 2019
- Nadlinger 2022

The article by Zapatero et al. from 2023 summarizes the state-of-the-art in the
field of diQKD and can be consulted to read further about the different
implementations of the CHSH key-distribution protocol that exists.

Basically, any non-local game with proven quantum advantage could be used. An
idea here is to look into other games for which I can derive a test of
entanglement. However, it is not clear to me how using another game could be
advantageous. Nonetheless, it might be of interest to the community to know
about different possibilities.

There are also variations of other QKD protocols that use entanglement as an
alternative method instead of one party being the source. These protocols include
BB84, SSP, and SARG04.

## Uncertainty-based protocols

Other protocols that do not rely on entanglement include the original BB84, BBM92,
B92, the six-state protocol, SARG04, and the COW protocol.
