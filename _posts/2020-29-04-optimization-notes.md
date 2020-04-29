---
layout:     post
title:      "Optimization Notes"
subtitle:   " "
date:       2020-04-20 12:00:00
author:     "Alejandro Blumentals"
---

# 1. Disciplined Convex Programming
Here I gather some notes from Stephen Boyd's short course on [optimization](http://web.stanford.edu/~boyd/papers/cvx_short_course.html). The main idea is to prove convexity (or construct a convex program) by having convex atom functions and use operations that preserve convexity.

## 1.1 Convex Atom Functions

* $x^p$ ($p>1$ or $p\leq0$)
* $x\log x$ (negative entropy)
* $a^T x + b$ (affine)
* $x^T P x$ for $P\succcurlyeq 0$ (quadratic forms for positive semidefinite matrices)
* $\vert \vert x \vert \vert$ any norm
* $\max (x_1, ..., x_n)$
* $\frac{x^2}{y}$ for $y>0$ (quad over lin, cvx in x and y)
* $\frac{x^T x}{y}$ for $y>0$ (quad over lin, cvx in x and y)
* $x^T Y^{-1} x$ for $Y\succ 0$ (least squares with inverse weights, cvx in x and Y)
* $\log(e^{x_1}+...+e^{x_n})$ (log sum exp)
* $x_{[1]}+...+x_{[k]}$ (sum of largest k entries in a vector)
* $x\log(\frac{x}{y})$ for $x,y>0$ (KL)
* $\lambda_{\max}(X)$ for $X$ symmetric (largest eigenvalue)

## 1.2 Concave Atom Functions
* $x^p$ ($0\leq p\leq 1$) e.g $\sqrt{x}$
* $log x$
* $\sqrt{xy}$ (geometric mean)
* $a^T x + b$ (affine)
* $x^T P x$ for $P\preccurlyeq 0$ (quadratic forms for negative semidefinite matrices)
* $\min (x_1, ..., x_n)$
* $\log \det(X)$ for $X\succ 0$
* $(\det(X))^{\frac{1}{n}}$ for $X\succ 0$
* $\log \Phi (x)$ (where $\Phi$ is the Gaussian cdf)
* $\lambda_{\min}(X)$ for $X$ symmetric (smallest eigenvalue)
  
## 1.3 Calculus Rules for preserving convextity
* Non negative scaling
* Sum
* Affine composition: $f$ cvx $\implies$ $f(Ax+b)$ cvx
* Pointwise max: $f_1,.., f_n$ cvx $\implies$ $\max_i f_i(x)$ cvx
* Composition: $h$ cvx increasing and $f$ cvx $\implies$ $h(f(x))$ cvx

**General composition rule**:
* If $h$ cvx and any one of the following
   * $h$ increasing in arg i and $f_i$ cvx
   * $h$ decreasing in arg i and $f_i$ ccv
   * $f_i$ affine
* Then $h(f_1(x), .., f_n(x))$ cvx.
