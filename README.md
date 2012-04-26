# QuantumBoosty

A few files to demonstrate some useful C++ features for integrating Schrödinger and master equations. These files use ublas (from [Boost](www.boost.org)) and the [odeint](www.odeint.com) library, which is currently in the Boost sandbox. Users may also find the [expm.hpp](https://www.dbtsai.com/blog/2008-11-25-matrix-exponential/) implementation of the general matrix exponential helpful for time independent systems.

## Background

One of the largest problems I came up against when working with C or Fortran was the lack of useful integrators. Obviously integrators are available, but I found myself jumping through hoops. In the case of C, I was using the GSL library, which both defines its own complex type (C has had its own since C99) and then fails to use it for the integrator routines, necessitating the doubling of the size of the system. That's not all that difficult in practise, but it's a an additional layer in the code that doesn't help readability. Worse, the routines rely on arcane drivers which means cracking out the manual, which is also unhelpful. In the case of Fortran, the VODE integrators are good, but require your program to be arranged in a particular way. Not so good for plug and play ODE solving.

Recently I came across the C++ [odeint](www.odeint.com) library. I was so impressed by its flexibility that I actually started using C++ (having had no prior experience) just for the convenience of it. I'm glad that I did this, because C++ has some other very useful features that make solving quantum mechanical systems simpler. Probably the most important feature that I use (perhaps abuse) is functors, a kind class with which instances can be used as functions. As an example of why this is useful, consider a Hamiltonian. The Hamiltonian can have time independent parts and time dependent parts, which add together to give the complete Hamiltonian. Most of the Hamiltonian can be determined upon instantiation, and only time is unknown, which will be the sole varable that the fuctor takes when behaivng as a function.