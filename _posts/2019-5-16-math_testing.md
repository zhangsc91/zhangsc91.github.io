---
layout: post
title: Welcome to my blog!
tags: [testing]
---

Inline math testing: $ \int_{i=1}^n a_i b_i $
This is not a new paragraph.

This is a new paragraph (just like LaTex).

In this new configuration, single dollar signs are for inline math, double dollar signs are for display math, just like Latex. Actual dollar sign needs a backslash: \$.

Speaking of backslash: \\

Display math testing:

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

Image in a link: 
[Cascades]({{ site.baseurl }}/images/cascades_clean.svg)

Literal Url (same image): <https://zhangsc91.github.io/images/cascades_clean.svg>

Embedded image (best to start a new paragraph): 

<img src="{{ site.baseurl }}/images/cascades_clean.svg" style="width: 400px;"/>