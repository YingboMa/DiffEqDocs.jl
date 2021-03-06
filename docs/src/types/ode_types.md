# ODE Problems

## Mathematical Specification of an ODE Problem

To define an ODE Problem, you simply need to give the function ``f`` and the initial
condition ``u₀`` which define an ODE:

```math
\frac{du}{dt} = f(t,u)
```

`f` should be specified as `f(t,u)` (or in-place as `f(t,u,du)`), and `u₀` should
be an AbstractArray (or number) whose geometry matches the desired geometry of `u`.
Note that we are not limited to numbers or vectors for `u₀`; one is allowed to
provide `u₀` as arbitrary matrices / higher dimension tensors as well.

## Problem Type

### Constructors

`ODEProblem{isinplace}(f,u0,tspan,callback=CallbackSet(),mass_matrix=I)` :
Defines the ODE with the specified functions. `isinplace` optionally sets whether
the function is inplace or not. This is determined automatically, but not inferred.

### Fields

* `f`: The function in the ODE.
* `u0`: The initial condition.
* `tspan`: The timespan for the problem.
* `callback`: A callback to be applied to every solver which uses the problem.
  Defaults to nothing.
* `mass_matrix`: The mass-matrix. Defaults to `I`, the `UniformScaling` identity matrix.

## Example Problems

Example problems can be found in [DiffEqProblemLibrary.jl](https://github.com/JuliaDiffEq/DiffEqProblemLibrary.jl/blob/master/src/ode_premade_problems.jl).

To use a sample problem, such as `prob_ode_linear`, you can do something like:

```julia
# Pkg.add("DiffEqProblemLibrary")
using DiffEqProblemLibrary
prob = prob_ode_linear
sol = solve(prob)
```

```@docs
DiffEqProblemLibrary.prob_ode_linear
DiffEqProblemLibrary.prob_ode_2Dlinear
DiffEqProblemLibrary.prob_ode_bigfloatlinear
DiffEqProblemLibrary.prob_ode_bigfloat2Dlinear
DiffEqProblemLibrary.prob_ode_large2Dlinear
DiffEqProblemLibrary.prob_ode_2Dlinear_notinplace
DiffEqProblemLibrary.prob_ode_threebody
DiffEqProblemLibrary.prob_ode_pleides
DiffEqProblemLibrary.prob_ode_vanderpol
DiffEqProblemLibrary.prob_ode_vanderpol_stiff
DiffEqProblemLibrary.prob_ode_rober
DiffEqProblemLibrary.prob_ode_rigidbody
```
