# DAE Problems

## Mathematical Specification of an DAE Problem

To define a DAE Problem, you simply need to give the function ``f`` and the initial
condition ``u₀`` which define an ODE:

```math
0 = f(t,u,du)
```

`f` should be specified as `f(t,u,du)` (or in-place as `f(t,u,du,resid)`).
Note that we are not limited to numbers or vectors for `u₀`; one is allowed to
provide `u₀` as arbitrary matrices / higher dimension tensors as well.

## Problem Type

### Constructors

`DAEProblem{isinplace}(f,u0,du0,tspan)` : Defines the DAE with the specified functions.
`isinplace` optionally sets whether the function is inplace or not. This is
determined automatically, but not inferred.

### Fields

* `f`: The function in the ODE.
* `u0`: The initial condition.
* `du0`: The initial condition for the derivative.
* `tspan`: The timespan for the problem.
* `callback`: A callback to be applied to every solver which uses the problem.
  Defaults to a black CallbackSet, which will have no effect.
* `differential_vars`: A logical array which declares which variables are the
  differential (non algebraic) vars (i.e. `du'` is in the equations for this
  variable). Defaults to nothing. Some solvers may require this be set if an
  initial condition needs to be determined.

## Example Problems

Examples problems can be found in [DiffEqProblemLibrary.jl](https://github.com/JuliaDiffEq/DiffEqProblemLibrary.jl/blob/master/src/dae_premade_problems.jl).

To use a sample problem, such as `prob_dae_resrob`, you can do something like:

```julia
#Pkg.add("DiffEqProblemLibrary")
using DiffEqProblemLibrary
prob = prob_dae_resrob
sol = solve(prob,IDA())
```
