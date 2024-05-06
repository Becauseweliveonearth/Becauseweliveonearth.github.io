---
title: Interposers(RF Considerations)
date: 2024-01-29 09:12:00 Z
---

Interposers are simple substrates used in connecing multiple chips paicularly in cases of heereogenous integraion.

Heterogeneous integration is a complex process that involves integrating different materials, devices, and systems to create new functionalities. Some of the challenges in heterogeneous integration include:
•	Reliability: Heterogeneous integration requires a convergence between the semiconductor industry and the packaging industry, and a unified reliability approach across the entire product architecture hierarchy from device level to package, boards/modules, and systems 1.
•	Design complexity: The design of interconnect interfaces and standards for diverse heterogeneous chips faces difficulties in balancing performance and flexibility in terms of technology and competitions for market domination 2.
•	Performance: The core packaging technologies of chiplets face challenges in performance, power consumption, cost, and so forth 2.
•	Heterogeneity: The heterogeneity of devices, formats of data, communication, and interoperability issues due to heterogeneity pose significant challenges in the integration of heterogeneous Internet of Things 3.

These complexities carry over to the design of interposers where Heterogeneous Integration design problems as related to interposers for HPC applications has recently gained momentum to not only enhance electrical, signal, routing, thermal, floor placement and mechanical properties but also control the performance and yield while managing cost. Each interposer parameter, i.e. material property thickness has different competing effects on the impedance matching, routing, assembly procedure, electrical, signal integrity, Power distribution network and thermal sub-system depending on the signal requirements.  The final design composition of these systems is thereby mainly governed by several considerations and tradeoffs between the systems and overall specifications that yield limited performance improvements. The reasons being, achieving a theoretical maximum performance requires 
1) extensive and complex model prototyping
2) Interactive analysis of package systems and tradeoffs and extensive design space exploration
3) and limited optimization methods and design flow specific to RF data methods.

1) extensive and complex model prototyping: Initial work has been done to apply modern data-driven Machine Learning (ML) to RF systems beyond standard tools that use models and equations based on idealized assumptions and approximations regarding hardware, environment, and the problem being solved.
2) Interactive analysis of package systems and tradeoffs and extensive design space exploration:
3) and limited optimization methods and design flow specific to RF data methods.

Methodology:
Decompositional electromagnetic analysis (diakoptics)
 Divide, build or find models for elements and unite the models
 Accurate and fast analysis of signal integrity (depends on
accuracy of the component models)
 May include coupling between nets and to parallel planes 
