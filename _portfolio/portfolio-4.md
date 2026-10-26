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

Find [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Finite_Volumes) my 1D implementation of the basic finite volumes method : 

$$u_i^{n+1} = u_i^n + \frac{\Delta t}{\Delta x} \Big( \mathcal{F}_{i+\frac{1}{2}} - \mathcal{F}_{i-\frac{1}{2}} \Big)$$

On some classical examples of hyperbolic conservation laws (Burgers, BBM...),

$$\partial_t u(t,x) + \partial_x f(u)(t,x) = 0 $$

or advection equations,

$$\partial_t u(t,x) + \partial_x \big( \beta(t,x) u(t,x) \big) = 0$$

with Dirichlet or periodic boundary conditions.

## Finite elements method 

Find [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Lagrange_FEM_Poisson) a 1D implementation of the Lagrange finite elements method on the classical Poisson problem,

$$- \Delta u = f$$

The main idea of the finite elements method is to transform the weak continuous problem (generally defined on Sobolev spaces) to a discrete weak formulation using polynomial test functions, defined on each cell of the mesh $T_h$. The numerical solution $u_h$ is then sought in the form,

$$u_h(t,x) = \sum_{K\in T_h}\sum_{i=0}^{d}u_i^K(t)\phi_i^K(x)$$

Where $(\phi_i^k)_{0 \leq i \leq d}$ is a polynomial basis (often a Lagrange basis) which interpolate functions of the continuous space $V$ to the discrete space $V_h \subset C^0(\Omega)\cap\mathbb{P}^d(T_h)$ on each cells $K \in T_h$.
The continuous problem is thus transformed into a linear problem in a finite dimension space. The discrete formulation reads : 
Find $u_h \in V_h$ such that for every $v_h \in V_h$ 

$$a_h(u_h,v_h) := \sum_{K \in T_h}\int_{K}\nabla u_h \cdot \nabla v_h = \int_{\Omega}fv_h $$

Letting $$A_h := \Big(\sum_{K \in T_h}a_h(\phi_i^K,\phi_j^K)\Big)_{0\leq i,j \leq d}$$, the linear problem problem reads, 

$$A_hU_h=B_h$$

## Discontinuous Galerkin method 

The discontinuous Galerkin method can be seen as a generalization of the finite element method to discontinuous spaces of functions. The idea is the same as the classical finite elements methods, but instead of a discrete space of continuous polynomials, the formulation use polynomials that are not necessarily continuous accross cell interfaces. The coupling of cells is then made through jumps or means values on interfaces, making this formulation close to the finite volumes one.

The discontinuous Galerkin method is often associated with modal approach, with modal polynomial basis as evocated earlier.

### Symmetric interior penalty discontinuous Galerkin (SIP-dG) method 

See [here](https://github.com/HerrBronstein/Numerical-Methods-Tools/tree/main/Discontinuous_Galerkin_Poisson) the code associated with the SIP-dG method.
The discrete bilinear form reads,

$$a_h(u_h,v_h)=\sum_{K \in T_h}\bigg( \int_{K} \nabla u_h \cdot \nabla v_h - \sum_{F \in F_K}\int_{F} \Big( \llbracket u_h \rrbracket \cdot \avg{\nabla v_h} +  \llbracket  v_h \rrbracket \cdot \avg{\nabla u_h} \Big) + \sum_{F \in F_K} \int_{F} \frac{\eta}{h_F} \llbracket u_h \rrbracket \llbracket v_h \rrbracket \bigg)$$

With $\llbracket \cdot \rrbracket$ jump and $\avg{\cdot}$ mean on the interface considered. 

$\eta > 0$ is a parameter that ensure the coercivity of the discrete bilinear form $a_h$, choosen arbitrary.

### Hyperbolic discontinuous Galerkin method 

Let's consider a general scalar conservation law,

$$\partial_t u + \partial_x f(u) = 0$$

With $f$ a physical flux function. Let $d\in \mathbb{N}$ be a polynomial degree. By choosing $v_h \in C^1(\Omega)$, we can establish a weak formulation of the problem on a cell $K \in T_h$,

$$\int_{K} \partial_t u v_h - \int_{K} f(u) \partial_x v_h + \int_{\partial K} f(u) v_h = 0$$

In the classical finite elements method, we would have changed $u$ for $u_h$ in the formulation, but in the discontinuous setting there is no reason that the flux $f$ stays continuous accross interfaces, since $v_h$ and $u_h$ are in $\mathbb{P}^d_K(T_h)$. The discrete weak formulation introduce a numerical flux $\widehat{F}$ (as well as in the finite volumes method), that we can choose later according to the physical flux considered, among a wide choice : global Lax-Friedrichs, Rusanov, Murman-Roe, Godunov...
The semi-discrete formulation reads,

$$\int_{K} \partial_t u v_h - \int_{K} \widehat{F}(u) \partial_x v_h + \int_{\partial K} \widehat{F}(u) v_h  = 0$$

By taking $v_h = \phi_j^K \in \mathbb{P}(K)^d$, we can finally write the linear system verified by the discrete weak formulation on the cell $K$,

$$M\Big( \frac{\text{d}}{\text{d}t}U_h^K\Big) + \widehat{F}^{\partial K} - \widehat{F}^K = 0$$

With $M$ the mass matrix of the associated polynomial basis.

## Hybrid high-order (HHO) method 
Not coded yet but this is a future goal !
