### Software Use and Implementation {#ssec:software}

There are a number of available software development kits (SDKs) available for
running simulations of quantum algorithms both on local machines and sometimes
on quantum infrastructure. In this project, we choose to implement the
experimental part in the Qiskit SDK which is an open-source software stack
developed by IBM supporting the OpenQASM instruction set for quantum circuits.
Crucially, this Python-based SDK supports execution on real quantum hardware from
IBM as well as other vendors @QiskitIBM.

IBM's cloud-based ecosystem for running and developing quantum computing
operations is by far the most used platform, as well as the Qiskit SDK being
the leading choice of quantum library by developers as found in @StateQuantum.
While the market has other offerings for running quantum tasks in the cloud,
such as AWS Braket with their SDK, or Google's Cirq SDK, these follow quite far
behind in the same survey. The popularity of Qiskit and the IBM tools ensure
that the simulations can be executed on a wide variety of hardware and provide
state-of-the-art solutions @QiskitEcosystem.

Qiskit was originally released in 2017 and consisted then of four elements;
Terra, Aqua, Ignis, and Aer @CelebratingQiskit. Qiskit Terra is the foundation
of the Qiskit SDK as it stands today, supporting execution of quantum circuits.
Both Qiskit Aqua and Ignis are deprecated in recent versions of Qiskit, and was
originally developed to build quantum applications and work on error
mitigation. Current infrastructure offers this functionality as applications or
so-called experiments. Finally, Qiskit Aer was built to perform
high-performance quantum simulation with realistic noise. Aer extends Qiskit
with the ability to simulate algorithms using different levels of noise on
local hardware to provide researchers with a resource efficient method for
running realistic experiments @QiskitAer.

For a deeper review of the Qiskit SDK, a recent preprint by researchers at IBM
Quantum which outlines its design and components, can be consulted
@Javadi-AbhariEtAlQuantumComputing2024.
