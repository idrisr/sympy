---
layout: post
title:  "Sympy Calculus"
date:   2021-04-23 09:39:23 -0500
categories: sympy basics
---



# Calculus


```python
from sympy import *
```

## Derivatives


```python
x = Symbol('x')
```


```python
diff(exp(x**2), x)
```




$\displaystyle 2 x e^{x^{2}}$




```python
diff(x**2, x)
```




$\displaystyle 2 x$




```python
f = Function('f')
f
```




    f




```python
diff(f(x**2), x)
```




$\displaystyle 2 x \left. \frac{d}{d \xi_{1}} f{\left(\xi_{1} \right)} \right|_{\substack{ \xi_{1}=x^{2} }}$



## Limits

## Integrals


```python
integrate(sin(x))
```




$\displaystyle - \cos{\left(x \right)}$




```python
integrate(sin(x), (x, 0, pi))
```




$\displaystyle 2$




```python
Integral(sin(x), (x, 0, pi))
```




$\displaystyle \int\limits_{0}^{\pi} \sin{\left(x \right)}\, dx$



## Taylor Series

## Solving Equations


```python

```
