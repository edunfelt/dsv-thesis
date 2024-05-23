### Research Strategy {#ssec:strategy}

We recall that the research questions addressed in this thesis as stated in
Section @ssec:researchq are:

1. How does simulations of prominent QKD protocols compare in terms of size of
   the keys generated and error in key generation?
2. How can QKD protocols be extended to be diQKD and what is the impact on their
   efficiency in this case?
3. What are the practical and theoretical benefit and drawbacks of using
   entanglement for key generation over relying on the Heisenberg uncertainty
   principle?

To address these questions, we choose to employ a experimental research
strategy as discussed in @DenscombeGoodResearch2010. An experimental study will
allow us to generate quantitative data through simulations and theoretical
analysis which can be used to answer the questions as posed. Firstly,
experimental simulations in Qiskit will produce data that can clearly
demonstrate the size of the keys generated from different protocols and
techniques as the number of qubits increase, as well as the impact on error
rates. Furthermore, based on a theoretical analysis of possible modifications
to existing protocols, quantitative data can be produced through subsequent
experiments to compare the impact of using different quantum techniques as
a basis for protocols in QKD, thus answering question four.

An experimental approach is taken in favor of other strategies since the
primary goal is to produce data from controlled simulations of protocols in QKD
in order to deduce the impact and relationship between certain properties.
Through experiments, a neutral view in which the impact of the parameters of
interest can be obtained in order to draw conclusions on the efficiency and
correctness of different approaches. This further opens up for testing new
approaches to existing protocols.
This approach is also repeatable in that the source code of the simulation will
be provided in the report as a means for further research into the area.

The output of conducted experiments will be numerical quantitative data
corresponding to the investigated variables, due to the experiments being
simulations of executing the QKD protocols for varying parameters.

The research process will proceed in several stages, the first of which is data
collection by implementing the identified QKD protocols in Qiskit and run
simulations. In this stage, a theoretical analysis of the protocols will also
be carried out in order to identify whether it is possible to modify existing
QKD protocols into diQKD, after which further experiments are performed. Next,
the resulting data is prepared and explored in order to identify possible
trends and identify suitable statistics. Then, proper data analysis will be
performed in order to produce descriptive statistics that can be used to answer
the research questions. The statistics will then be presented in the form of
plots and tables showing the relevant results. The remainder of this chapter
will discuss the details of these stages.