Reference[https://www.simberian.com/Presentations/14-MP2_Shlepnev_ElementsOfDecompositionalAnalysisOfInterconnects.pdf]

More reference:
iakpics popularied by Kron n the couse of  unifying study of basic problems in engineering sciences by means of geometry [Kazuo Kondo (1973) "An Oriental Expansion of Kron’s Science beyond Electrical Engineering", pp 153–64 in Gabriel Kron and Systems Theory, H.H. Happ editor, Union College Press OCLC 613720 ISBN 978-0-912156-02-6, see p 154]
Orginal works in the field of emag show he application of diakoptics

https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=508531
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=276728

Doing research with what I know and not what I don't know

Diakoptics is solving in time domain
Not needed if we are doing sparameers in frequency domain an using FEM 3D solvers which use the best algorithims.

From Ivan Ndip:
Multilumped
modeling, which is traditionally used for uniform transmission lines, where only the
fundamental mode (e.g., TEM or quasi-TEM) exists, was successfully applied for the first
time to develop wideband models for complete signal paths in complex SiP modules, where
both the fundamental as well as higher-order modes (HOMs) exist. Since the multilumped
modeling technique generally entails a segmentation of the uniform transmission line,
separate modeling of each portion and cascading the results to increase bandwidth, the
complete signal paths in the SiP module also had to be segmented at points where only the
fundamental mode exists. For this purpose, a novel methodology was first developed to define
the electrical boundaries of all geometrical discontinuities (e.g., flip chip interconnects, bends
on package traces, vias, BGA balls…) along an entire signal path, i.e., the points away from
the physical boundaries of each discontinuity where fields of HOMs, excited at the
discontinuity vanish or become insignificant (end of discontinuity effect), and the
fundamental mode continues unperturbed. Based on these boundaries, the path was then
segmented and novel modeling techniques were used to extract wideband models for each
segment. 
[methodolgy.JPG](/uploads/methodolgy.JPG)
This is mainly because lumped/distributed element modeling is based on
TEM wave theory. 
As will be illustrated in the next chapter, without defining the electrical
boundaries of these discontinuities, a conventional circuit-theory-based analysis fails to
accurately capture the effects of a discontinuity. Consequently, defining the electrical
boundaries of each package/board discontinuity is a pre-requisite for efficient and accurate
wideband modeling and analysis of complete signal paths in electronic packages and boards
for RF/high-speed applications. 
Secondly, to perform 3D full-wave EM field computations of discontinuities using
conventional field solvers, they are connected to ports using uniform transmission lines (e.g.,
microstrip, stripline...), which represent the actual configuration of traces in the package or
board. The length of the transmission line used for this interconnection depends on the
electrical boundaries of the discontinuity under consideration, and it determines the accuracy,
duration and memory requirements of the field computation. If the transmission line is too
short, then HOMs excited at the discontinuity will be captured at the ports. This will lead to
erroneous results. If the transmission line is longer than required, then the field computation
20
time and memory required will increase, leading either to unsuccessful computations due to
insufficient memory or computations that may run for days, instead of just a few hours. 

Basically in summary. Ref: https://api-depositonce.tu-berlin.de/server/api/core/bitstreams/63956721-07c8-4b75-b3c3-68a45e462bfd/content
Since a represents the substrate thickness, it can be deduced from (3.45) that the Lo-HOM can
only propagate if this thickness is greater than, or equal to half the wavelength of the
propagating signal. This indicates that for SiP modules used for RF/high-speed applications
with very thin dielectric substrates, HOMs can not propagate. Once excited, they will always
decay exponentially with distance away from the point of excitation. 


Basically what I was wondering: This variation in power, as we move away from the discontinuity, can also be seen in Sparameters since S-parameters can be derived directly from power. For example, 2
Snn is
equal to the ratio of power reflected from, to power incident on, an n-port. However, for the
computation of these S-parameters, a numerical technique (e.g., the finite element method)
that solves the complete wave equation must be used so as to take into consideration the
effects of all the modes. Prior to performing such a computation, an accurate EM model of the
discontinuity and its interconnecting traces must first be defined. This involves creating the
geometry, assigning the material parameters, setting-up the necessary boundary conditions,
defining the source of excitation and the frequency of interest. Only the fundamental mode
has to be excited at the ports, since only the effects of the HOMs on this fundamental mode
are of interest in defining the boundaries of the discontinuities. Furthermore, to prevent the
frequency-dependent losses, given by Pl in (3.53), if any, from overshadowing the results, the
S-parameters have to be computed only at a single frequency point – the highest frequency of
interest. After the field computation, the extracted S-parameters shouldn’t be renormalized to
any impedance, since this may influence the results. In the next chapter, it will be explained
how S-parameters were computed in this work.

Different lengths of the interconnecting traces needed for the field computations are taken
from (3.51). At the end of the field computations, nn S is plotted against these lengths. From
this plot, it will then be seen that as the electrical boundaries of the discontinuity is
approached, nn S converges to a particular value and then becomes constant for a while.
Therefore, the electrical boundaries of discontinuities, represented by bod l , can be defined as
follows:
If
0 nn nn l ll S S +∆ − ≈ , (3.54)
then bod l l = .
Depending on the problem at hand, the electrical boundaries of a discontinuity can also be
defined as the point away from the discontinuity where nn S changes by less than a self defined
limit, e.g., 5%. 

. The solutions of such
full-wave computations are normally exported as S-parameters, and contain all field
components describing the modes associated with the segment, i.e., the HOMs as a result
of the 3D component and TEM or quasi-TEM modes due to the uniform interconnecting
traces. 

Generally, cascaded sections of two-ports (see Figure 3. 11) can be analyzed by multiplying
T-matrices of individual sections to yield the T-matrix of the overall network, as shown in
(3.69). Generally, cascaded sections of two-ports (see Figure 3. 11) can be analyzed by multiplying
T-matrices of individual sections to yield the T-matrix of the overall network, as shown in
(3.69). 

Each wideband model developed in this work is represented by a set of S-parameters.
However, S-matrices cannot be cascaded, because some of the variables at the port are
independent while the rest are dependent. Therefore, the S-matrices obtained from each
segment must first be converted to transfer scattering or T-parameters using the following
relationship then reconverted back.

Two major Considerations forr he design:
1. Optimal Choice and Design of Critical Components:
2. Consideration of the Effects of Technological Tolerances at the Beginning of the
Design Cycle so i doesn't go ou of desired range.

[methodolgy2.JPG](/uploads/methodolgy2.JPG)

Examples given, plot of 3D EM, showing the change away from the port
Great Job!

I previously wanted people to applaud me for having a lo of math in my dissertation but I do not really care how I appear anymore, simply my contributions to the field. Hopefully they have enough people oing mah.

Once we have ascerained this is an acceptable mehodology, all of the measurements and verifications come in.

Nothing new so far.

Side note, can evaluate tolerances for MRR.

Gotten from this excercise: great accurate models, statistical analysis/relative change. 

To be used for PC methods, linear regression, how the model changes, scaling the model.

Conlusion: Observed pattern of trail-off. Maybe can use that in an optimization scheme/algorithim.

Phase 1 Finished.