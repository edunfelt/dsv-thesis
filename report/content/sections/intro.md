## Introduction {#sec:intro}

Modern cryptography is a field that is largely concerned with the development
of secure algorithms for symmetric or asymmetric encryption, either relying of
complex shuffling procedures in the case of the former, or on complex
mathematical problems in the latter case. Both types of encryption schemes come
with certain drawbacks that make them more or less viable in different
scenarios. For instance, asymmetric encryption by its often mathematical nature
can be quite computationally intensive, especially on a larger scale. On the
other hand, symmetric encryption relies on the distribution of a shared key
that needs to stay secure from prying eyes. For this reason, the two types of 
encryption are most often used in conjunction with one another, where asymmetric
cryptography is used to distribute a private key that is then later used in a 
symmetric encryption scheme. Such is the case with TLS, which is used in virtually
all communication on the Internet today.

However, with the advent of quantum computers, the asymmetric encryption
schemes used today are threatened as the new computational powers captured by
quantum mechanics allows adversaries to tackle the mathematical underpinnings
of most such schemes. In this work, we investigate an alternative approach to
cryptography, or more specifically to the key distribution phase of secure
communication, that also utilize the powerful properties of quantum
computation. Through quantum key distribution, it is possible to obtain methods
for distributing private keys without relying on classical asymmetric
encryption schemes.
