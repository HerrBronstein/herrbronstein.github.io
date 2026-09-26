---
title: "Supervised research project : Benjamin-Bona-Mahony (BBM) equation"
excerpt: "A general study (from mathematical modelling, including theoretical study, to numerical analysis and computation) of BBM equation "
collection: portfolio
share: false
---
During this project with [Adrien Martinelli](https://github.com/SequoiaCode), we studied the Benjamin-Bona-Mahony (BBM) equation, describing long wave of small amplitude in dispersive medium (solitons for instance). The equation writes : 

$$\partial_t u + \partial_x u + u \partial_x u - \partial_{txx}^3 u = 0$$

This model can be seen as a variation of the Korteweg - de Vries equation, by substituting $\partial_{x}^3$ by $-\partial_{txx}^3$.

The first part of our work is dedicaced to physical motivation, derivation and justification of the mathematical model (first by deriving Korteweg- de Vries equation, and then by justifying the variation of the KdV equation by the original 1972 article).
From this model, we then discussed and proved some mathematical properties, such as existence, uniqueness and regularity of solutions or finite number of conservations laws.

The last part of our work is about numerical analysis and numerical method adaptated to the resolution of the BBM equation. 
The nature of the differents terms leds us to consider hybrid schemes to deal with both hyperbolic and dispersive/elliptic terms.
So as to, we introduced three types of numerical schemes, two hybrid schemes : finite volumes / finite differences, MUSCL / finite differences and a full discontinuous Galerkin scheme, using both hyperbolic formulation and elliptic symetric interior penalty (SIP) formulation.
After theoretical study and computation of these schemes, we put the emphasis on the gain of order due to MUSCL formulation for the hyperbolic part of the equation.

The report also contains some proofs for functional analysis results used for the convergence proof of our first hybrid scheme.

Supervised by [Fabien Marche](https://imag.umontpellier.fr/~marche/).


See [report](/files/BBM_report.pdf) / [slides](/files/Présentation_BBM.pdf)

Find the full project on my GitHub [here](https://github.com/HerrBronstein/Benjamin-Bona-Mahony-BBM-equation)
