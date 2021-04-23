---
layout: post
title:  "Welcome to Sympy!"
date:   2021-04-23 09:39:23 -0500
categories: sympy basics
---


# Sympy


```python
from sympy import *
```

## Expression


```python
Integer(3)
```




$\displaystyle 3$




```python
Rational(4)
```




$\displaystyle 4$




```python
type(Integer(12) % Integer(5))
```




    sympy.core.numbers.Integer




```python
factorint(42)
```




    {2: 1, 3: 1, 7: 1}




```python
type(S(1))
```




    sympy.core.numbers.One



## Symbols


```python
z = Symbol('z')
x = Symbol('x', real=True)
a = Symbol('a', positive=True)
```


```python
type(z)
```




    sympy.core.symbol.Symbol




```python
type(x)
```




    sympy.core.symbol.Symbol




```python
type(a)
```




    sympy.core.symbol.Symbol




```python
symbols('a:c, i:k')
```




    (a, b, c, i, j, k)




```python
symbols("x3:12")
```




    (x3, x4, x5, x6, x7, x8, x9, x10, x11)




```python
a = Symbol("alpha")
a
```




$\displaystyle \alpha$




```python
type(a)
```




    sympy.core.symbol.Symbol




```python
Symbol("zeta")
```




$\displaystyle \zeta$




```python
x, y = symbols('x y', real=True)
```


```python
(x+y)*(x-y)
```




$\displaystyle \left(x - y\right) \left(x + y\right)$



## Functions


```python
cos(log(2))
```




$\displaystyle \cos{\left(\log{\left(2 \right)} \right)}$




```python
type(cos)
```




    sympy.core.function.FunctionClass




```python
g = Lambda([x], 1 - x**2)
```


```python
g
```




$\displaystyle \left( x \mapsto 1 - x^{2} \right)$




```python
g(2)
```




$\displaystyle -3$



## Manipulating Expressions

```python
integer
rational
constant
symbol
```

all called `atoms`. All obey the following invariant

`expr == expr.__class__(*expr.args)`

all their properties derive solely from their type and the contents of their `.args` attribute


```python
# expression tree
srepr(g)
```




    "Lambda(Tuple(Symbol('x', real=True)), Add(Integer(1), Mul(Integer(-1), Pow(Symbol('x', real=True), Integer(2)))))"




```python
expr = exp(-x)*log(1-x)*2
expr
```




$\displaystyle 2 e^{- x} \log{\left(1 - x \right)}$




```python
srepr(expr)
```




    "Mul(Integer(2), exp(Mul(Integer(-1), Symbol('x', real=True))), log(Add(Integer(1), Mul(Integer(-1), Symbol('x', real=True)))))"




```python
list(preorder_traversal(expr))
```




    [2*exp(-x)*log(1 - x), 2, exp(-x), -x, -1, x, log(1 - x), 1 - x, 1, -x, -1, x]




```python
expr.__class__, expr.args
```




    (sympy.core.mul.Mul, (2, exp(-x), log(1 - x)))




```python
expr.args[1].__class__, expr.args[1].args
```




    (exp, (-x,))




```python
expr.atoms()
```




    {-1, 1, 2, x}




```python
expr.atoms(Integer)
```




    {-1, 1, 2}




```python
expr.atoms(Symbol)
```




    {x}




```python
g
```




$\displaystyle \left( x \mapsto 1 - x^{2} \right)$




```python
g.free_symbols
```




    set()




```python
b = Symbol('b')
```


```python
Lambda([x, y], a*x + b*y).free_symbols
```




    {alpha, b}



## Querying Properties


```python
(pi**2 - 9).is_positive
```




    True




```python
(pi**2 - 9)
```




$\displaystyle -9 + \pi^{2}$




```python
sqrt(z**2)
```




$\displaystyle \sqrt{z^{2}}$




```python
sqrt(z**2).is_real is None
```




    True



## Substitution


```python
x, y = symbols('x y', real=True)
```


```python
(cos(x) * exp(y))
```




$\displaystyle e^{y} \cos{\left(x \right)}$




```python
(cos(x) * exp(y)).subs({x: pi, y:2})
```




$\displaystyle - e^{2}$




```python
expr = exp(x+1) / (x**2-2)
expr
```




$\displaystyle \frac{e^{x + 1}}{x^{2} - 2}$




```python
expr.subs(x, 2)
```




$\displaystyle \frac{e^{3}}{2}$




```python
e = sqrt((z-1)**2)
e
```




$\displaystyle \sqrt{\left(z - 1\right)^{2}}$




```python
e.subs(z, 1+a)
```




$\displaystyle \sqrt{\alpha^{2}}$



## Simplify

* applies heuristic combination of simplification algorithms
* not a well defined concept
* what is considered simplest depends on what's done next


```python
cos(x)**2 + sin(x)**2
```




$\displaystyle \sin^{2}{\left(x \right)} + \cos^{2}{\left(x \right)}$




```python
simplify(cos(x)**2 + sin(x)**2)
```




$\displaystyle 1$




```python
cos(log(a**2))*tan(log(a**2))
```




$\displaystyle \cos{\left(\log{\left(\alpha^{2} \right)} \right)} \tan{\left(\log{\left(\alpha^{2} \right)} \right)}$




```python
simplify(cos(log(a**2))*tan(log(a**2)))
```




$\displaystyle \sin{\left(\log{\left(\alpha^{2} \right)} \right)}$




```python
radsimp, trigsimp, cancel, together, apart
```




    (<function sympy.simplify.radsimp.radsimp(expr, symbolic=True, max_terms=4)>,
     <function sympy.simplify.trigsimp.trigsimp(expr, **opts)>,
     <function sympy.polys.polytools.cancel(f, *gens, **args)>,
     <function sympy.polys.rationaltools.together(expr, deep=False, fraction=True)>,
     <function sympy.polys.partfrac.apart(f, x=None, full=False, **options)>)



## Numerical Evaluation


```python
expr = exp(x)/(x+1)
deriv = diff(expr, x)
expr
```




$\displaystyle \frac{e^{x}}{x + 1}$




```python
deriv
```




$\displaystyle \frac{e^{x}}{x + 1} - \frac{e^{x}}{\left(x + 1\right)^{2}}$




```python
N(deriv, subs={x:1.2345})
```




$\displaystyle 0.849702535502635$



## Compiling Expression
* compiles the expression into numpy code


```python

```
