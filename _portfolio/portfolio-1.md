---
title: "Supervised research project : Benjamin-Bona-Mahony (BBM) equation"
excerpt: "A general study (from mathematical modelling, including theoretical study, to numerical analysis and computation) of BBM equation "
collection: portfolio
share: false
---
Supervised by [Fabien Marche](https://imag.umontpellier.fr/~marche/).

During this project with [Adrien Martinelli](https://github.com/SequoiaCode), we studied the Benjamin-Bona-Mahony (BBM) equation, describing long wave in dispersive medium (solitons for instance). 

The first part of our work is dedicaced to physical motivation, derivation and justification of the mathematical model (first by deriving Korteweg- de Vries equation, and then by justifying the variation of the KdV equation by the original 1972 article).
From this model, we then discussed and proved some mathematical properties, such as existence, uniqueness and regularity of solutions or finite number of conservations laws.

The last part of our work is about numerical analysis and numerical method adaptated to the resolution of the BBM equation. 
The nature of the differents terms leds us to consider hybrid schemes to deal with both hyperbolic and dispersive/elliptic terms.
So as to, we introduced three types of numerical schemes, two hybrid schemes : finite volumes / finite differences, MUSCL / finite differences and a full discontinuous Galerkin scheme, using both hyperbolic formulation and elliptic symetric interior penalty (SIP) formulation.
After theoretical study and computation of these schemes, we put the emphasis on the gain of order due to MUSCL formulation for the hyperbolic part of the equation.

The report also contains some proofs for functional analysis results used for the convergence proof of our first hybrid scheme.


See report / slides
Find the full project on my github [here](https://github.com/HerrBronstein/Benjamin-Bona-Mahony-BBM-equation)
