---
title: "Numerical methods and tools : personnal project"
excerpt: "In my free time I code some numerical analysis tools and/or methods in C++ in order to create a framework for later"
collection: portfolio
share: false
---

See the [full repository](https://github.com/HerrBronstein/Numerical-Methods-Tools).

During my master degree courses, I had to learn some basics of C++ programmation for scientific computing. 
As exercises, we had to create classes for useful tools in numerical analysis such as polynomial basis, interpolation, basic finite volumes method... Later, in the context of [supervised research projet](https://herrbronstein.github.io/portfolio/portfolio-2/), we had to implement the numerical resolution of the Benjamin-Bona-Mahony equation using various methods through hybrid schemes (finite differences, finite volumes and discontinuous Galerkin). 

As a personnal project I decided to create a framework that could be useful for future use. You can find some more tools and methods here, mostly in the one dimensional case for the moment. 

## General tools
### Interpolation
### Time solving schemes
### Meshes

## Polynomial basis

Find [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Polynomials) some polynomial basis, useful for Galerkin type methods. Since differents approaches are possible for Galerkin type methods, nodal or modal essentially, we are led to use differents types of polynomial basis. 

For the nodal case, for instance, we want to represent the degrees of freedom through the values taken by the polynomials in some well-choosen nodes in the cells. The main choice for this type of approach is the Lagrange polynomial basis, constructed with the Lagrange interpolation polynomials in the cell. 

In the modal case, we represent the degrees of freedom through the degree of polynomials used to interpolate the exact solution. In this approach, the polynomials are not based on nodes in the cells, they represent a decomposition into oscillation modes. The values of the polynomials does not represent a physical value, so for the numerical solution a reconstruction is needed to recover the physical values of the solution on the nodes. 
In order to do so, we have an important choice of polynomial basis (with different properties), such as the Tchebychev basis (which minimizes the Gibbs effect) or the Legendre basis (with interesting orthogonality properties).


## Finite volumes method

Find [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Finite_Volumes) my 1D implementation of the basic finite element method on some classical examples of hyperbolic conservation laws (Burgers, BBM...),
$$ \partial_t u + \partial_x f(u) = 0  $$
or advection equations,
$$ \partial_t u + \beta(t,x) \partial_x f(u) = 0 $$
with Dirichlet or periodic boundary conditions.

## Finite elements method 

Find [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Lagrange_FEM_Poisson) a 1D implementation of the Lagrange finite elements method on the classical Poisson problem,
$$ - \Delta u = f $$

## Discontinuous Galerkin method 
### Symmetric interior penalty discontinuous Galerkin method 
### Hyperbolic discontinuous Galerkin method 

## Hybrid high-order (HHO) method 
Not coded yet but this is a future goal !
