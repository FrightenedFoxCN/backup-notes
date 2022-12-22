# TCS Toolkits

## Introdution

TCS: Algorithm and Computational Complexity (Theory A) = STOC/FOCS topics

- Reading TCS papers
- Attending TCS talks
- Doing TCS research

http://cstheory-feed.org

https://sites.google.com/site.plustcs/

https://video.ias.edu/csdm

https://simons.berkeley.edu/videos

FOCS/STOC/SODA/CCC

https://arxiv.org/archive/cs

https://eccc.weizmann.ac.il

BibTex: www.ams.org/mrlookup

[tex.stackexchange.com][tex.stackexchange.com]

Street Fighting Mathematics

[The On-Line Encyclopedia of Integer Sequences® (OEIS®)](http://oeis.org)

[Inverse Symbol Calculator](http://wayback.cecm.sfu.ca/projects/ISC/ISCmain.html)

https://mathoverflow.net

https://math.stackexchange.com

https://cstheory.stackexchange,com

https://cs.stackexchange.com

Chebyshev polynomials

## Basic Asymptopia

Asymptopia, by Spencer

Concrete Mathematics, Graham-Knuth-Patashnik

Asymptotic Methods in Analysis, De Bruijn
$$
f(x) = O(g(x))( as \ x \rightarrow \infty)\\
\equiv \exists C, x_0, s.t.|f(x|\leqslant Cg(x), \forall x \geqslant x_0
$$
Similar notation when $x \rarr 0^+, \forall x \in (0,x_0]$.

Extension: $O(g(x))$ denotes an anomymous function $f(x)$, s.t. $0 \leqslant f(x) \leqslant Cg(x)$.
$$
f(x) = \Omega(g(x))( as \ x \rightarrow \infty)\\
\equiv \exists C, x_0, s.t.|f(x|\geqslant Cg(x), \forall x \geqslant x_0\\
f(x) = \Theta(g(x))( as \ x \rightarrow \infty)\\
\equiv f(x) = O(g(x)) \wedge f(x) = \Omega(g(x))\\
f(x) = o(g(x))( as \ x \rightarrow \infty) \equiv \frac {f(x)} {g(x)} = 0\\
f(x) = \omega (g(x))( as \ x \rightarrow \infty) \equiv \frac {g(x)} {f(x)} = 0\\
f(x) = \mathrm{poly}(g(x)) \equiv f(x)=g(x)^{(O(1))}\\
f(x) = \widetilde O(g(x)) \equiv f(x) \leqslant g(x)\cdot \mathrm{poly}(\log g(x))\\
f(x) = \widetilde \Omega(g(x)) \equiv f(x) \geqslant \frac {g(x)}{\mathrm{poly}(\log g(x))}
$$
When $x \rarr 0, g(x) \rarr 0$, $f(x) = \widetilde O(g(x)) \equiv f(x) \leqslant g(x)\cdot \mathrm{poly}(\frac 1 {\log g(x))}$

Sometimes, in order to show the variable, subscription $n$ is attached.

>**Notation:**
>
>$g(n)$ is in standard form if it's a product of:
>
>1. constant number
>2. constant powers of $\ln n$
>3. constant powers of $n$
>4. exponential functions
>5. $n^{Cn}$, where $C$ is a constant
>
>Each "type" is asymptolically smaller than next type, even with positive powers.

Example: Harmonic number
$$
H_n = 1 + \frac 12 + \frac 13+\frac 14+\cdots + \frac 1n \sim \ln n
$$
To get the upper bound:
$$
H_n \leqslant 1 + \frac 12 + \frac 12 + \frac 14 + \frac 14 + \cdots \leqslant [\log_2n]+1
$$
To get the lower bound:
$$
H_n \geqslant 1 + \frac 12 + \frac 14 + \frac 14 \cdots \geqslant \frac 12[\log_2n] + \frac32
$$
Therefore:
$$
H_n = \Theta(\log n)
$$
Define:
$$
f(x) \sim g(x)(as\ x \rightarrow \infty) \equiv \frac{f(x)}{g(x)} \rarr 1
$$
To prove:
$$
H_n \sim \ln(n)
$$
Draw the rectangles of which th sum of the areas is $H_n$
$$
H_n \leqslant 1 + \int_1^n \frac 1t\mathrm dt = \ln n + 1\\
H_n \geqslant \int_1^{n+1} \frac 1t\mathrm dt = \ln (n+1)
$$


## Fourier Transforms

## Algebra & Applications

## Spectral Graph Theory

## CSPs & Hierarachies

## Information & Learning

## Hardness

