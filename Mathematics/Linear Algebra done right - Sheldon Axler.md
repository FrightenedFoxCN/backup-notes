# Linear Algebra done right - Sheldon Axler

## Chap. 8 Operators on Complex Vector Spaces

> Preface & Notations: When we look into an operator $T \in \mathcal L(V)$, we'd like to decompose $V$ into direct sums of the invariant subspace of it under $T$. Unfortunately decomposition into 1D subspaces, which is what we prefer is only possible under certain conditions, as shown in previous chapters. Hereby we introduce the decomposition into subspaces with dimension larger than 1 and find the simpliest representation of such decomposition by Jordan Forms, with some interesting conclusions found during the exploration for such forms.
>
> $\mathbb{F}$ denotes $\R$ or $\C$. $V$ denotes a finite-dimentional vector space over $\mathbb{F}$. Normally, $n = \dim V$ 

### Structures of null spaces and ranges of powers of an operator

**Th. 1 Sequence of increasing null spaces** Suppose $T \in \mathcal{L}(V)$, then
$$
\{0\} = \mathrm{null}\ T^0 \sub \mathrm{null}\ T^1 \sub \mathrm{null}\ T^2 \sub \cdots \sub \mathrm{null}\ T^k \sub \mathrm{null}\ T^{k+1} \sub \cdots
$$
 **Pf.** Suppose $k \in \Z^+$, $v \in \mathrm{null}\ T^k$. By definition, $T^kv = 0$, hence $T^{k+1}v = T(T^kv) = T(0)=0$, which means $\mathrm{null}\ T^k \sub \mathrm{null}\ T^{k+1}$.

> Notes: Actually, ranges observe a similar rule:
> $$
> V = \mathrm{range}\ T^0 \supset \mathrm{range}\ T^1 \supset \mathrm{range}\ T^2 \supset \cdots \supset \mathrm{range}\ T^k \supset \mathrm{range}\ T^{k+1} \supset \cdots
> $$
> Pf: Suppose $v \in \mathrm{range}\ T^k$, which means by definition $\exists u \in V, T^ku = v = T^{k - 1}(Tu)$, hence $\mathrm{range}\ T^k \sub \mathrm{range}\ T^{k - 1}$.

**Th. 2 Equality in the sequence of null spaces** Suppose $m \in \Z^+ : \mathrm{null}\ T^m = \mathrm{null}\ T^{m + 1}$, then
$$
\mathrm{null}\ T^m = \mathrm{null}\ T^{m+1} = \mathrm{null}\ T^{m+2} = \cdots
$$
**Pf.** Suppose $k \in Z^+$, we'd prove $\mathrm{null}\ T^{m+k} = \mathrm{null}\ T^{m+k+1}$. By **Th. 1**, we've already shown $\mathrm{null}\ T^{m+k} \sub \mathrm{null}\ T^{m+k+1}$.  Suppose $v \in \mathrm{null}\ T^{m+k+1}$, which means $T^{m+k+1}v = T^{m+1}(T^kv) = 0$, $T^kv \in \mathrm{null}\ T^{m+1} = \mathrm{null}\ T^m$. Therefore it's safe to conclude that $T^{m+k}v = T^m(T^kv) = 0$, which shows $\mathrm{null}\ T^{m+k} \supset \mathrm{null}\ T^{m+k+1}$, completing the proof.

> Notes: Here a similar rule for ranges is shown: Suppose $m \in \Z^+: \mathrm{range}\ T^m = \mathrm{range}\ T^{m+1}$, then
> $$
> \mathrm{range}\ T^m = \mathrm{range}\ T^{m+1} = \mathrm{range}\ T^{m+1} = \cdots
> $$
> Pf: We'd prove the inclusion in the other direction and the other things are analogical to the proof above. Suppose $v \in \mathrm{range}\ T^{m+k}$, which means $\exist u \in V, T^{m+k}u = v = T^k(T^mu)$. Because $T^mu \in \mathrm{range}\ T^m = \mathrm{range}\ T^{m+1}$, $\exist w \in V, T^{m+1}w = T^mu$. Hence $T^{m+k}u = v = T^{m+k+1}w$, which shows $\mathrm{range}\ T^{m+k} \sub \mathrm{range}\ T^{m+k+1}$, completing the proof.

**Th. 3 Null space stop growing** Suppose $T \in \mathcal{L}(V)$, $n = \dim V$, then
$$
\mathrm{null}\ T^n = \mathrm{null}\ T^{n+1} = \mathrm{null}\ T^{n+2} = \cdots
$$
**Pf.** Just notice that $\forall i \in \Z^+, \mathrm{null}\ T^i \subseteq V$, which means the dimension cannot exceed $n$ for all null spaces, then according to **Th. 1** & **Th. 2** the conclusion cannot be more obvious.

> Notes: Similar statement can also be made for ranges, which means
> $$
> \mathrm{range}\ T^n = \mathrm{range}\ T^{n+1} = \mathrm{range}\ T^{n+2} = \cdots
> $$
> Proof is omitted for clarity.
>
> Note that it doesn't has to get to $n$ to get growing for **Th 3**, yet when the power of $T$ exceeds $n$, it definitely stops growing.

**Th. 4 $V$ is the direct sum of $\mathrm{null}\ T^n$ and $\mathrm{range}\ T^n$** Suppose $T \in \mathcal{L}(V)$, $n = \dim V$, then
$$
V = \mathrm{null}\ T^n \oplus \mathrm{range}\ T^n
$$
**Pf.** First we have to show that $\mathrm{null}\ T^n \cap \mathrm{range}\ T^n = \{0\}$. Suppose $v \in \mathrm{null}\ T^n \cap \mathrm{range}\ T^n$, which by definition means $T^n = 0$ and $\exist u \in V, T^nu = v$. Hence $T^{2n}u = 0$, which by **Th. 3** indicates $T^nu = v = 0$. Then according to the equation
$$
\dim(\mathrm{null}\ T^n \oplus \mathrm{range}\ T^n) = \dim \mathrm{null}\ T^n + \dim \mathrm{range}\ T^n = \dim V
$$
the proof is complete.

> Notes: Refer to Chap. 3 for the eqn. above.

### Generalized eigenvector and eigenspace

**Def 1. generalized eigenvector** Suppose $T \in \mathcal L(V)$ and $\lambda$ is an eigenvalue of $T$. A vector $v \in V$ is called a generalized eigenvector of $T$ corresponding to $\lambda$ if $v \ne 0$ and $(T-\lambda I)^jv=0$ for some positive interger $j$.

> Notes: Sometimes it might be confusing to state eigenvalue instead of something like generalized eigenvalue in the definition above. Yet it can be shown that so-called generalized eigenvalues ($\lambda$ that $\exist v \in V$, $v \ne 0$, s. t. $(T - \lambda I)^jv=0$) are exactly the same as eigenvalues. First, eigenvalues are generalized eigenvalues, if we take $j = 1$. Also, generalized eigenvalues are eigenvalues, with proof given as follows: $\lambda$ is a generalized eigenvalue means $(T - \lambda I)^j$ is an injection, which lead to the conclusion that $T - \lambda I$ is also an injection, i. e. $\lambda$ is an eigenvalue.

